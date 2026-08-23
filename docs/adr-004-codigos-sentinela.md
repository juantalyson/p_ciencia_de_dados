# ADR-004 — Códigos 96 e 98 tratados como sentinela

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-008](adr-008-score-rank-percentil.md)

---

## Contexto

As três colunas de atraso contêm os valores 96 e 98 em 225 registros. Não são contagens: são
códigos especiais do dataset original. Interpretá-los literalmente significaria "98 atrasos de
90+ dias" para um mesmo cliente.

O impacto era estrutural. A soma ponderada `Historico_Atrasos` atingia **588**
(98 × 1 + 98 × 2 + 98 × 3), contra um percentil 99 real de **11**. Esse máximo artificial era o
denominador da normalização min-max do score — ver [ADR-008](adr-008-score-rank-percentil.md).

## Decisão

Converter valores ≥ 90 nessas colunas para nulo, imputar a mediana da coluna, e marcar os
registros afetados em uma coluna técnica `Registro_Sentinela` (não exportada ao painel).

## Consequências

`Historico_Atrasos` passa de máximo 588 para **51**. Os 225 registros são 0,15% da base —
imputar preserva as demais variáveis dessas linhas em vez de descartá-las.
---

[← Índice das ADRs](ADR.md)
