# Architecture Decision Records — Risco de Crédito Global

Registro das decisões técnicas do pipeline de dados, com o contexto que as motivou e as
consequências aceitas. Cada ADR responde a três perguntas: **o que foi decidido**, **por que**,
e **o que se perde com isso**.

Uma ADR por arquivo. Decisões superadas não são apagadas — recebem status *Substituída* e um
link para a que as substitui.

## Índice

| ADR | Decisão | Status |
|---|---|---|
| [001](adr-001-dominios-separados.md) | Carteira e macroeconomia como domínios separados | Aceito |
| [002](adr-002-series-bcb.md) | Séries do BCB identificadas pelo nome oficial | Aceito |
| [003](adr-003-data-extracao.md) | Data de extração registrada nas séries do BCB | Aceito |
| [004](adr-004-codigos-sentinela.md) | Códigos 96 e 98 tratados como sentinela | Aceito |
| [005](adr-005-razao-divida-renda.md) | Razão dívida/renda reconstruída | Aceito |
| [006](adr-006-winsorizacao.md) | Winsorização em vez de remoção de linhas | Aceito |
| [007](adr-007-ordem-pipeline.md) | Ordem do pipeline: tratar antes de imputar | Aceito |
| [008](adr-008-score-rank-percentil.md) | Score de risco por rank percentil | Aceito |
| [009](adr-009-encoding-exportacao.md) | Codificação e separador decimal na exportação | Aceito |
| [010](adr-010-exportacao-granular.md) | Uma agregação, um arquivo | Aceito |
| [011](adr-011-validacao-score.md) | Validação do score por asserção | Aceito |
| [012](adr-012-versionamento-dados.md) | Versionamento dos dados derivados | Aceito |

## Por tema

**Fontes de dados**
[ADR-001](adr-001-dominios-separados.md) · [ADR-002](adr-002-series-bcb.md) · [ADR-003](adr-003-data-extracao.md)

**Limpeza e tratamento**
[ADR-004](adr-004-codigos-sentinela.md) · [ADR-005](adr-005-razao-divida-renda.md) · [ADR-006](adr-006-winsorizacao.md) · [ADR-007](adr-007-ordem-pipeline.md)

**Modelagem e validação**
[ADR-008](adr-008-score-rank-percentil.md) · [ADR-011](adr-011-validacao-score.md)

**Entrega e infraestrutura**
[ADR-009](adr-009-encoding-exportacao.md) · [ADR-010](adr-010-exportacao-granular.md) · [ADR-012](adr-012-versionamento-dados.md)

---

## Referências

- [Portal de Dados Abertos do BCB — série 20631, Concessões de crédito](https://dadosabertos.bcb.gov.br/dataset/20631-concessoes-de-credito---total)
- [Portal de Dados Abertos do BCB — série 20714, Taxa média de juros](https://dadosabertos.bcb.gov.br/dataset/20714-taxa-media-de-juros-das-operacoes-de-credito---total/resource/56176dd7-6bf5-4fb7-a513-3bd742a55560)
- [Portal de Dados Abertos do BCB — série 25433, Taxa média mensal de juros](https://dadosabertos.bcb.gov.br/dataset/25433-taxa-media-mensal-de-juros-das-operacoes-de-credito---total)
- [Kaggle — Give Me Some Credit](https://www.kaggle.com/c/GiveMeSomeCredit)
