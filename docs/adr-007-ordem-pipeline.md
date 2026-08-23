# ADR-007 — Ordem do pipeline: tratar antes de imputar

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-005](adr-005-razao-divida-renda.md), [ADR-006](adr-006-winsorizacao.md)

---

## Contexto

A versão inicial imputava a renda pela mediana **antes** de tratar os outliers. A mediana usada
como valor de preenchimento era, portanto, calculada sobre uma distribuição que ainda continha
rendas de até R$ 3.008.750.

## Decisão

Ordem fixa do pipeline:

```
carregar → deduplicar → sentinelas → imputar renda → recalcular razão → winsorizar → features → validar → exportar
```

A imputação da renda vem **antes** do recálculo da razão
([ADR-005](adr-005-razao-divida-renda.md) depende dela) e **antes** da winsorização, mas
**depois** da deduplicação e do tratamento de sentinelas, que distorcem estatísticas de resumo.

## Consequências

Cada etapa opera sobre dados já saneados pelas anteriores. A função `registrar()` grava um log
de cada etapa em `output/log_limpeza.csv`, tornando a sequência auditável sem reler o código.
---

[← Índice das ADRs](ADR.md)
