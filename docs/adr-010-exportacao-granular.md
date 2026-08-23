# ADR-010 — Uma agregação, um arquivo

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-009](adr-009-encoding-exportacao.md)

---

## Contexto

A versão inicial calculava 17 indicadores mas exportava apenas 9 valores escalares. Oito
agregações — inadimplência por nível de endividamento, distribuição por faixa etária, renda
média por grupo, ranking de correlações — eram calculadas, impressas no console e **descartadas**.
Seriam justamente as tabelas de apoio a reconstruir manualmente em DAX.

A numeração dos KPIs também estava quebrada: o painel anunciava 20 indicadores, mas os de número
12, 13 e 14 não existiam.

## Decisão

Cada agregação vira um arquivo em `output/`. A numeração arbitrária foi abandonada em favor de
nomes descritivos.

| Arquivo | Conteúdo |
|---|---|
| `credit_clean.csv` | tabela fato — 149.390 clientes |
| `bcb_macro.csv` | série mensal do BCB — 120 meses |
| `kpis_resumo.csv` | 12 indicadores escalares para cartões |
| `kpi_default_por_endividamento.csv` | inadimplência e renda por nível |
| `kpi_default_por_faixa_etaria.csv` | inadimplência, renda e razão por faixa |
| `kpi_default_por_utilizacao.csv` | inadimplência por nível de utilização |
| `kpi_default_por_faixa_score.csv` | inadimplência por faixa de score |
| `kpi_correlacoes.csv` | correlação com a inadimplência, **com sinal** |
| `log_limpeza.csv` | registro das etapas de limpeza |

## Consequências

O Power BI carrega tabelas prontas em vez de recalcular agregações sobre 149 mil linhas.
Cada arquivo é pequeno o suficiente para atualização instantânea.

### Decisão relacionada: sinal das correlações

O ranking de correlações **preserva o sinal**. A versão anterior aplicava valor absoluto antes de
ordenar, o que fazia `Idade` aparecer como terceira variável mais preditiva sem revelar que a
relação é **inversa** — mais idade, menos risco (r = −0,1157). Um painel construído sobre o
ranking em valor absoluto inverteria essa leitura de negócio.
---

[← Índice das ADRs](ADR.md)
