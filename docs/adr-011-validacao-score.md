# ADR-011 — Validação do score por asserção

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-008](adr-008-score-rank-percentil.md)

---

## Contexto

O defeito descrito na [ADR-008](adr-008-score-rank-percentil.md) — score não monotônico — passou
despercebido porque nada no pipeline verificava a premissa mais básica de um score de risco: que
a inadimplência **cresça** junto com ele. A célula de verificação existente declarava
"Dataset 100% limpo!" mas executava **antes** da criação das features, sem cobrir nada do que
quebrava depois.

## Decisão

Incluir asserções que interrompem a execução do notebook:

```python
assert monotonico, 'Score não é monotônico — não usar no painel'
assert df.isnull().sum().sum() == 0
assert df['Idade'].between(18, 120).all()
assert df['Razao_Divida'].max() <= 2.0
assert set(df['Inadimplente'].unique()) <= {0, 1}
```

A verificação de nulos foi movida para **depois** da criação das features.

## Consequências

Um pipeline que produza um score invertido falha em vez de exportar um CSV com aparência normal.
O custo é que alterações nos pesos exigem revalidação — que é exatamente o comportamento desejado.

Essa asserção capturaria também o defeito de `Nivel_Utilizacao`, que gerava 2.604 nulos
silenciosos (1,75%): as faixas terminavam em 1,01 enquanto a variável chegava a 747. Corrigido
com `np.inf` no limite superior, esses registros virariam a categoria "(Em branco)" nos visuais.
---

[← Índice das ADRs](ADR.md)
