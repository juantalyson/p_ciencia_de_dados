# ADR-009 — Codificação e separador decimal na exportação

**Status:** Aceito
**Data:** 2026-08-22
**Relacionadas:** [ADR-010](adr-010-exportacao-granular.md)

---

## Contexto

Os arquivos são consumidos pelo Power BI, frequentemente em ambiente pt-BR.

## Decisão

Exportar todos os CSVs com `encoding='utf-8-sig'` e ponto como separador decimal
(padrão do pandas).

## Consequências

- O BOM do `utf-8-sig` faz o Excel e o Power BI reconhecerem acentuação automaticamente.
- **Exige configuração no Power Query:** a origem do arquivo deve ser definida como
  *Inglês (Estados Unidos)*. Sem isso, em ambiente pt-BR o valor `0.766` é interpretado como
  `766` e todos os percentuais e razões ficam inflados por três ordens de grandeza.
- A alternativa (`decimal=','`) foi descartada por quebrar a releitura dos arquivos em pandas.
---

[← Índice das ADRs](ADR.md)
