# Modelo de classificação para Credit Scoring para estudo de inadimplência 

#### Aluno: [Maria Rita de Sousa](https://github.com/link_do_github](https://github.com/Marri-Sousa))
#### Orientadora:  [Professora Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".


- [Link para o código](https://github.com/link_do_repositorio).

- Trabalhos relacionados:
    - [Machine Learning approach for Credit Scoring](https://link_do_trabalho.com](https://arxiv.org/abs/2008.01687)).

---

### Resumo

O estudo utilizou a base sintética Financial Risk for Loan Approval, com 20.000 registros contendo informações demográficas, de renda, histórico de crédito, dívidas e indicadores financeiros, permitindo tanto a previsão de risco quanto a classificação de aprovação de empréstimos. O dataset foi segmentado em DEV e OOT por safra. A EDA incluiu estatísticas descritivas, análise de dados faltantes, distribuições, outliers e correlações, seguida de seleção de variáveis via IV, PSI e correlação de Pearson, garantindo estabilidade temporal e redução de colinearidade. As variáveis finais foram tratadas com OneHotEncoder (categorias) e padronização (numéricas), e testaram‑se três modelos: Regressão Logística, LightGBM e XGBoost, todos avaliados pelas métricas AUC e KS. A interpretação foi feita por SHAP, evidenciando MonthlyIncome como principal variável de aprovação, além de variáveis como CreditScore, PaymentHistory e JobTenure. Entre os modelos, o LightGBM apresentou alta AUC e maior estabilidade de KS entre DEV, Validação e OOT, sendo escolhido como modelo final por combinar boa capacidade discriminante, robustez temporal e alinhamento com os fatores de risco identificados pelo SHAP.

### 1. Introdução

Neste trabalho é desenvolvido um modelo de credit scoring para avaliação de risco de aprovação de empréstimos. O objetivo é construir e comparar modelos de classificação capazes de estimar a probabilidade de aprovação de crédito, utilizando práticas usuais de modelagem de crédito. Para isso, o conjunto de dados é segmentado em base de desenvolvimento (DEV) e out-of-time (OOT), garantindo a avaliação de performance em safras mais recentes. A etapa de análise exploratória inclui estatísticas descritivas, identificação de dados faltantes, análise de distribuições, outliers e correlação, seguida da seleção de variáveis com base em IV, PSI e correlação de Pearson. Em seguida, são aplicadas transformações apropriadas e padronização de variáveis numéricas. 

Por fim, modelos como Regressão Logística, LightGBM e XGBoost foram treinados e comparados nas bases DEV, Validação e OOT por meio das métricas AUC e KS, além de técnicas de explicabilidade como SHAP, para apoiar a escolha do modelo final e sua interpretação em um contexto de concessão de crédito.

### 2. Modelagem

Para as etapas de modelagem inicialmente, o dataset foi dividido em bases de desenvolvimento (treino/validação) e out-of-time (OOT). Em seguida, realizou-se a EDA para entender distribuições, outliers e correlações, identificando variáveis numéricas e categóricas relevantes. Depois, foram aplicadas técnicas de seleção de variáveis, combinando IV, PSI e correlação de Pearson para manter apenas atributos com boa classificação e estabilidade temporal. As variáveis categóricas foram tratadas com codificação One-Hot, enquanto as numéricas foram padronizadas via StandardScaler. Após os tratamentos foram testados diferentes modelos de classificação (Regressão Logística, LightGBM e XGBoost) que foram treinados e comparados através das métricas AUC e KS nas bases de Treino, Validação e OOT.

<img width="1394" height="273" alt="image" src="https://github.com/user-attachments/assets/0d89eec5-d399-4854-ba12-3fb96d566860" />

### 3. Resultados

Após a comparação entre os três modelos (Regressão Logística, LightGBM e XGBoost), foi possível observar que todos apresentam um alto nível de discriminação, com AUC acima de 0,83 e KS acima de 0,50 nas bases de validação e OOT, indicando uma boa capacidade de separação de bons/maus ao longo do tempo.

<img width="1790" height="396" alt="image" src="https://github.com/user-attachments/assets/714a81a3-d6d2-402a-aa8c-48df13af0a36" />


    
|       Modelo        |      Base     |      AUC      |       KS      |
| ------------------- | ------------- | ------------- | ------------- |
| Regressão Logística | Treino        | 0.9214        | 0.6869        |
| Regressão Logística | Validação     | 0.8491        | 0.5334        |
| Regressão Logística | OOT           | 0.9017        | 0.6402        |
| ------------------- | ------------- | ------------- | ------------- |
| LightGBM            | Treino        | 1.0000        | 1.0000        |
| LightGBM            | Validação     | 0.8405        | 0.5464        |
| LightGBM            | OOT           | 0.8917        | 0.6192        |
| ------------------- | ------------- | ------------- | ------------- |
| XGBoost             | Treino        | 1.0000        | 1.0000        |
| XGBoost             | Validação     | 0.8344        | 0.5090        |
| XGBoost             | OOT           | 0.8910        | 0.6191        |
    


Apesar do modelo de regressão apresentar patamares maiores de KS no treino e OOT, o modelo de LightGBM apresentou excelente desempenho em termos de AUC e demonstrou maior estabilidade de KS entre as bases de validação e out-of-time, indicando boa capacidade de generalização ao longo do tempo.

### 4. Conclusões

Para o modelo testado podemos observar que a variavel MonthlyIncome aparece com alto SHAP, sendo assim a renda mensal a variavel que mais impacta na probabilidade de aprovação. As demais variaveis como CreditScore, PaymentHistory e JobTenure também contribuem fortemente, mostrando que o modelo está capturando bem o risco de inadimplência. Com base nas análises realizadas e nos resultados obtidos, o modelo selecionado foi o LightGBM, além de apresentar excelente desempenho em termos de AUC, o modelo demonstrou maior estabilidade de KS entre as bases de validação e out-of-time, indicando boa capacidade de generalização ao longo do tempo.

<img width="500" height="600" alt="image" src="https://github.com/user-attachments/assets/893beac5-33ff-4eba-9e3c-91feb1a50dc0" />

A escolha do LightGBM como modelo final foi a combinação de capacidade preditiva, estabilidade e aderência ao problema de crédito, mesmo com o overfitting observado no treino e do bom desempenho da Regressão Logística em algumas bases. O modelo LGBM por sua própria definição consegue explorar de forma mais abrangente, oscilações e combinações entre variáveis que impactam de forma diferenciada a probabilidade de aprovação. Os resultados nas bases de Validação e OOT mostram que, mesmo com sinais de overfitting na base de Treino, o modelo mantém AUC e KS elevados e consistentes ao longo do tempo não perdendo performance fora da amostra, demonstrando sua boa capacidade de generalização e robustez temporal. 

Como possibilidade para estudos futuros, aprofundar a calibragem do modelo escolhido e testar novas abordagens, além de avaliar o desempenho em bases reais de diferentes carteiras e períodos econômicos, incorporando também métricas para garantir que o modelo não seja apenas preditivo, mas também aderente a requisitos regulatórios de crédito.

---

Matrícula: 232.100.482

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
