# ADR-005 — Razão dívida/renda reconstruída

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-007](adr-007-ordem-pipeline.md), [ADR-006](adr-006-winsorizacao.md)

---

## Contexto

O campo `DebtRatio` apresentava 23,4% dos valores acima de 1 — impossível para uma razão bem
formada. A investigação segmentando pela presença de renda revelou a causa:

| Subconjunto | n | Mediana | p90 | % acima de 1 |
|---|---|---|---|---|
| Renda **presente** | 120.269 | 0,296 | 0,76 | 6,0% |
| Renda **ausente** | 29.731 | **1.159,00** | 3.785,00 | **93,9%** |

Onde a renda mensal é nula, `DebtRatio` não guarda uma razão: guarda o **valor absoluto** da dívida.

Isso corrompia o KPI de inadimplência por nível de endividamento, que saía não monotônico —
"Alto" com 8,18% de default contra "Crítico" com 6,84%. Um painel publicando esse gráfico
afirmaria que clientes criticamente endividados dão menos calote que os muito endividados.

## Decisão

Com a renda já imputada ([ADR-007](adr-007-ordem-pipeline.md)), reconstruir a razão nesses registros:

```
Razao_Divida = divida_absoluta / Renda_Mensal_imputada
```

## Consequências

- A mediana do subconjunto afetado cai de 1.159,00 para **0,217**, alinhando-se ao subconjunto
  íntegro (0,296).
- O KPI passa a destacar "Crítico" com **9,03%** de default, a maior taxa entre os quatro níveis.

### Limitação aceita

A razão reconstruída herda o erro da renda imputada. É uma estimativa, não uma medição.
A coluna `Renda_Imputada` (0/1) fica no arquivo exportado para que o painel possa segmentar
ou excluir esses registros.
---

[← Índice das ADRs](ADR.md)
