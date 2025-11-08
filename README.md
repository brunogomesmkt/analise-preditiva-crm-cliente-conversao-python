
## 🚀  Projeto de Data Science: Previsão de Conversão de Marketing (Lead Scoring)
Este é um projeto completo de Ciência de Dados focado em prever a conversão de clientes (Lead Scoring) com base em dados de uma campanha de marketing de um banco.

O objetivo principal é construir um modelo de Machine Learning que possa identificar quais clientes têm a maior probabilidade de converter (subscrever um produto) após serem contactados pela equipa de marketing. Prever se um cliente do CRM, contactado por uma campanha de marketing, irá converter (ou seja, comprar um produto ou subscrever um serviço).


## 🎯 O Problema de Negócio
Uma equipa de marketing tem um orçamento e tempo limitados. Contactar todos os clientes da base de dados é caro e ineficiente. A maioria dos clientes contactados não irá converter, resultando em desperdício de recursos.

O pior erro, no entanto, é um Falso Negativo: um cliente que o modelo previu como "Não" (não converte), mas que na realidade iria converter. Esta é uma venda perdida.

O objetivo deste projeto é criar um modelo que minimize os Falsos Negativos, aumentando o Recall (a capacidade de "apanhar" todos os clientes que realmente iriam converter), para que a equipa de marketing possa focar os seus esforços nos leads mais promissores.


## 📊 O Dataset
Utilizámos o Bank Marketing Dataset (Bank Additional Full), um conjunto de dados público e popular para problemas de classificação.

Este dataset contém 41.188 registos de clientes e 20 colunas, incluindo:

Dados Demográficos: age, job, marital, education.

Dados da Campanha: contact, month, day_of_week, duration (duração da chamada).

Histórico: pdays, previous, poutcome.

Variáveis Económicas: emp.var.rate, cons.price.idx.

Variável Alvo: y - O cliente subscreveu o depósito a prazo? ('yes' ou 'no').


##  🛠️ Ferramentas Utilizadas
Python (3.x)

Jupyter Notebook: Para exploração e prototipagem interativa.

Pandas: Para manipulação e carregamento dos dados.

Scikit-learn (sklearn): Para todo o fluxo de Machine Learning.


##  📈 Metodologia (O Processo)
O projeto seguiu os passos clássicos de um fluxo de trabalho de Machine Learning:

Carregamento e Exploração: Os dados foram carregados e analisados. Verificámos que o dataset estava limpo (sem valores nulos) e que o nosso alvo (y) era altamente desbalanceado (~89% 'no' vs. ~11% 'yes').

Pré-processamento:

Features Categóricas: Aplicámos OneHotEncoder para transformar colunas de texto (como job ou marital) em colunas numéricas (0s e 1s).

Features Numéricas: Aplicámos StandardScaler para normalizar as colunas numéricas (como age), colocando-as na mesma escala.

Pipeline: Todo o pré-processamento foi encapsulado num ColumnTransformer e, por sua vez, numa Pipeline do Scikit-learn para evitar data leakage (fuga de dados) e otimizar o fluxo.

Modelo 1 (Baseline): Regressão Logística

Criámos um primeiro modelo simples usando LogisticRegression.

Resultado: A acurácia foi alta (~91%), mas a Matriz de Confusão revelou o problema: o modelo tinha um número muito elevado de Falsos Negativos. Ele estava "viciado" em dizer 'Não' devido ao desbalanceamento dos dados.

Modelo 2 (Otimizado): Random Forest com Balanceamento

Para resolver o problema dos Falsos Negativos, trocámos o algoritmo para um RandomForestClassifier, que é mais poderoso.

A "Magia": Usámos o parâmetro class_weight='balanced'. Isto força o modelo a dar um "peso" (penalização) muito maior ao erro de classificar um 'yes' como 'no'.

Resultado: O modelo final sacrificou um pouco da precisão (Precision) para ganhar um aumento drástico no Recall (capacidade de encontrar os 'yes').


##  💡 Principais Insights e Conclusões
A Acurácia pode enganar: O nosso primeiro modelo tinha 91% de acurácia, mas era péssimo para o negócio. O segundo modelo, focado no Recall, é muito mais valioso, pois encontra de facto as oportunidades de venda.

O Problema dos Falsos Negativos: Este projeto demonstrou como a Matriz de Confusão é vital. Focar na redução de Falsos Negativos (oportunidades perdidas) foi a chave para o sucesso.

Valor para o Negócio: Este modelo final pode agora ser usado para criar um score (pontuação) para cada novo cliente. A equipa de marketing pode filtrar a base de dados e focar os seus esforços apenas nos clientes com uma probabilidade de conversão acima de X%, otimizando drasticamente o ROI (Retorno sobre o Investimento) das campanhas.


##  🚀 Próximos Passos
Feature Importance: Analisar quais variáveis (duration, age, poutcome?) são as mais importantes para a previsão do modelo RandomForest.

Hyperparameter Tuning: Usar GridSearchCV ou RandomizedSearchCV para encontrar os melhores parâmetros para o RandomForest e otimizar ainda mais o Recall.

Outros Modelos: Testar algoritmos de Gradient Boosting (como XGBoost ou LightGBM), que são frequentemente os vencedores em competições de dados tabulares.
