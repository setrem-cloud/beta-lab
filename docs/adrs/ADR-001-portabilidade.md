# ETAPA 2 — ADR

# ADR-001: Uso de Logs Gerenciados do Provedor Cloud

## Status
Aceito

## Contexto
O sistema CloudPonto exige auditoria, rastreabilidade e observabilidade devido às exigências de compliance.

A equipe possui prazo limitado e precisa de uma solução de rápida implementação.

Alternativas:
- Stack open-source (ELK / Loki)
- Serviço gerenciado do provedor cloud

Restrições:
- Tempo curto
- Alta exigência de confiabilidade
- Equipe com pouca experiência em operação de logs complexos

## Decision
Foi adotado o uso de logs gerenciados do provedor cloud.

Essa decisão aceita explicitamente um lock-in técnico, devido à dependência de APIs proprietárias.

A escolha prioriza rapidez, simplicidade operacional e integração.

## Consequências

### Positivas
- Implementação rápida
- Baixa complexidade operacional
- Integração nativa com a cloud
- Alta disponibilidade

### Negativas — lock-in explícito
- Lock-in técnico (APIs proprietárias)
- Lock-in de dados (dificuldade de migração)
- Lock-in financeiro (alto custo de saída)

Estimativa de esforço para sair:
- Reconfiguração completa da observabilidade
- Migração de dados históricos
- Reescrita de integrações

### Mitigação
- Exportação periódica de logs
- Uso de formatos abertos (JSON)
- Documentação das integrações
- Planejamento de migração futura

## Alternatives Consideradas

| Alternativa | Prós | Contras | Por que foi descartada |
|-------------|------|---------|------------------------|
| ELK / Loki | Alta portabilidade | Alta complexidade | Exige mais tempo |
| Logs gerenciados | Simples e rápido | Alto lock-in | Escolhida |