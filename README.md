# 🐞 Software Bug Prediction using Decision Trees and Random Forest

## 📖 Sobre o Projeto

Este projeto aplica técnicas de Machine Learning para prever a ocorrência de bugs em arquivos de software a partir de métricas extraídas do histórico de desenvolvimento.

O estudo utiliza métricas relacionadas à evolução do código-fonte, como número de versões, autores, linhas adicionadas e removidas, permitindo identificar padrões associados à introdução de defeitos em sistemas de software.

Além da construção dos modelos, o projeto analisa:

* Importância das variáveis;
* Impacto dos hiperparâmetros;
* Matrizes de confusão;
* Comparação entre Árvores de Decisão e Random Forest.

---

## 🎯 Objetivos

* Identificar arquivos com maior probabilidade de conter bugs;
* Avaliar modelos supervisionados de classificação;
* Interpretar os fatores mais relevantes para a ocorrência de defeitos;
* Comparar o desempenho de Árvores de Decisão e Random Forest.

---

## 📊 Dataset

O projeto utiliza o dataset **Metrics**, composto por métricas históricas de arquivos de software.

### Variável Alvo

| Classe | Significado                   |
| ------ | ----------------------------- |
| BUG    | Arquivo com ocorrência de bug |
| NO_BUG | Arquivo sem ocorrência de bug |

### Informações Gerais

* 997 registros
* 15 atributos preditores
* Problema de classificação binária
* Dataset desbalanceado

Distribuição das classes:

| Classe | Percentual |
| ------ | ---------- |
| NO_BUG | ~79%       |
| BUG    | ~21%       |

---

## 📈 Métricas Utilizadas

As métricas representam características do histórico de manutenção dos arquivos.

Exemplos:

| Variável      | Descrição             |
| ------------- | --------------------- |
| n_versions    | Número de versões     |
| n_authors     | Número de autores     |
| lines_added   | Linhas adicionadas    |
| lines_deleted | Linhas removidas      |
| code_churn    | Alterações acumuladas |
| age           | Idade do arquivo      |
| fixes         | Número de correções   |

Essas informações ajudam a identificar arquivos mais propensos a apresentar defeitos.

---

## 🛠 Tecnologias Utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Scikit-Learn

---

## 🌳 Modelo 1 — Árvore de Decisão

Foi construída uma Árvore de Decisão utilizando:

```python
DecisionTreeClassifier(
    criterion="gini",
    max_depth=2,
    min_samples_leaf=50
)
```

### Principais Variáveis Identificadas

A árvore indicou como atributos mais relevantes:

1. `lines_added`
2. `n_authors`
3. `n_versions`

Essas variáveis foram utilizadas nos primeiros níveis da árvore, indicando maior capacidade de separar arquivos com e sem bugs.

---

## 📊 Avaliação da Árvore

### Resultados

| Métrica         | Valor |
| --------------- | ----- |
| Acurácia Treino | 83.5% |
| Acurácia Teste  | 86.8% |

Os resultados mostram boa capacidade de generalização, sem sinais evidentes de overfitting.

---

## ⚙️ Teste de Hiperparâmetros

Foram avaliadas diferentes combinações de:

* Profundidade máxima (`max_depth`)
* Número mínimo de exemplos por folha (`min_samples_leaf`)

### Configurações Testadas

```text
Depth: 4, 5, 6
Leaf: 5, 30, 60
```

### Melhor Resultado

```text
Accuracy ≈ 86.8%
```

Obtido em configurações com aproximadamente:

```text
min_samples_leaf = 30
```

---

## 📉 Matriz de Confusão

A análise mostrou que o modelo:

✅ Classifica muito bem arquivos sem bugs

⚠️ Possui mais dificuldade para identificar todos os arquivos com bugs.

Isso ocorre devido ao desbalanceamento das classes, já que a maioria dos registros pertence à categoria NO_BUG.

---

## 🌲 Modelo 2 — Random Forest

Foi treinado um modelo Random Forest utilizando:

```python
RandomForestClassifier(
    n_estimators=200,
    max_features=3
)
```

### Resultado

| Métrica        | Valor |
| -------------- | ----- |
| Acurácia Teste | 85.2% |

---

## 🔍 Importância das Variáveis

Foi utilizada a técnica de **Permutation Importance** para avaliar a influência de cada atributo.

### Variáveis Mais Relevantes

* `n_versions`
* `lines_added`

Essas métricas apresentaram maior impacto na redução da acurácia quando perturbadas, indicando forte relação com a ocorrência de bugs.

---

## 📊 Comparação dos Modelos

| Modelo        | Acurácia |
| ------------- | -------- |
| Decision Tree | 86.8%    |
| Random Forest | 85.2%    |

### Resultado Final

A Árvore de Decisão apresentou desempenho ligeiramente superior ao Random Forest neste conjunto de dados.

Embora Random Forest seja geralmente mais robusto, a simplicidade da Árvore de Decisão mostrou-se suficiente para capturar os padrões presentes no dataset.

---

## 🚀 Como Executar

### Instalar Dependências

```bash
pip install pandas numpy matplotlib scikit-learn
```

### Executar o Projeto

```bash
python exercicio01_tbs5.py
```

---

## 📂 Estrutura do Projeto

```text
.
├── metrics.csv
├── exercicio01_tbs5.py
└── README.md
```

---

## 📚 Conceitos Aplicados

* Machine Learning
* Classificação Supervisionada
* Predição de Bugs
* Árvores de Decisão
* Random Forest
* Engenharia de Software Baseada em Dados
* Feature Importance
* Matriz de Confusão
* Avaliação de Modelos

---

## 📈 Principais Conclusões

* Arquivos com mais alterações tendem a apresentar maior probabilidade de defeitos.
* O número de versões e a quantidade de linhas adicionadas foram os atributos mais importantes.
* A Árvore de Decisão alcançou a melhor acurácia no conjunto avaliado.
* O desbalanceamento das classes influencia a capacidade de detecção de bugs.

---

## 👨‍💻 Autor

Tamyres Silva
