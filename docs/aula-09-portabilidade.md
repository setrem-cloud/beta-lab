# ETAPA 1 — Decisões Técnicas (6 decisões)

| # | Decisão Técnica | Descrição | Estratégia (6 Rs) |
|--|----------------|----------|------------------|
| 1 | Uso de Containers (Docker/OCI) | Aplicação empacotada em containers para padronização | Replatform |
| 2 | Orquestração com Kubernetes | Gerenciamento de containers via cluster K8s | Replatform |
| 3 | Banco de dados PostgreSQL | Uso de banco relacional open-source | Rehost |
| 4 | Autenticação com Auth0 | Serviço SaaS para autenticação | Repurchase |
| 5 | CI/CD com GitHub Actions | Pipeline automatizado para build/deploy | Replatform |
| 6 | Logs com serviço gerenciado | Uso de ferramenta nativa do provedor | Refactor |


# ETAPA 2 — Trade-offs + Análise

## Tabela de Trade-offs

| Decisão | Portabilidade | Produtividade | Custo | Complexidade |
|--------|-------------|--------------|------|-------------|
| Containers | Alta | Média | Médio | Média |
| Kubernetes | Alta | Média | Alto | Alta |
| PostgreSQL | Alta | Alta | Baixo | Baixa |
| Auth0 | Média | Alta | Médio | Baixa |
| GitHub Actions | Média | Alta | Baixo | Baixa |
| Logs gerenciados | Baixa | Alta | Médio | Baixa |

## 3 Provocações

1. Kubernetes melhora portabilidade, mas aumenta significativamente a complexidade operacional.
2. O uso de Auth0 reduz esforço de desenvolvimento, porém mantém dependência externa (lock-in de serviço).
3. Logs gerenciados simplificam a operação, mas criam forte lock-in técnico devido a APIs proprietárias.

## 4 Perguntas Originais do Caso

1. Vale a pena sacrificar portabilidade para ganhar velocidade de desenvolvimento?
2. Qual componente seria mais difícil de migrar em caso de troca de provedor?
3. A equipe atual conseguiria operar em outra cloud sem treinamento adicional?
4. Quais componentes são críticos ao negócio e deveriam ter maior portabilidade?


# ETAPA 3 — Proposta Alternativa

## Proposta

- Substituir logs gerenciados por stack open-source (ELK ou Loki)
- Avaliar autenticação baseada em padrões abertos (OAuth2/OpenID)
- Tornar o CI/CD menos dependente de plataforma específica

## Avaliação nos 3 Testes

### Teste de Portabilidade
✔ Reduz dependência de APIs proprietárias  
✔ Facilita migração entre provedores  

### Teste de Complexidade
⚠ Aumenta responsabilidade operacional  
⚠ Exige maior conhecimento técnico  

### Teste de Custo
✔ Reduz custo de longo prazo  
⚠ Aumenta custo inicial de implementação  


# SÍNTESE — Parte A

## Classificação dos Componentes

| Componente | Classificação | Justificativa |
|------------|-------------|--------------|
| API (Container OCI) | Portável | Executa em qualquer ambiente com suporte a containers |
| PostgreSQL | Portável | Banco open-source padrão |
| Kubernetes | Portável | Orquestração baseada em padrão aberto |
| GitHub Actions | Adaptável | Pode ser migrado com ajustes |
| Auth0 | Adaptável | Serviço SaaS substituível |
| Logs gerenciados | Reescrita | Dependência de APIs proprietárias |


# SÍNTESE — Parte B

## Decisão de Maior Risco de Lock-in

A decisão de maior risco de lock-in é o uso de serviços gerenciados de logs do provedor cloud.

### Justificativa
- Dependência direta de APIs proprietárias
- Dificuldade de exportação de dados
- Forte acoplamento com o provedor

### Impacto
Essa decisão pode tornar a migração lenta, cara e tecnicamente complexa.