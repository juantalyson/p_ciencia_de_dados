# ADR-008 — Score de risco por rank percentil

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-004](adr-004-codigos-sentinela.md), [ADR-006](adr-006-winsorizacao.md), [ADR-011](adr-011-validacao-score.md)

---

## Contexto

O score original combinava três variáveis normalizadas por min-max:

```
score = normalizar(utilizacao)*0.40 + normalizar(historico)*0.35 + normalizar(razao)*0.25
```

Min-max divide pela amplitude observada. Com máximos de 747, 588 e 6.467 — todos artefatos
descritos nas ADRs [004](adr-004-codigos-sentinela.md), [005](adr-005-razao-divida-renda.md) e
[006](adr-006-winsorizacao.md) — a distribuição inteira colapsava perto de zero:

| Métrica | Score original | Esperado |
|---|---|---|
| Mediana | **0,03** | ~50 |
| Percentil 75 | **0,17** | ~75 |
| Máximo | 42,1 | ~100 |
| Correlação com inadimplência | **0,0297** | — |

Pior que a escala: o score **não era monotônico**. A taxa de inadimplência por decil ia a 21,24%
no nono decil e **caía para 5,92%** no décimo — abaixo da média global de 6,68%. O grupo apontado
como o mais arriscado da carteira era, na prática, menos inadimplente que a média.

## Decisão

Substituir min-max por **rank percentil** (`Series.rank(pct=True)`), mantendo os mesmos pesos.
O rank depende apenas da posição relativa do cliente, não da magnitude absoluta, o que o torna
imune a caudas longas.

## Consequências

| Métrica | Antes | Depois |
|---|---|---|
| Mediana | 0,03 | **49,8** |
| Correlação com inadimplência | 0,0297 | **0,3045** |
| Monotônico por decil | Não | **Sim** |
| Lift (decil 10 / decil 1) | — | **40,7x** |

Inadimplência por decil após a mudança: 0,76% · 0,80% · 1,10% · 1,76% · 2,49% · 5,03% · 5,14% ·
6,49% · 12,70% · **30,75%**.

### Limitações aceitas

- O score passa a ser uma medida **relativa à carteira**. Um cliente com score 80 está no
  percentil 80 *desta base*, não numa escala absoluta comparável a outra carteira. Para o
  objetivo do painel — priorizar clientes por risco dentro da carteira — é o comportamento
  desejado. Para comparação entre carteiras, exigiria recalibração.
- Os pesos (0,40 / 0,35 / 0,25) foram herdados da versão original e **não foram otimizados**.
  São uma escolha de negócio, não um resultado estatístico. Um modelo supervisionado
  (regressão logística) estimaria pesos melhores — fora do escopo desta entrega.
---

[← Índice das ADRs](ADR.md)
