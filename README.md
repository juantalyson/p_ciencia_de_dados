# Risco de Crédito Global — BI 

Projeto de Business Intelligence para análise de inadimplência,
desenvolvido para a disciplina de Ciência de Dados — CEUB 2026.

## Problema
Prever a probabilidade de um cliente dar calote com base em
seu histórico financeiro e no contexto macroeconômico do Brasil.

## Datasets
- **Give Me Some Credit** (Kaggle) — 150.000 clientes reais
- **Banco Central do Brasil** — séries macroeconômicas (2015–2024)

## Tecnologias
- Python (pandas, numpy, matplotlib, seaborn, scikit-learn)
- Power BI Desktop
- Jupyter Notebook / VS Code

## Estrutura
```
projeto/
  data/           ← dados brutos (não versionados)
  output/         ← CSVs gerados pelo notebook
  risco_credito_entrega1.ipynb  ← notebook principal
```

## Como executar
1. Baixe o dataset no Kaggle e coloque em `data/`
2. Execute todas as células do notebook em ordem
3. Importe os CSVs da pasta `output/` no Power BI
