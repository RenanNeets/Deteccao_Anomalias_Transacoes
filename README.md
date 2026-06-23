# Detecção de Anomalias em Transações Financeiras

Este repositório contém um pipeline completo de Ciência de Dados voltado para a **Detecção de Anomalias (Fraudes/Inconsistências) em Transações**, utilizando técnicas avançadas para lidar com dados altamente desbalanceados e ferramentas de explicabilidade de modelos (*XAI*).

O projeto foi desenvolvido em um Jupyter Notebook (`DeteccaoAnomaliasTransacoes.ipynb`) utilizando o ecossistema Python.

---

## 📌 Visão Geral do Projeto

Em cenários reais de detecção de fraude, a classe de interesse (anomalia) geralmente representa uma fração minúscula do total de transações (geralmente menos de 1%). Este projeto simula essa dinâmica utilizando um dataset público e aborda o problema passo a passo: desde a falha de modelos tradicionais até a aplicação de algoritmos robustos com balanceamento sintético.

### O que é abordado no pipeline:

1. **Carregamento e Exploração de Dados:** Importação e análise inicial da base.
2. **Simulação de Anomalias e Feature Engineering:** Criação de um cenário artificial de anomalias (~5% da base) baseado em regras de negócio e geração de novas variáveis explicativas.
3. **Métricas em Dados Desbalanceados:** Demonstração prática de por que a *Acurácia* é uma métrica enganosa nesses cenários e como avaliar utilizando *Recall*, *Precision* e *F1-Score*.
4. **Balanceamento de Dados (SMOTE):** Aplicação da técnica *Synthetic Minority Over-sampling Technique* para equilibrar o conjunto de treino.
5. **Modelagem Avançada (XGBoost):** Treinamento de um classificador de ponta baseado em árvores (*Gradient Boosting*).
6. **Ajuste de Hiperparâmetros:** Otimização do modelo via `GridSearchCV` focando na maximização do *Recall*.
7. **Explicabilidade do Modelo (SHAP):** Uso de *Shapley Additive exPlanations* para entender o peso global das variáveis e interpretar decisões individuais.

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas

* **Python 3**
* **Pandas & NumPy:** Manipulação e processamento de dados.
* **Scikit-Learn:** Divisão de dados, Regressão Logística, Grid Search e métricas de avaliação.
* **Imbalanced-Learn (SMOTE):** Balanceamento de dados.
* **XGBoost:** Algoritmo de aprendizado de máquina de alto desempenho.
* **SHAP:** Interpretabilidade e explicabilidade do modelo (*Explainable AI*).
* **Matplotlib & Seaborn:** Visualização de dados e matrizes de confusão.

---


## 📊 Estrutura do Notebook

* **`1. Carregamento de Dados`**: Consome a base pública `tips` do Seaborn para servir de fundação estrutural para as transações.
* **`2. Engenharia de Features`**: Criação das colunas `pct_gorjeta` (percentual de gorjeta) e `gasto_por_pessoa`, além de aplicar *One-Hot Encoding* em variáveis categóricas.
* **`4. Regressão Logística (Baseline)`**: Treina um modelo simples sem tratamento de desbalanceamento para evidenciar o problema do *Recall* zerado.
* **`5. Aplicação do SMOTE`**: Reamostragem da classe minoritária e re-treinamento da Regressão Logística, mostrando o salto de performance na detecção.
* **`6. Otimização com XGBoost & SHAP`**: Implementação do modelo campeão, ajuste fino dos parâmetros e geração dos gráficos de importância global e dependência do SHAP.

---

## 📈 Principais Conclusões

* **A armadilha da acurácia:** O modelo inicial apresentou acurácia elevada, mas foi incapaz de detectar **nenhuma** anomalia (Recall = 0%).
* **SMOTE é indispensável:** A aplicação do SMOTE permitiu que o modelo finalmente aprendesse os padrões das anomalias, sacrificando uma quantidade mínima de precisão para salvar o Recall.
* **XGBoost + SHAP:** O modelo avançado não só entregou métricas superiores, mas através do SHAP tornou-se totalmente auditável, permitindo explicar exatamente o porquê de uma transação ter sido classificada como suspeita.

---
