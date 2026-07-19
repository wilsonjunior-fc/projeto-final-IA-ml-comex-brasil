# Projeto Final — Aprendizado de Máquina
## Estimativa do Valor FOB em Operações de Comércio Exterior do Brasil

## 🎯 Objetivo

Estimar o valor FOB (`VL_FOB`, em US$) de uma operação de comércio exterior brasileira a partir de características da transação (produto, país, UF, via de transporte, período etc.), identificando quais fatores mais influenciam o valor negociado.

## 👥 Integrantes

- Wilson Fernandes Carneiro Junior 
- Lucas Thiery Oliveira dos Santos
- João Bosco Montalvao Neto

## 📊 Fonte dos dados

[Data of Brazilian Import and Export data](https://www.kaggle.com/datasets/juniorfazzio/data-of-brazilian-import-and-export-data) (Kaggle), compilado a partir do [Comex Stat / MDIC](http://comexstat.mdic.gov.br/pt/home) — banco SQLite com registros de exportação e importação do Brasil de 1997 a 2021.

## 🧠 Tipo da tarefa

**Regressão.** O atributo-alvo (`VL_FOB`) é uma variável numérica contínua, não representa categorias.

- **Atributo-alvo:** `VL_FOB`
- **Atributos preditivos:** `CO_ANO`, `CO_MES`, `CO_NCM`, `CO_PAIS`, `SG_UF_NCM`, `CO_VIA`, `CO_URF`, `QT_ESTAT`, `KG_LIQUIDO`, `TIPO_OPERACAO`

## 📁 Organização dos arquivos

```
├── README.md
├── notebooks/
│   ├── 01_eda.ipynb                        # Seções 5.1 a 5.3 — Integrante 1
│   ├── 02_modelagem_base.ipynb             # Seções 5.4, 5.5, 5.6 (parte 1) — Integrante 2
│   └── 03_modelo_final_avaliacao.ipynb     # Seções 5.6 (parte 2), 5.7 — Integrante 3
└── Projeto_Final_ML_Comex.ipynb            # Notebook final consolidado (todas as seções)
```

## ▶️ Como rodar no Google Colab

1. Abra o notebook desejado no [Google Colab](https://colab.research.google.com) (Arquivo → Abrir notebook → GitHub → colar o link deste repositório).
2. Gere seu próprio token de API do Kaggle: [kaggle.com](https://www.kaggle.com) → avatar → **Settings** → aba **API** → **Generate New Token**.
3. No Colab, clique no ícone de chave 🔑 (Secrets) na barra lateral esquerda → **Add new secret** → nome exatamente `KAGGLE_API_TOKEN` → cole o valor do token → ative **Notebook access**.
4. Rode as células em ordem (Ambiente de execução → Executar tudo). O notebook baixa o dataset automaticamente via `kagglehub`, sem necessidade de upload manual.

## 🤖 Modelos utilizados

- Baseline (preditor ingênuo)
- Regressão Linear
- Árvore de Decisão
- Random Forest

## 📈 Principais resultados

*(preencher após a avaliação final: MAE, MSE, RMSE e R² do modelo escolhido)*

| Modelo | MAE | MSE | RMSE | R² |
|---|---|---|---|---|
| Baseline | | | | |
| Regressão Linear | | | | |
| Árvore de Decisão | | | | |
| Random Forest | | | | |

## 🙋 Divisão das contribuições

| Integrante | Responsabilidade |
|---|---|
| [NOME 1] | Análise exploratória e compreensão dos dados (5.1–5.3) |
| [NOME 2] | Pré-processamento, separação dos dados e modelos base (5.4–5.6 parte 1) |
| [NOME 3] | Random Forest, comparação final, avaliação e documentação (5.6 parte 2–5.7) |

## 🎥 Vídeo

[Link do vídeo explicativo]

## 🧾 Declaração de uso de Inteligência Artificial

- **Ferramenta utilizada:** [ex.: Claude / ChatGPT]
- **Finalidade:** [ex.: apoio na estruturação do notebook, revisão de código, organização da divisão de tarefas]
- **Parte do trabalho em que foi utilizada:** [ex.: estrutura inicial do notebook, revisão de texto do README]
- **Forma de verificação do conteúdo/código:** [ex.: todo código foi executado e revisado manualmente pelos integrantes antes da entrega; interpretações escritas pelos próprios integrantes após análise dos resultados]
