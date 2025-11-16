# Classificação de Doenças Cardíacas

Este repositório contém o trabalho da disciplina de Fundamentos de Inteligência Artificial (FIA), focado na construção de uma Rede Neural Artificial (ANN) para classificação binária de doenças cardíacas. Este trabalho foi realizado por alunos do curso de Engenharia de Software da Universidade Federal do Amazonas

## Integrantes

* Lucas da Silva Moura - lucas.dasilvamoura@icomp.ufam.edu.br
* Luiz Felipe Nery Soares - luiz.nery@icomp.ufam.edu.br
* Rafael Emanuel Dantas Viana - rafael.emanuel@icomp.ufam.edu.br
* Sarah Campos Fernandes Lima - sarah.lima@icomp.ufam.edu.br
* Sofia da Silva Souza - sofia.souza@icomp.ufam.edu.br
* Victor José Nunes Kossmann - victor.kossmann@icomp.ufam.edu.br

---

## 1. Contexto e Objetivo do Problema

As doenças cardiovasculares são a principal causa de morte em todo o mundo, tornando a detecção precoce um desafio crítico para a saúde pública .

O objetivo deste projeto é construir um modelo de classificação binária capaz de prever a **presença (1)** ou **ausência (0)** de doença cardíaca em um paciente, com base em um conjunto de atributos clínicos .

## 2. Conjunto de Dados (Dataset)

O projeto utiliza o dataset "Heart Disease UCI", disponível no Kaggle .

* **Fonte:** [Heart Disease UCI (Kaggle)](https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset)
* **Características:** O conjunto de dados original possui 14 atributos. Para este modelo, utilizamos 13 atributos clínicos como features (entradas), incluindo `age` (idade), `sex` (sexo), `cp` (tipo de dor no peito), `trestbps` (pressão arterial em repouso) e `chol` (colesterol sérico) .
* **Variável-Alvo:** A coluna `target` é a nossa saída, onde **0** indica ausência de doença e **1** indica presença .
* **Amostras:** A versão do dataset utilizada no notebook contém 1025 amostras [cell 7].

## 3. Fluxo de Trabalho (Metodologia)

O Jupyter Notebook (`heart_disease.ipynb`) segue um fluxo completo de análise e modelagem de dados:

1.  **Importação e Análise Exploratória (EDA):** Os dados foram carregados com `pandas`. As bibliotecas `matplotlib` e `seaborn` foram usadas para visualizar a distribuição dos dados (histogramas), a correlação entre variáveis (heatmap) e outras relações (gráficos de barra e pontos) [cells 21, 23, 25, 27].
2.  **Pré-processamento e Normalização:**
    * As 13 features (X) e a variável alvo (y) foram separadas [cell 29].
    * Foi aplicado um passo crucial de **normalização** nas features (X) [cell 33]. Isso é vital para redes neurais, pois os atributos possuem escalas muito diferentes (ex: `age` ~29-77 vs. `chol` ~126-564) . A normalização (média 0, desvio padrão 1) garante que o modelo não seja enviesado por atributos com valores maiores.
3.  **Divisão dos Dados:** O conjunto foi dividido em 80% para treino e 20% para teste (`train_test_split`) [cell 37].
4.  **Construção do Modelo (Classificação Binária):**
    * Foi construída uma Rede Neural Artificial (ANN) feedforward usando a API `Sequential` do Keras [cell 55].
    * **Arquitetura:** O modelo possui 2 camadas ocultas (com 16 e 8 neurônios, respectivamente) usando a ativação `ReLU` .
    * **Regularização:** Para evitar overfitting, foram aplicadas camadas de `Dropout` (0.25) e regularização `L2` nas camadas densas [cell 55, source 27].
    * **Camada de Saída:** A camada final contém 1 neurônio com ativação `sigmoid`, ideal para classificação binária, pois retorna uma probabilidade entre 0 e 1 [cell 55, source: 31].
5.  **Treinamento:** O modelo foi compilado com a função de perda `binary_crossentropy` (adequada para problemas binários) e o otimizador `rmsprop`. Foi treinado por 50 épocas [cells 55, 57].

## 4. Resultados e Avaliação

O desempenho do modelo binário foi avaliado no conjunto de teste (20% dos dados) [cell 63].

* **Acurácia:** O modelo atingiu uma acurácia geral de **91,7%** [cell 63 output].

### Relatório de Classificação (Binário)

| Classe | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| 0 (Sem Doença) | 0.93 | 0.90 | 0.91 | 100 |
| 1 (Com Doença) | 0.91 | 0.93 | 0.92 | 105 |
| **Média (Pond.)** | **0.92** | **0.92** | **0.92** | **205** |

A **Matriz de Confusão** (visualizada no notebook) confirma o bom desempenho, mostrando que o modelo teve uma taxa baixa de falsos positivos e falsos negativos [cell 63].

## 5. Conclusão

O modelo de rede neural demonstrou ser altamente eficaz para esta tarefa, alcançando uma acurácia de 91,7% na previsão de doenças cardíacas.

O passo de **normalização de características** foi fundamental para o sucesso do modelo . Sem ele, a rede neural teria dificuldade em convergir, pois atributos com escalas maiores (como `chol`/colesterol) dominariam o processo de aprendizado em detrimento de outros com valores menores (como `sex` ou `cp`). Isso confirma a importância do pré-processamento adequado ao trabalhar com redes neurais.

Transformar todas as 13 características para terem uma escala semelhante, através da Padronização (onde todas elas têm média 0 e desvio padrão 1), permite que o otimizador funcione de forma muito mais rápida e estável, ajudando o modelo a encontrar a melhor combinação de pesos. Dessa forma, o modelo é capaz de alcançar um alto nível de acurácia.
