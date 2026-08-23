# ADR-003 — Data de extração registrada nas séries do BCB

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-002](adr-002-series-bcb.md)

---

## Contexto

O BCB revisa séries retroativamente. Comparando o CSV gerado em março/2026 com a API em
agosto/2026, os mesmos meses retornaram valores diferentes:

| Mês | CSV de março | API em agosto |
|---|---|---|
| out/2024 | 3,17 | 3,30 |
| nov/2024 | 3,14 | 3,27 |
| dez/2024 | 2,95 | 3,08 |

## Decisão

Gravar a coluna `Data_Extracao` em `bcb_macro.csv` a cada execução.

## Consequências

Números do painel podem ser reconciliados com a data em que foram obtidos. Sem isso, uma
divergência entre o painel e o site do BCB seria indistinguível de um erro de cálculo.

O intervalo permanece fixo (01/2015–12/2024) para que o painel não mude sozinho a cada execução.
---

[← Índice das ADRs](ADR.md)
