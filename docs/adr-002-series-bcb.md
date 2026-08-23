# ADR-002 — Séries do BCB identificadas pelo nome oficial

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-001](adr-001-dominios-separados.md), [ADR-003](adr-003-data-extracao.md)

---

## Contexto

A versão inicial baixava três séries do SGS com rótulos atribuídos por suposição. A conferência
no Portal de Dados Abertos do BCB mostrou que dois dos três estavam incorretos:

| Código | Rótulo atribuído | Nome oficial | Unidade real |
|---|---|---|---|
| 21082 | `Inadimplencia_Pct` | Inadimplência da carteira — Total | % ✅ |
| 20714 | `Concessoes_Credito_Mi` | Taxa média de juros das operações de crédito — Total | **% a.a.** ❌ |
| 25433 | `Spread_Medio_Pct` | Taxa média **mensal** de juros das operações de crédito | **% a.m.** ❌ |

Duas evidências quantitativas confirmaram o erro:

- **Implausibilidade de grandeza.** O rótulo indicava concessões de "R$ 28 milhões/mês". As
  concessões reais no Brasil giram em torno de R$ 600 bilhões/mês — erro de quatro ordens de grandeza.
- **Redundância.** As colunas 20714 e 25433 têm correlação de **0,999861** entre si, e
  `(1 + mensal/100)^12 − 1 = anual` com erro médio de 0,038 p.p. São a mesma variável em
  periodicidades diferentes.

## Decisão

1. Renomear 20714 para `Juros_Medio_Aa_Pct`.
2. **Descartar** a série 25433 — não acrescenta informação ao modelo.
3. Adicionar a série **20631** (*Concessões de crédito — Total*, em R$ milhões), que é o
   indicador originalmente pretendido. Valor verificado: R$ 699.427 milhões em dez/2024.

## Consequências

- O KPI antes chamado "Spread Bancário Médio" deixa de existir. Spread bancário no Brasil fica
  em torno de 30 p.p.; o valor exibido (1,98%) era taxa de juros mensal.
- A correlação juros × inadimplência (r = 0,776) permanece válida — apenas passa a ser rotulada
  corretamente.
- Um nome de coluna errado é mais perigoso que um dado ausente: ele é publicado com aparência
  de certeza. Rótulos de séries externas passam a exigir conferência na fonte.
---

[← Índice das ADRs](ADR.md)
