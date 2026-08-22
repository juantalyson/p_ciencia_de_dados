# 🏦 Risco de Crédito Global
### Prevendo Inadimplência com Machine Learning e Business Intelligence

> **Disciplina:** Ciência de Dados — Ciência da Computação  
> **Instituição:** UniCEUB — Brasília, DF   
> **Ano:** 2026

---

## 📋 Sobre o Projeto

Toda instituição financeira precisa responder diariamente a mesma pergunta:

> *"Esse cliente vai pagar ou vai dar calote?"*

Emprestar para quem não vai pagar gera prejuízo. Negar crédito para quem pagaria gera perda de receita e de clientes.

Este projeto constrói um sistema analítico completo de **Business Intelligence** para análise de risco de crédito, combinando dados comportamentais de 150.000 clientes reais com séries macroeconômicas do Banco Central do Brasil — transformando dados brutos em decisões de negócio.

---

## 🎯 Problema de Negócio

A inadimplência impacta três dimensões críticas de qualquer instituição financeira:

- 💸 **Lucros** — prejuízo direto com crédito não recuperado
- 📉 **Concessão de crédito** — capital imobilizado reduz capacidade de emprestar
- ⚠️ **Risco financeiro** — exposição ao risco sistêmico

---

## 📊 Datasets Utilizados

| Dataset | Fonte | Nível | Descrição |
|---|---|---|---|
| Give Me Some Credit | [Kaggle](https://www.kaggle.com/competitions/GiveMeSomeCredit) | Micro — cliente individual | 150.000 registros reais com histórico financeiro |
| Séries do BCB | [dadosabertos.bcb.gov.br](https://dadosabertos.bcb.gov.br) | Macro — contexto nacional | Taxa de inadimplência, spread bancário e volume de crédito (2015–2024) |

### Por que dois datasets?

Um cliente considerado bom pagador em economia estável pode se tornar inadimplente em crise. O contexto macroeconômico explica o que os dados individuais não conseguem sozinhos.

---

## 🛠️ Tecnologias Utilizadas

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-yellow?logo=powerbi)
![VS Code](https://img.shields.io/badge/VS%20Code-Jupyter-blue?logo=visualstudiocode)
![pandas](https://img.shields.io/badge/pandas-2.0-lightblue?logo=pandas)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3-orange?logo=scikitlearn)

| Ferramenta | Versão | Finalidade |
|---|---|---|
| Python | 3.11.9 | Coleta, limpeza, análise e Feature Engineering |
| pandas | 2.0+ | Manipulação e análise de dados tabulares |
| numpy | 1.25+ | Cálculos matemáticos e estatísticos |
| matplotlib / seaborn | Atual | Criação de gráficos e visualizações |
| scikit-learn | 1.3+ | Machine Learning — K-Means e Regressão Logística |
| requests | Atual | Requisições HTTP para API do BCB |
| Power BI Desktop | 2024+ | Dashboard interativo com KPIs |
| VS Code + Jupyter | Atual | Ambiente de desenvolvimento |

---

## 📁 Estrutura do Projeto

```
p_ciencia_de_dados/
  Data Kaggle/
    data/
      cs-training.csv          ← dataset bruto (não versionado)
    output/
      bcb_macro.csv            ← séries do Banco Central
      credit_clean.csv         ← dataset limpo com features
      kpis_resumo.csv          ← KPIs calculados em Python
    GiveMeSomeCredit.zip       ← arquivo original do Kaggle
    risco_credito_entrega1.ipynb  ← notebook principal
  README.md
```

> **Regra de ouro:** `data/` é só leitura (dados brutos). `output/` é onde o código escreve os resultados.

---

## 🚀 Como Executar

### Pré-requisitos

- Python 3.10+
- VS Code com extensão Jupyter
- Power BI Desktop (gratuito)

### Passo a passo

**1. Clonar o repositório**
```bash
git clone https://github.com/juantalyson/p_ciencia_de_dados.git
cd p_ciencia_de_dados/Data\ Kaggle
```

**2. Instalar as dependências**
```bash
pip install pandas numpy matplotlib seaborn requests openpyxl scikit-learn
```

**3. Baixar o dataset do Kaggle**
- Acesse: [kaggle.com/competitions/GiveMeSomeCredit](https://www.kaggle.com/competitions/GiveMeSomeCredit/data)
- Baixe o arquivo `cs-training.csv`
- Coloque-o na pasta `data/`

**4. Executar o notebook**
```bash
# Abrir no VS Code
code risco_credito_entrega1.ipynb

# Ou via Jupyter
jupyter notebook risco_credito_entrega1.ipynb
```

Execute todas as células em ordem. Os dados do BCB são baixados automaticamente via API.

**5. Abrir o dashboard no Power BI**
- Abra o Power BI Desktop
- Importe os 3 CSVs da pasta `output/`
- Ou abra diretamente o arquivo `Dashboard_Risco_Credito.pbix`

---

## 🔬 Conceitos de Ciência de Dados Aplicados

| # | Conceito | Como foi aplicado |
|---|---|---|
| 01 | **Coleta de Dados** | API pública do BCB (sem cadastro) + Kaggle |
| 02 | **Limpeza e Pré-processamento** | Imputação com mediana/moda, remoção de outliers via Z-Score |
| 03 | **Estatísticas Descritivas** | Média, mediana, desvio padrão, quartis, distribuições |
| 04 | **Análise Exploratória (EDA)** | Identificação de padrões, anomalias e correlações |
| 05 | **Criação de Novas Variáveis** | Faixa etária, Score de Risco, Nível de Endividamento |
| 06 | **Machine Learning** | K-Means (segmentação) + Regressão Logística (predição) |

---

## 📈 Principais Resultados

### KPIs Calculados

| KPI | Resultado | Interpretação |
|---|---|---|
| Taxa Global de Inadimplência | **6.68%** | 7 em cada 100 clientes deram calote |
| Utilização Média de Crédito | **42.16%** | Nível moderado — espaço para crescer |
| Clientes com Atraso Grave | **1.03%** | Poucos, mas de alto risco |
| Inadimplência Nacional (BCB) | **2.95%** | Contexto macro saudável |
| Variação Mensal | **-0.190%** | Tendência de queda — sinal positivo |
| Correlação Spread × Inadimplência | **0.769** | Correlação forte — juros sobem, calotes sobem |

### 5 Insights do Projeto

**1. Endividamento e inadimplência andam juntos**
Clientes com maior nível de endividamento têm taxas mais altas de calote. O nível ALTO (8.18%) supera o CRÍTICO (6.84%) — clientes extremamente endividados já são filtrados pelo próprio sistema antes de receber crédito.

**2. Alta utilização de crédito = maior risco**
Clientes usando 75-100% do limite têm probabilidade de inadimplência significativamente superior à média.

**3. Histórico de atraso é o melhor preditor**
As variáveis de atraso (30-59d, 60-89d, 90d+) são as mais correlacionadas com inadimplência futura. Comportamento passado prediz comportamento futuro.

**4. Contexto macro importa**
Correlação de 0.769 entre spread bancário e inadimplência nacional. Quando os juros sobem, mais gente não consegue pagar.

**5. Concentração de risco em grupos específicos**
A segmentação K-Means identificou 4 perfis distintos — permite estratégias diferenciadas: aprovação automática para conservadores, análise manual para críticos.

---

## 🤖 Machine Learning

### K-Means — Segmentação de Clientes

Agrupa os 148.799 clientes em 4 perfis de risco sem supervisão:

| Perfil | Característica | Estratégia sugerida |
|---|---|---|
| 🟢 Conservador | Baixo endividamento, sem atrasos | Aprovação automática, limite maior |
| 🟡 Moderado | Endividamento médio, atrasos leves | Aprovação padrão |
| 🟠 Arriscado | Alta utilização, histórico de atrasos | Aprovação com análise |
| 🔴 Crítico | Múltiplos atrasos graves, alto endividamento | Análise manual obrigatória |

### Regressão Logística — Predição Individual

Estima a probabilidade de cada cliente dar calote:

```
Entrada: idade, renda, utilização, histórico de atrasos, endividamento
    ↓
Modelo calcula com pesos aprendidos em 118.000+ casos históricos
    ↓
Saída: probabilidade = 0.73 → 73% de chance de calote
       classificação = Inadimplente
```

**Métricas esperadas:**
- F1-Score: ~0.30 (métrica principal — dataset desbalanceado)
- Recall de inadimplentes: ~0.77 (77% dos calotes detectados)
- AUC-ROC: ~0.75-0.80

> **Por que F1-Score e não acurácia?** Com 93% de adimplentes, um modelo que sempre diz "vai pagar" teria 93% de acurácia — mas seria inútil. O F1-Score equilibra Precisão e Recall, focando em detectar calotes.

---

## 📊 Dashboard Power BI

O dashboard tem 4 páginas navegáveis:

| Página | Conteúdo |
|---|---|
| 1 — Visão Geral | Taxa de inadimplência, utilização de crédito, série temporal BCB |
| 2 — Perfil de Risco | Distribuição por faixa etária, nível de endividamento, atrasos |
| 3 — Clusters | Segmentação K-Means com gráfico de bolhas e mapa de calor |
| 4 — Performance | Matriz de confusão e métricas do modelo preditivo |

---

## 📂 Arquivos Gerados

| Arquivo | Descrição | Linhas |
|---|---|---|
| `output/credit_clean.csv` | Dataset limpo com 16 colunas (11 originais + 5 features) | 148.799 |
| `output/bcb_macro.csv` | Séries macroeconômicas do BCB (2015-2024) | 120 |
| `output/kpis_resumo.csv` | 9 KPIs escalares calculados em Python | 9 |

---

## 🧹 Limpeza dos Dados

| Problema | Coluna | Solução | Justificativa |
|---|---|---|---|
| 19.82% de nulos | Renda_Mensal | Mediana por faixa etária | Renda assimétrica — mediana mais robusta que média |
| 2.62% de nulos | Dependentes | Moda (valor = 0) | Variável inteira — média geraria decimal sem sentido |
| Idade = 0 | Idade | Remover linha | Dado impossível — cliente não existe |
| max = 50.708 | Utilizacao_Credito | Z-Score > 3 | Erro de cadastro — 5.070.800% do limite é impossível |
| max = 329.664 | Razao_Divida | Z-Score > 3 | Nenhum cliente deve 329k vezes a renda |

**Resultado:** 150.000 → 148.799 linhas (apenas 0.80% removido)

---

## 📚 Referências

- [Give Me Some Credit — Kaggle](https://www.kaggle.com/competitions/GiveMeSomeCredit)
- [API de Dados Abertos — Banco Central do Brasil](https://dadosabertos.bcb.gov.br)
- [Documentação pandas](https://pandas.pydata.org/docs/)
- [Documentação scikit-learn](https://scikit-learn.org/stable/)
- [Power BI Desktop](https://powerbi.microsoft.com/pt-br/desktop/)

---

## 👥 Equipe

| Nome | Função |
|---|---|
| Gabriela | Análise exploratória e visualizações |
| Juan Talysson | Coleta de dados, limpeza e Machine Learning |
| Maria Elis | Feature Engineering, KPIs e dashboard Power BI |

---

<div align="center">

**Ciência da Computação — UniCEUB**  
**Disciplina: Ciência de Dados — 2026**

*"Transformando dados em decisões."*

</div>
