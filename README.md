Projeto de Precificação de Seguros
Este projeto foca na análise exploratória de dados e no desenvolvimento de modelos de Machine Learning para prever os custos de seguro de saúde (charges) com base em diversas características dos indivíduos.

Sumário do Projeto
O objetivo principal deste projeto é construir um modelo preditivo robusto para estimar os custos individuais de seguro de saúde, utilizando um dataset que contém informações demográficas, de saúde e hábitos dos segurados. Exploramos diferentes algoritmos de regressão e avaliamos seu desempenho para identificar o modelo mais adequado.

Análise Exploratória de Dados (EDA) e Pré-processamento
A etapa inicial envolveu uma análise detalhada do dataset Precificacao_Seguros.csv, cobrindo:

Verificação de Valores Ausentes: Confirmamos a ausência de valores nulos, garantindo a completude dos dados.
Tipos de Dados: Observamos os tipos de dados para cada variável, identificando categóricas e numéricas.
Estatísticas Descritivas: Geramos estatísticas para entender a distribuição e a centralidade das variáveis numéricas.
Visualização: Boxplots e scatter plots foram utilizados para identificar outliers (notavelmente em bmi e charges) e relações entre variáveis. A variável smoker (fumante) mostrou ser o fator mais determinante para charges.
Codificação de Variáveis Categóricas:
smoker: Codificada para smoker_encoded (0 para não fumante, 1 para fumante).
sex: Codificada para sex_encoded (0 para feminino, 1 para masculino).
region: Convertida usando One-Hot Encoding em region_northwest, region_southeast, region_southwest.
Análise de Correlação: Uma forte correlação positiva (0.7873) foi encontrada entre smoker_encoded e charges.
Teste de Hipótese: Um teste t de Welch confirmou uma diferença estatisticamente significativa nas médias de charges entre fumantes e não fumantes (p-value extremamente baixo).
Modelagem Preditiva
Foram testados três modelos de regressão:

Regressão Linear:

Modelo Inicial: age, bmi, smoker_encoded. R² de 0.7777.
Modelo Expandido: age, bmi, children, smoker_encoded, sex_encoded. R² de 0.7811 (impacto mínimo de sex e children).
Modelo Final: age, bmi, children, smoker_encoded, region (one-hot encoded). R² de 0.7836. Este foi o melhor modelo de regressão linear.
Decision Tree Regressor: Treinado com as mesmas features do modelo final de Regressão Linear.

MSE: 39876049.53
R²: 0.7431
Conclusão: Desempenho inferior ao da Regressão Linear.
Random Forest Regressor: Treinado com as mesmas features do modelo final de Regressão Linear.

MSE: 20255300.47
R²: 0.8695
MAE: 2473.87
RMSE: 4500.59
Conclusão: Desempenho significativamente superior a ambos os modelos anteriores, tornando-o o algoritmo escolhido como o modelo final.
Importância das Features no Random Forest
O modelo Random Forest confirmou que as variáveis mais importantes para prever os custos de seguro são:

smoker_encoded: De longe a feature mais influente (importância de ~0.61).
bmi: Segunda feature mais importante (importância de ~0.22).
age: Terceira feature mais importante (importância de ~0.13).
children e as variáveis de region mostraram impacto muito menor.
Visualização do Desempenho
Um gráfico de dispersão dos valores reais vs. previstos pelo Random Forest mostrou que a maioria dos pontos se alinha bem com a linha de previsão perfeita, indicando um alto grau de acurácia do modelo.

Modelo Salvo
O modelo RandomForestRegressor treinado foi salvo como random_forest_regressor_model.joblib para uso futuro. Isso permite carregar o modelo e fazer novas previsões sem a necessidade de retreinamento.

Como Utilizar o Modelo Salvo
Para carregar o modelo e fazer previsões em novos dados:

import joblib
import pandas as pd

# Carregar o modelo salvo
model_filename = 'random_forest_regressor_model.joblib'
loaded_rf_model = joblib.load(model_filename)

print(f"Modelo '{model_filename}' carregado com sucesso!")

# Preparar novos dados para previsão
# **IMPORTANTE:** As colunas e a codificação devem ser exatamente as mesmas do treinamento.
# Features: 'age', 'bmi', 'children', 'smoker_encoded', 'region_northwest', 'region_southeast', 'region_southwest'

new_individual_data = pd.DataFrame({
    'age': [35], # Exemplo: 35 anos
    'bmi': [28.5], # Exemplo: BMI de 28.5
    'children': [2], # Exemplo: 2 filhos
    'smoker_encoded': [1], # Exemplo: É fumante (1)
    'region_northwest': [0],
    'region_southeast': [0],
    'region_southwest': [1] # Exemplo: Região sudoeste (1)
})

# Realizar a previsão
predicted_charge = loaded_rf_model.predict(new_individual_data)

print(f"Custo de seguro previsto para o novo indivíduo: ${predicted_charge[0]:.2f}")
