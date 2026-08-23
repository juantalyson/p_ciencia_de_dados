# ADR-012 — Versionamento dos dados derivados

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-010](adr-010-exportacao-granular.md)

---

## Contexto

O repositório versiona hoje ~28 MB de dados: `GiveMeSomeCredit.zip` (5,4 MB),
`data/cs-training.csv` (7,6 MB) e `output/credit_clean.csv` (16,1 MB). O último é **derivado** —
regenerado integralmente a cada execução do notebook.

## Opções

1. **Ignorar `output/`.** O repositório fica leve e nenhuma reexecução gera diff. Em contrapartida,
   quem clonar precisa rodar o notebook (com acesso à internet, pela API do BCB) antes de abrir o painel.
2. **Ignorar apenas `credit_clean.csv`.** Mantém versionadas as tabelas de KPI, que são pequenas
   (menos de 1 KB cada) e úteis para inspeção direta no GitHub.
3. **Manter tudo.** Clone funciona sem execução; o custo é um diff de 16 MB a cada reexecução.

## Decisão

**Opção 2.** Ignorar os dados derivados, manter versionadas as tabelas de KPI.

O `.gitignore` cobre:

| Caminho | Motivo |
|---|---|
| `Data Kaggle/output/credit_clean.csv` | 16 MB, regenerado a cada execução |
| `Data Kaggle/data/` | `cs-training.csv` é extraído de `GiveMeSomeCredit.zip` pelo notebook |

Permanece versionado: `GiveMeSomeCredit.zip` (fonte, 5,4 MB), as sete tabelas de KPI
(menos de 1 KB cada) e `bcb_macro.csv` (4,9 KB).

Os arquivos foram removidos do índice com `git rm --cached`, que os desversiona **sem apagá-los
do disco** — o painel local continua funcionando sem reexecutar nada.

## Consequências

- O repositório deixa de carregar 23,6 MB de dados reconstruíveis. Reexecutar o notebook não
  gera mais diff de 16 MB.
- As tabelas de KPI ficam legíveis direto no GitHub, sem clonar.
- **Custo aceito:** quem clonar precisa executar o notebook antes de abrir o painel — o que exige
  acesso à internet, pela chamada à API do BCB. O `GiveMeSomeCredit.zip` versionado garante que
  a parte da carteira não depende de download externo.
- Blobs já existentes no histórico não são removidos por esta decisão. O repositório continua
  com ~28 MB de histórico; a mudança evita o **crescimento** futuro, não o passivo.
---

[← Índice das ADRs](ADR.md)
