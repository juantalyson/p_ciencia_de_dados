# ADR-006 — Winsorização em vez de remoção de linhas

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-008](adr-008-score-rank-percentil.md), [ADR-005](adr-005-razao-divida-renda.md)

---

## Contexto

O corte por *média + 3 desvios-padrão* falha em distribuições muito assimétricas: os próprios
outliers inflam o desvio-padrão, e o limite resultante ultrapassa os valores que deveria cortar.

| Coluna | p99 real | Limite por média+3σ | Removidos |
|---|---|---|---|
| `Utilizacao_Credito` | 1,09 | **755,31** | 191 de 3.321 acima de 1 |
| `Razao_Divida` | 4.979 | **6.466** | 659 |
| `Renda_Mensal` | 25.000 | 49.824 | 321 |

O método removia 1.201 de 150.000 linhas (0,80%) e deixava na base máximos de 747 para utilização
e 6.467 para razão dívida/renda — exatamente os valores que quebravam o score e as faixas.

## Decisão

Winsorizar (limitar ao teto) em vez de remover:

| Coluna | Teto | Critério |
|---|---|---|
| `Utilizacao_Credito` | p99 | percentil |
| `Renda_Mensal` | p99 | percentil |
| `Razao_Divida` | **2,0** | teto de negócio — dívida igual a 200% da renda |

## Consequências

- Retenção sobe para **99,59%** (149.390 linhas). Winsorizar preserva as demais variáveis do
  registro; remover descarta o cliente inteiro por causa de um campo.
- O teto de 2,0 na razão afeta 2,3% das linhas e a torna legível em gráficos — o corte por p99
  ainda deixaria o máximo em 272.
- A escolha do teto não afeta o score, que usa rank percentil
  ([ADR-008](adr-008-score-rank-percentil.md)): a ordenação relativa é preservada sob qualquer
  transformação monotônica.

### Limitação aceita

Valores winsorizados deixam de refletir a magnitude original. Para distribuição da variável isso
é adequado; para somatórios financeiros, não seria.
---

[← Índice das ADRs](ADR.md)
