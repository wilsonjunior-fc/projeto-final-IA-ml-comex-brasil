# Projeto Final — Aprendizado de Máquina
## Estimativa do Valor FOB em Operações de Comércio Exterior do Brasil

## Objetivo

Estimar o valor FOB (`VL_FOB`, em US\$) de uma operação de comércio exterior brasileira a partir de características da transação (produto, país, UF, via de transporte, período etc.), identificando quais fatores mais influenciam o valor negociado.

## Integrantes

- João Bosco Montalvão Neto
- Lucas Thiery Oliveira dos Santos
- Wilson Fernandes Carneiro Junior


## Fonte dos dados

[Data of Brazilian Import and Export data](https://www.kaggle.com/datasets/juniorfazzio/data-of-brazilian-import-and-export-data) (Kaggle), compilado a partir do [Comex Stat / MDIC](http://comexstat.mdic.gov.br/pt/home) — banco SQLite com registros de exportação e importação do Brasil de 1997 a 2021.

## Tipo da tarefa

**Regressão.** O atributo-alvo (`VL_FOB`) é uma variável numérica contínua, não representa categorias.

- **Atributo-alvo:** `VL_FOB`
- **Atributos preditivos:** `CO_ANO`, `CO_MES`, `CO_NCM`, `CO_PAIS`, `SG_UF_NCM`, `CO_VIA`, `CO_URF`, `QT_ESTAT`, `KG_LIQUIDO`, `TIPO_OPERACAO`

## Organização dos arquivos

```
├── README.md
└── previsao_valor_fob_comex.ipynb    # Notebook único, com todas as seções (5.1 a 5.7)
```

O trabalho foi desenvolvido em um único notebook, dividido internamente por seções (5.1 a 5.7), com cada seção sinalizando o integrante responsável. A divisão de responsabilidades está detalhada na tabela "Divisão das contribuições" abaixo.

## Como rodar no Google Colab

1. Abra o notebook `previsao_valor_fob_comex.ipynb` no [Google Colab](https://colab.research.google.com) (Arquivo → Abrir notebook → GitHub → colar o link deste repositório).
2. Gere seu próprio token de API do Kaggle: [kaggle.com](https://www.kaggle.com) → avatar → **Settings** → aba **API** → **Generate New Token**.
3. No Colab, clique no ícone de chave (Secrets) na barra lateral esquerda → **Add new secret** → nome exatamente `KAGGLE_API_TOKEN` → cole o valor do token → ative **Notebook access**.
4. Rode as células em ordem (Ambiente de execução → Executar tudo). O notebook baixa o dataset automaticamente via `kagglehub`, sem necessidade de upload manual.

**Atenção:** a etapa de treinamento do Random Forest final (seção 5.7) leva cerca de 30 minutos para concluir. É esperado — não indica travamento.

## Modelos utilizados

- Baseline (preditor da mediana)
- Regressão Linear (com transformação logarítmica do alvo)
- Árvore de Decisão (`max_depth=10`, poda por `min_samples_split`)
- Random Forest (modelo final escolhido)

## Principais resultados

### Comparação de modelos (validação cruzada, 5 folds, conjunto de treino)

| Modelo | RMSE médio (CV) |
|---|---|
| Baseline (mediana) | US\$ 3.190.959,80 (± 348.713,34) |
| Regressão Linear | US\$ 2.480.931,08 (± 1.010.220,76) |
| Árvore de Decisão (max_depth=10) | US\$ 2.414.054,02 (± 865.768,81) |
| Random Forest (max_depth=10)* | US\$ 2.477.206,96 (± 3.185.410,36) |

\* Avaliado em amostra reduzida (50 mil linhas, 15 árvores) por limitação de tempo de execução no Colab gratuito — ver nota metodológica no notebook (seção 5.6). Não é diretamente comparável aos demais modelos, avaliados no conjunto de treino completo (~458 mil linhas).

Todos os modelos, exceto o baseline, foram treinados com o alvo (`VL_FOB`) transformado logaritmicamente via `TransformedTargetRegressor`, devido à assimetria extrema identificada na análise exploratória (skew ≈ 164). As métricas acima já estão revertidas para a escala original (US\$).

### Avaliação final no conjunto de teste (modelo escolhido: Random Forest, 100 árvores)

| Métrica | Valor |
|---|---|
| MAE | US\$ 66.444,74 |
| MSE | 1.310.527.958.511,27 |
| RMSE | US\$ 1.144.782,93 |
| R² | 0,8246 |

O Random Forest final foi treinado no conjunto de treino completo (100 árvores, `max_depth=10`) e avaliado uma única vez no conjunto de teste (114.613 registros nunca vistos), sem contaminação da escolha do modelo pelos dados de teste. Mais detalhes da discussão de resultados, erros e limitações estão na seção 5.7 do notebook.

## Divisão das contribuições

| Integrante | Responsabilidade |
|---|---|
| Wilson Junior | Análise exploratória e compreensão dos dados (5.1–5.3) |
| Lucas Thiery | Pré-processamento, separação dos dados e modelos base (5.4–5.6 parte 1) |
| João Bosco | Random Forest, comparação final, avaliação e documentação (5.6 parte 2–5.7) |

## Vídeo

https://drive.google.com/file/d/1A32DdUGk2ovyp3bgkAxLAHLDdU_EXYgi/view?usp=sharing

## Declaração de uso de Inteligência Artificial
**Ferramentas utilizadas:** Gemini e Claude Code.

**Finalidade:** aprimoramento de conceitos de Aprendizado de Máquina, revisão de código e apoio na depuração (debug) de erros durante o desenvolvimento.

**Parte do trabalho em que foram utilizadas:** etapas de análise exploratória (seções 5.1 a 5.3), pré-processamento e modelagem (seções 5.4 a 5.6), incluindo revisão de trechos de código e discussão de decisões técnicas (como transformação do alvo e configuração de hiperparâmetros).

**Forma de verificação:** todo código sugerido foi executado e validado pelo grupo antes de ser incorporado ao notebook, com os resultados (métricas, tempos de execução e saídas impressas) conferidos manualmente para confirmar que correspondiam ao esperado.
