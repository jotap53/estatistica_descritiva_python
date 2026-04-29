# O Pipeline Completo de um Projeto de Dados

```
1. Definição do Problema
        ↓
2. Coleta de Dados
        ↓
3. EDA
        ↓
4. Pré-processamento e Feature Engineering
        ↓
5. Modelagem
        ↓
6. Avaliação
        ↓
7. Deploy
        ↓
8. Monitoramento
```

---

### 1. Definição do Problema

É o ponto de partida de qualquer projeto. Sem isso bem definido, todo o resto pode ser trabalho inútil.

* **Entender o objetivo de negócio** — o que a empresa ou cliente quer resolver ou melhorar?
* **Traduzir para um problema de dados** — classificação, regressão, clustering, otimização?
* **Definir métrica de sucesso** — como saberemos se o modelo funcionou? (reduzir churn em X%, prever com erro máximo de Y)
* **Definir viabilidade** — temos dados suficientes? O problema é tecnicamente solucionável?
* **Alinhar expectativas** — prazo, recursos, limitações técnicas e éticas

Serve para: evitar construir a solução certa para o problema errado.

---

### 2. Coleta de Dados

Com o problema definido, você vai atrás dos dados necessários para resolvê-lo.

* **Identificar fontes** — bancos de dados internos, APIs externas, web scraping, sensores, formulários, dados públicos
* **Extração** — queries SQL, chamadas de API, leitura de arquivos (CSV, JSON, Parquet, Excel)
* **Integração** — combinar dados de múltiplas fontes em um único dataset
* **Armazenamento** — definir onde os dados ficam (data lake, data warehouse, arquivos locais)
* **Legalidade e privacidade** — os dados podem ser usados? LGPD/GDPR se aplicam?
* **Volume e representatividade** — os dados cobrem bem o problema? Há viés de coleta?

Serve para: garantir que você tem a matéria-prima certa antes de qualquer análise.

---

### 3. EDA (Análise Exploratória de Dados)

A etapa em que você "conversa" com os dados antes de modelar qualquer coisa.

```
EDA
├── 1. Entendimento inicial
├── 2. Qualidade dos dados
├── 3. Tendência central
├── 4. Dispersão
├── 5. Distribuição e forma
├── 6. Outliers
├── 7. Univariada (categóricas)
├── 8. Bivariada (num×num, num×cat, cat×cat)
├── 9. Multivariada (PCA, clusters, correlação)
├── 10. Temporal (se aplicável)
├── 11. Texto (se aplicável)
└── 12. Síntese e hipóteses
```

Serve para: entender distribuições, qualidade, relações e padrões dos dados antes de qualquer modelagem.

---

### 4. Pré-processamento e Feature Engineering

É aqui que você age sobre tudo que a EDA revelou. É a etapa mais trabalhosa e que mais impacta o resultado final.

* **Tratamento de missings** — imputar pela mediana, média, moda, por modelo (KNN imputer), ou remover
* **Tratamento de outliers** — remover, capping (winsorização), transformar
* **Transformações** — log, raiz quadrada, Box-Cox para normalizar distribuições assimétricas
* **Encoding de categóricas** — Label Encoding, One-Hot, Target Encoding, Embeddings
* **Escalonamento** — StandardScaler, MinMaxScaler, RobustScaler (importante para modelos sensíveis a escala)
* **Feature Engineering** — criar novas variáveis a partir das existentes (ex: idade a partir da data de nascimento, razão entre duas colunas, lag de uma série temporal)
* **Feature Selection** — eliminar variáveis redundantes, com baixa variância ou que causam multicolinearidade (usando VIF, correlação, importância de features)
* **Divisão dos dados** — separar treino, validação e teste antes de qualquer modelagem (e nunca vazar informação do teste para o treino)

---

### 5. Modelagem

Com os dados limpos e preparados, você escolhe e treina algoritmos.

* **Escolha do algoritmo** — baseada no tipo de problema (classificação, regressão, clustering, séries temporais) e nas características dos dados que a EDA revelou
* **Baseline** — sempre comece com um modelo simples (regressão linear, árvore rasa, média histórica) para ter um ponto de comparação
* **Treinamento** — ajustar o modelo nos dados de treino
* **Tunagem de hiperparâmetros** — Grid Search, Random Search, Optuna/Bayesian Optimization
* **Validação cruzada (Cross-validation)** — garante que o desempenho é robusto e não dependente de um split específico

---

### 6. Avaliação

Medir se o modelo realmente resolve o problema de negócio, não apenas se tem boa métrica.

* **Métricas técnicas** — Acurácia, F1, AUC-ROC, RMSE, MAE, R², dependendo do problema
* **Análise de erros** — onde o modelo erra mais? Há padrão nos erros? (análise de resíduos)
* **Interpretabilidade** — SHAP values, LIME, importância de features para entender o "porquê" das previsões
* **Teste de sanidade** — o modelo faz sentido de negócio? Uma feature com peso altíssimo faz sentido real?
* **Comparação de modelos** — qual performa melhor no conjunto de teste (nunca visto antes)?

---

### 7. Deploy (Implantação)

Colocar o modelo em produção para gerar valor real.

* **Serialização do modelo** — salvar o modelo treinado (pickle, joblib, ONNX, etc.)
* **API de inferência** — criar um endpoint (FastAPI, Flask) que recebe dados e retorna previsões
* **Containerização** — Docker para garantir que o ambiente de produção replica o de desenvolvimento
* **Integração com sistemas** — conectar a API ao produto, dashboard ou pipeline de dados da empresa
* **Testes de carga** — o modelo aguenta o volume de requisições esperado?

---

### 8. Monitoramento

O trabalho não termina no deploy. Modelos degradam com o tempo.

* **Data drift** — a distribuição dos dados de entrada mudou em relação ao que o modelo foi treinado?
* **Concept drift** — a relação entre features e target mudou? (ex: comportamento de consumidor pós-pandemia)
* **Performance monitoring** — acompanhar as métricas do modelo em produção ao longo do tempo
* **Retreinamento** — definir quando e como retreinar (agendado, por gatilho de queda de performance)
* **Versionamento** — controle de versão de dados e modelos (MLflow, DVC, Weights & Biases)

---

### Lembrando: o pipeline não é linear

```
EDA → Pré-processamento → Modelagem
         ↑                      |
         |______________________|
         (modelo ruim revela necessidade
          de nova feature ou tratamento)
```
