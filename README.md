# 🏥 Precificação de Seguros de Saúde com Machine Learning

## 📌 Visão Geral

Este projeto tem como objetivo desenvolver modelos de Machine Learning capazes de prever os custos médicos individuais cobrados por planos de saúde, utilizando características demográficas e comportamentais dos segurados.

A precificação adequada é um dos principais desafios das seguradoras, pois impacta diretamente a rentabilidade do negócio, a competitividade dos produtos oferecidos e a sustentabilidade financeira da carteira de clientes.

Por meio de análises estatísticas, exploração dos dados e algoritmos de Machine Learning, buscamos identificar os principais fatores que influenciam o valor dos custos médicos e construir um modelo preditivo capaz de estimar esses valores com precisão.

---

# 🎯 Problema de Negócio

Seguradoras precisam definir preços compatíveis com o risco apresentado por cada segurado.

Uma precificação inadequada pode gerar:

* Subprecificação: prejuízos financeiros devido à cobrança insuficiente.
* Superprecificação: perda de clientes para concorrentes.
* Dificuldade na gestão de riscos.
* Problemas de sustentabilidade da carteira de seguros.

O objetivo deste projeto é responder à seguinte pergunta:

> É possível prever os custos médicos individuais de um segurado utilizando características pessoais e comportamentais?

---

# 📊 Base de Dados

A base utilizada contém informações demográficas, geográficas e comportamentais dos segurados.

## Dicionário de Dados

| Variável | Descrição                                                   |
| -------- | ----------------------------------------------------------- |
| age      | Idade do beneficiário principal                             |
| sex      | Sexo do segurado                                            |
| bmi      | Índice de Massa Corporal (IMC)                              |
| children | Quantidade de dependentes cobertos pelo seguro              |
| smoker   | Indica se o beneficiário é fumante                          |
| region   | Região de residência nos Estados Unidos                     |
| charges  | Custos médicos cobrados pelo plano de saúde (variável alvo) |

---

# 🔎 Entendimento do Negócio

Do ponto de vista atuarial e financeiro, algumas hipóteses podem explicar o aumento dos custos médicos:

* Pessoas mais velhas tendem a utilizar mais serviços médicos.
* Fumantes costumam apresentar maior risco de doenças crônicas.
* IMC elevado pode estar associado a problemas de saúde.
* Famílias maiores podem gerar maior utilização do plano.
* Diferenças regionais podem refletir custos distintos de atendimento.

Essas hipóteses foram investigadas ao longo da análise exploratória.

---

# 🛠️ Tecnologias Utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-Learn
* Joblib
* Jupyter Notebook

---

# 📈 Análise Exploratória dos Dados (EDA)

A etapa de Análise Exploratória teve como objetivo compreender o comportamento das variáveis e identificar padrões relevantes para o negócio.


## Etapas realizadas

### 1. Verificação da Qualidade dos Dados

* Identificação de valores ausentes.
* Validação dos tipos de dados.
* Verificação da consistência das variáveis.

### 2. Estatísticas Descritivas

Foram calculadas medidas como:

* Média
* Mediana
* Desvio padrão
* Valores mínimos e máximos
* Quartis

para todas as variáveis numéricas.

### 3. Análise das Variáveis Categóricas

Avaliação da distribuição das categorias:

* Sexo
* Fumante
* Região

---

## 📦 Distribuição das Variáveis

Foram construídos boxplots para:

* Age
* BMI
* Children
* Charges

Objetivos:

* Detectar possíveis outliers.
* Avaliar dispersão dos dados.
* Compreender a distribuição das variáveis.

## Box Plot 

![Heatmap](images/Box_plot_1.png)
---

## 🔥 Impacto do Tabagismo

Uma das análises mais relevantes foi a comparação dos custos médicos entre fumantes e não fumantes.

Os resultados evidenciaram que:

* Fumantes apresentam custos significativamente superiores.
* A variável "smoker" demonstrou forte capacidade explicativa sobre os custos médicos.

Essa conclusão foi posteriormente confirmada pelos modelos preditivos.

---

## 🔗 Análise de Correlação

Foram realizadas:

### Correlação de Pearson

Avaliando a relação entre:

* Age × Charges
* BMI × Charges
* Smoker × Charges
* Children × Charges

### Heatmap de Correlação

Foi construída uma matriz de correlação para identificar relações lineares entre todas as variáveis numéricas.

## Matriz de Correlação

![Heatmap](images/Matriz_Corr.png)
---

# 🧪 Teste de Hipótese

Foi realizado um teste estatístico para verificar se existe diferença significativa entre os custos médicos de:

* Fumantes
* Não fumantes

Resultado:

* A hipótese nula foi rejeitada.
* Existe evidência estatística de que fumantes possuem custos médicos significativamente maiores.

Esse resultado reforça a importância do comportamento do segurado na precificação dos seguros.

---

# 🤖 Engenharia de Features

Para preparar os dados para os algoritmos de Machine Learning foram realizadas transformações como:

### Variáveis Binárias

* smoker → smoker_encoded
* sex → sex_encoded

### One-Hot Encoding

Aplicado na variável:

* region

Gerando novas variáveis indicadoras para cada região.

---

# 🚀 Modelos de Machine Learning Testados

Foram avaliados diferentes algoritmos de regressão para estimar os custos médicos.

## 1. Regressão Linear

Modelo base utilizado para entender o comportamento das variáveis.

### Variáveis utilizadas inicialmente

* age
* bmi
* smoker

Posteriormente foram adicionadas:

* children
* sex
* region

### Resultado Final

| Métrica | Valor      |
| ------- | ---------- |
| R²      | 0.7836     |
| MSE     | 33.602.504 |

---

## 2. Decision Tree Regressor

Modelo não linear capaz de capturar relações mais complexas entre as variáveis.

### Resultado

| Métrica | Valor      |
| ------- | ---------- |
| R²      | 0.7431     |
| MSE     | 39.876.049 |

---

## 3. Random Forest Regressor

Modelo baseado em múltiplas árvores de decisão, reduzindo overfitting e aumentando a capacidade preditiva.

### Resultado

| Métrica | Valor      |
| ------- | ---------- |
| R²      | 0.8695     |
| MSE     | 20.255.300 |
| MAE     | 2.473,87   |
| RMSE    | 4.500,59   |

## Gráfico de Dispersão  

![Heatmap](images/Random_Forest_pred_real.png)

---

# 🏆 Comparação dos Modelos

| Modelo           | R²         | MSE            |
| ---------------- | ---------- | -------------- |
| Regressão Linear | 0.7836     | 33.602.504     |
| Decision Tree    | 0.7431     | 39.876.049     |
| Random Forest    | **0.8695** | **20.255.300** |

O Random Forest apresentou o melhor desempenho entre os modelos avaliados.

---

# 📌 Importância das Variáveis

A análise de importância das features mostrou que algumas variáveis possuem maior influência na previsão dos custos médicos.

Os principais fatores explicativos observados foram:

1. Tabagismo (smoker)
2. Idade (age)
3. Índice de Massa Corporal (BMI)
4. Número de dependentes
5. Região de residência

Do ponto de vista do negócio, esse resultado é coerente com fatores tradicionalmente utilizados em análises de risco e precificação.

---

# 💾 Persistência do Modelo

O modelo final foi salvo utilizando a biblioteca Joblib, permitindo:

* Reutilização em produção.
* Integração com APIs.
* Implementação em aplicações web.
* Criação de simuladores de cotação.

---

# 📊 Conclusões

Os resultados demonstram que é possível prever custos médicos com boa precisão utilizando características demográficas e comportamentais dos segurados.

Principais aprendizados:

* O tabagismo é o principal fator associado ao aumento dos custos médicos.
* Idade e IMC possuem forte influência sobre os gastos.
* Modelos não lineares capturam melhor os padrões dos dados.
* O Random Forest apresentou desempenho superior aos demais algoritmos avaliados.

Com um R² de aproximadamente 87%, o modelo foi capaz de explicar grande parte da variabilidade dos custos médicos observados.

---

# 🚀 Próximos Passos

Para evoluir este projeto para um cenário mais próximo da realidade de mercado, algumas melhorias podem ser implementadas:

### Modelagem

* XGBoost
* LightGBM
* CatBoost
* Gradient Boosting

### Engenharia de Features

* Faixas etárias
* Categorias de IMC
* Interações entre variáveis
* Variáveis de risco compostas

### Avaliação

* Cross Validation
* Grid Search
* Random Search
* Feature Selection

### Deploy

* API com FastAPI
* Dashboard com Streamlit
* Containerização com Docker
* Deploy em Cloud (AWS, Azure ou GCP)

---

# 📚 Aprendizados

Este projeto permitiu aplicar conceitos fundamentais e avançados de Ciência de Dados:

* Estatística Descritiva
* Testes de Hipótese
* Análise Exploratória de Dados
* Engenharia de Features
* Machine Learning Supervisionado
* Avaliação de Modelos
* Interpretabilidade
* Persistência de Modelos

---

# 👨‍💻 Autor

**Everson Cardozo Machado**

Cientista de Dados com experiência em Analytics, Machine Learning, People Analytics, Business Intelligence e desenvolvimento de soluções orientadas a dados.


