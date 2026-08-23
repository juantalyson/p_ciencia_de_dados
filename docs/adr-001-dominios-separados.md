# ADR-001 — Carteira e macroeconomia como domínios separados

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-002](adr-002-series-bcb.md)

---

## Contexto

O projeto combina duas fontes: o dataset *Give Me Some Credit* (Kaggle, 2011) e séries do
Banco Central do Brasil. Duas incompatibilidades impedem tratá-las como um modelo único:

1. **Sem chave temporal.** A base de clientes não possui coluna de data — nenhuma. Não existe
   campo que permita relacioná-la a uma série mensal.
2. **Populações distintas.** O dataset é de consumidores **norte-americanos**, com renda em USD,
   coletado em 2011. As séries do BCB descrevem o mercado de crédito **brasileiro** de 2015 a 2024.

## Decisão

Manter as duas bases como domínios independentes no modelo do Power BI, sem relacionamento.
O BCB entra como **contexto setorial** — um painel de mercado — e não como variável explicativa
do comportamento da carteira.

## Consequências

- O painel terá seções separadas: *perfil de risco da carteira* e *contexto do crédito no Brasil*.
- Comparações entre as duas (ex.: 6,70% de inadimplência da carteira contra 3,08% nacional) são
  legítimas como ilustração, desde que declaradas como bases distintas.
- Fica **vedado** afirmar que a macroeconomia brasileira explica a inadimplência dessa carteira.
  Seria uma correlação espúria entre populações que não se sobrepõem.
---

[← Índice das ADRs](ADR.md)
