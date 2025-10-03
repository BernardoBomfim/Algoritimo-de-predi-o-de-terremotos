# 🌍 Classificação de Alertas de Terremoto: Uma Análise Comparativa entre Modelos K-NN e SVC

---

## 🎯 Objetivo do Projeto

Este projeto de Machine Learning visa **comparar a eficácia** dos algoritmos **K-Nearest Neighbors (KNN)** e **Support Vector Machine (SVC) com kernel linear** na classificação dos diferentes níveis de alerta (multi-classe) de um dataset de terremotos.

O foco é analisar a relação entre a complexidade do modelo (abordagem local vs. global) e as métricas de desempenho (**Acurácia** e **F1-Score**), demonstrando qual abordagem é mais adequada para prever alertas sísmicos.

### Informações do Trabalho

| Atribuições | Detalhes |
| :--- | :--- |
| **Instituição** | FATEC SHUNJI NISHIMURA |
| **Autores** | Bernardo Braga Bomfim, Eduardo Ribeiro de Morais |
| **Ano** | 2025 |

---

## 📚 Dataset: Alertas de Terremoto

O experimento utilizou o dataset de alertas de terremoto para a tarefa de classificação multiclasse.

### Fonte e Link
| Detalhe | Valor |
| :--- | :--- |
| **Nome do Arquivo** | `earthquake_alert_balanced_dataset.csv` |
| **Plataforma** | Kaggle |
| **URL** | [https://www.kaggle.com/datasets/ahmeduzaki/earthquake-alert-prediction-dataset](https://www.kaggle.com/datasets/ahmeduzaki/earthquake-alert-prediction-dataset) |

### Características do Dataset

* **Tamanho:** 1300 entradas.
* **Integridade:** Todas as colunas numéricas estão completas (sem valores nulos).
* **Alvo:** `alert` (nível de alerta - classificação multiclasse).
* **Colunas Principais:**
    * `magnitude`: intensidade do terremoto (float64).
    * `depth`: profundidade do evento em km (float64).
    * `cdi`: índice de intensidade percebida (float64).
    * `mmi`: índice de intensidade modificada (float64).
    * `sig`: nível de significância do evento (float64).

---

## 🛠️ Tecnologias e Stack

O projeto está contido em um **Jupyter Notebook**, garantindo a reprodutibilidade e documentação interativa.

| Componente | Ferramenta/Biblioteca | Versão | Função |
| :--- | :--- | :--- | :--- |
| **Linguagem** | Python | 3.13 | Linguagem de programação central. |
| **Dados** | Pandas | 2.3.3 | Manipulação e leitura do dataset. |
| **Machine Learning** | Scikit-learn | 1.7.2 | Treinamento, pré-processamento (`StandardScaler`, `LabelEncoder`) e avaliação de modelos. |
| **Visualização** | Matplotlib & Seaborn | 3.10.6 & 0.13.2 | Criação de gráficos, como Matrizes de Confusão e comparação de métricas. |

---

## 🧪 Metodologia e Modelos

O experimento de classificação foi conduzido em três etapas: **Pré-processamento**, **Treinamento e Predição**, e **Avaliação**.

### 1. Pré-processamento

* **Codificação:** A coluna alvo (`alert`) foi convertida de nominal para numérica (`LabelEncoder`).
* **Divisão:** O dataset foi dividido em conjuntos de **Treino (80%)** e **Teste (20%)** com estratégia estratificada (`stratify=y`).
* **Normalização:** As características foram padronizadas (`StandardScaler`) para otimizar modelos baseados em distância.

### 2. Modelos em Comparação

| Modelo | Descrição | Configuração Principal | Hipótese |
| :--- | :--- | :--- | :--- |
| **K-Nearest Neighbors (KNN)** | Classificador baseado em instância. A classificação é feita pela maioria de `k` vizinhos mais próximos. | `n_neighbors=5` | Esperado um bom desempenho, pois a normalização otimiza a métrica de distância para padrões agrupados. |
| **Support Vector Machine (SVC)** | Classificador que busca um hiperplano de separação. | `kernel='linear'` | Escolhido para avaliar se a relação entre as variáveis e o alerta é linearmente separável. |

### 3. Métricas de Avaliação

As seguintes métricas foram utilizadas para a comparação:

* **Acurácia (Accuracy):** Proporção de previsões corretas sobre o total.
* **F1-Score (Média Ponderada):** Média harmônica de Precisão e Recall. É a métrica principal por ser mais robusta em classificações multi-classe, equilibrando falsos positivos e falsos negativos.

---

## 📈 Resultados e Conclusão

### Comparação de Desempenho

O modelo **K-Nearest Neighbors (KNN)** demonstrou um desempenho significativamente superior ao **SVC (Linear)**.

| Modelo | Acurácia | F1-Score |
| :--- | :--- | :--- |
| **KNN (k=5)** | **0.84** | **0.84** |
| **SVC (Linear)** | 0.67 | 0.66 |

* **KNN:** Apresentou a maior parte das classificações corretas (concentrada na diagonal da Matriz de Confusão), com erro aceitável (maioria dos erros sendo "falsos positivos de risco" na classe C0).
* **SVC (Linear):** Demonstrou dificuldades críticas, especialmente nas classes C1 e C3, com alta incidência de Falsos Negativos.

### Conclusão Principal

O experimento demonstrou que o problema de classificação de alertas de terremoto neste conjunto de dados **não é linearmente separável**. O modelo baseado em proximidade local (**KNN**) foi capaz de capturar a estrutura não-linear dos dados e modelar as fronteiras de decisão com muito mais eficácia.

---

## 💡 Sugestões para Trabalhos Futuros

Para aprimorar o estudo, sugerimos as seguintes melhorias:

1.  **Hyperparameter Tuning:** Otimizar o KNN testando diferentes valores de $k$ (além de $k=5$) e métricas de distância.
2.  **Kernel Não-Linear para SVC:** Reavaliar o SVC utilizando um kernel não-linear, como o **RBF (Radial Basis Function)**, para verificar se ele pode superar o KNN ao mapear relações complexas.
3.  **Análise de Features:** Aplicar técnicas de Feature Selection para determinar se a remoção de variáveis de baixa relevância pode simplificar o modelo e melhorar o desempenho.