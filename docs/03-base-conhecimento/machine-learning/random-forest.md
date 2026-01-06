# 🌳 Random Forest

> **Status:** 🟨 Em revisão     
> **Tags:** #Supervisionado #Classificacao #Regressao #Ensemble


---


## 📝 O que é o modelo?

O **Random Forest** é um algoritmo de aprendizado **supervisionado** que utiliza a técnica de **Ensemble Learning**, ou aprendizado por conjunto. Em vez de confiar em apenas uma [Árvore de Decisão](arvore-decisao.md), o modelo cria uma "floresta", com várias árvores independentes, e assim combina os resultados individuais para obter uma previsão mais robusta e precisa, que seria melhor que apenas uma única árvore.

![Random Tree](https://www.researchgate.net/publication/354354484/figure/fig4/AS:1080214163595269@1634554534720/Illustration-of-random-forest-trees.jpg)


## 💡 Como funciona?

> Para avaliar um filme, é necessário coletar a opinião de diferentes críticos de cinema. Cada crítico tem uma percepção diferente sobre o filme, por ser profissional como cineasta, diretor, ator, ou ser um cinéfilo e grande fã de cinema por ter assistindo muitos filmes! Desse modo, com uma regressão sobre a nota média, ou a classificação sobre opinião da maioria, se o filme é bom, médio ou ruim. A decisão do grupo tende a ser muito mais assertiva que a de um indivíduo isolado, isso é conhecido como sabedoria da multidão!


### Lógica do modelo
O modelo consiste em base na aleatoriedade, obtida do seguinte modo:

1. **Bagging**: É a abreviação de *bootstrap aggregating*, parte do conjunto principal dos metodos de *Ensemble Learning*, que consiste em cada árvore da floresta é treinada com uma amostragem aleatória dos dados originais com reposição. Para garantir que uma árvore tenha acesso aos mesmos dados que as outras;

2. **Feature Randomness:** Ao decidir como dividir um nó, o algoritmo escolhe um subconjunto aleatório de colunas, as *features*. Para evitar que uma variável dominante crie um padrão de árvores semelhantes;

3. **Agregação:** Para o método de *classificação*, ocorre o processo de votação majoritária, ou seja, a classe mais votada vence. No método de *regressão*, é calculado a média aritmética dos resultados de todas as árvores;

### Classificação

Como mencionado no início, os modelos de *random tree* podem ser utilizados tanto para **classificação** como também para **regressão**. Nos modelos de classificaão a intenção é agrupar dados em classes diferentes ou conjuntos predefinidos.

### Regressão

Nos modelos de *random tree* para regressão, o objetivo é prever valores contínuos, ou seja, preços, temperatura, quantidade, etc., que podem variar dado um intervalo. 


## ⚙ Principais Hiperparâmetros

Os hiperparâmetros são configurações de um modelo que podem alterar seu desempenho e eficácia. Diferente dos parâmetros do modelo, que são ajustados automaticamente durante o treinamento, os hiperparâmetros devem ser definidos antes do processo de aprendizado.

Hiperparâmetros mal ajustados podem levar a problemas como overfitting, onde o modelo se ajusta excessivamente aos dados de treinamento, ou underfitting, onde o modelo não consegue capturar a complexidade dos dados.

Como o *Random Forest* é um conjunto de árvores, são hiperparâmetros semelhantes ao da Árvore de Decisão, adicionando controles específicos sobre a floresta inteira, com '*' ao lado dos hiperparâmetros de árvore de decisão:

| Hiperparâmetro | Função | Impacto |
| :--- | :--- | :--- |
| `n_stimators` | Número de árvores utilizadas na floresta. | Melhora a estabilidade, mas aumenta o tempo de processamento.
| `max_features` | Quantidade de colunas que serão sorteadas para cada divisão. | Aumenta a diversidade entre as árvores, reduzindo o overfitting.
| `bootstrap` | Se deve ou não usar amostras aleatórias com reposição. | `False`, cada árvore utilizará o dataset inteiro, não recomendado. |
| *`max_depth` | Profundidade máxima da árvore. | Mais complexidade, aumentando o risco de overfitting. |
| *`min_samples_split` | Mínimo de amostras para criar uma nova divisão. | Divisões mais específicas, maior risco de overfitting. |
| *`min_samples_leaf` | Mínimo de amostras que uma "folha" deve ter | Suaviza o modelo, evita folhas com apenas um dado. |
| *`criterion` | Função que mede a qualidade da divisão. | Opção de `gini`, para ser mais rápido, ou `entropy`, para ser mais rigoroso |
| *`random_state` | Gerador de número randômicos | Geralmente utilizado para garantir a replicabilidade dos experimêntos.
| `oob_score` | Utiliza dados que ficaram de fora do treino para validar o modelo. | Uma forma mais simples para testar a acurácia, sem a necessidade de configurar um set específico de validação.

## ⚠️ Atenção aos erros de principiante!
* **Quanto mais árvores, melhor!:** Após certo nível, o ganho de acurácia é reduzido, mas o custo computacional e o tamanho do arquivo do modelo continuam aumentando;

* **Perder interpretabilidade:** Quando se utiliza apenas uma árvore é simples entender a lógica dela, mas quando se utilizam 500 ou 1000 árvores é mais complicado desenhar a lógica de todas elas. Desse modo, é necessário utilizar outros métodos, como o `feature_importances_`;

* **Não tratar Outliers em Regressão:** Embora seja modelo robusto, o *Random Forest* não consegue prever valores fora do intervalo encontrado no treino, ele não extrapola tendências como uma regressão linear;

## 📈 Vantagens & Limitações

| ✅ Vantagens | ❌ Limitações |
|:--- | :--- |
| **Alta precisão:** Geralmente performa melhor que uma árvores simples e outros modelos lineares, dependendo do problema. | **Caixa-Preta:** Difícil de explicar visualmente o "porquê" de cada decisão individual, sendo necessário outros métodos para interpretabilidade. |
| **Robustez overfitting:** A média de várias árvores lida melhor com os erros de memorização individuais. | **Lentidão em Tempo Real:** Caso a floresta seja muito grande, ou seja, existam muitas árvores, a predição pode ficar lenta para aplicações onde tempo de processamento e latência sejam prioridade.|
| **Lida com dados faltantes:** Consegue manter boa performance mesmo com valores faltantes. | **Consumo de Memória:** O modelo salvo em disco pode ocupar espaço razoável dependendo do número de árvores. |


## 🧩 Quando usar?
* **Dados Complexos:** Quando a relação entre as variáveis não é linear e existem muitas interações entre elas;

* **Ranking de Importância:** Para descobrir quais variáveis são realmente cruciais para o seu problema de negócio, utilizando a *Feature Selection*;

### 📋 Aplicações

* **:** O algoritmo pode analisar transações, valores, localização, histórico do cliente, etc. e classificar as transações com "fradulentas" ou "não fraudulentas";

* **Detecção de Fraude:** O algoritmo pode analisar transações, valores, localização, histórico do cliente, etc. e classificar as transações com "fradulentas" ou "não fraudulentas";


## 🎮 Implementação Rápida (Python)
```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split

# Inicializando a floresta com 100 árvores
model = RandomForestClassifier(
    n_estimators=100, 
    max_depth=10, 
    random_state=42
)

# Treino e Predição
model.fit(X_train, y_train)
previsoes = model.predict(X_test)

# Analisando a importância das colunas
importances = model.feature_importances_
```


## 🔗 Referências e Links Adicionais
- [Documentação Oficial Scikit-Learn (Ensembles: Gradient boosting, random forests, bagging, voting, stacking)](https://scikit-learn.org/stable/modules/ensemble.html)