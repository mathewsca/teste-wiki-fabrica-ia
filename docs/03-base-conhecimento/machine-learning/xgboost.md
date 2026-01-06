# 🚀 XGBoost (eXtreme Gradient Boosting)
> Status: 🟨 Em revisão     
> Tags: #Supervisionado #Classificacao #Regressao #Ensemble #Boosting

---

## 📝 O que é o modelo?

O **XGBoost** é uma implementação otimizada do algoritmo de **Gradient Boosting**, utilizado para **classificação** e **regressão**. Ele pertence à categoria de **Ensemble Learning**, mas ao contrário do [Random Forest](random-forest.md), onde as árvores são independentes, no XGBoost as árvores são construídas sequencialmente, utilizando uma abordagem aditiva. Cada nova árvore tenta corrigir os erros cometidos pelas árvores anteriores.

![XGBoost](https://assets.ibm.com/is/image/ibm/6-1_sequential-ensemble-learning_boosting:16x9?dpr=on%2C1&wid=1536&hei=864)
## 💡 Como funciona?

> Um professor passa um desafio de matemática de 100 questões para uma turma:  
    > O Primeiro aluno resolve a prova, acerta 60 questões e erra 40.  
    > O Segundo aluno não tenta resolver a prova inteira do zero. O professor entrega para ele apenas as 40 questões que o primeiro errou. Dessas 40, erra 10.  
    > O Terceiro aluno é chamado para focar exclusivamente nesses 10 erros restantes. Assim por diante...  

O funcionamento do **XGBoost** segue esse mesmo princípio, um aprendizado sequencial focado na correção de erros ou resíduos do anterior. O modelo aprende errando, corrigindo e se especializando progressivamente.

### Lógica do modelo

* **Gradiente:** Utiliza o cálculo de derivadas da função de perda para saber em qual direção deve ajustar os pesos para diminuir o erro;

* **Regularização:** O modelo possui penalidades embutidas, L1 e L2, o que o torna mais resistente ao overfitting do que o Gradient Boosting comum;

* **Sparsity Aware:** Com um algoritmo, aprende automaticamente como lidar com dados faltantes, decidindo qual o melhor caminho em cada nó;

![Boosting](https://www.dailydoseofds.com/content/images/size/w1000/2024/08/image-61.png)

## ⚙ Principais Hiperparâmetros

Os hiperparâmetros são configurações de um modelo que podem alterar seu desempenho e eficácia. Diferente dos parâmetros do modelo, que são ajustados automaticamente durante o treinamento, os hiperparâmetros devem ser definidos antes do processo de aprendizado.

Hiperparâmetros mal ajustados podem levar a problemas como overfitting, onde o modelo se ajusta excessivamente aos dados de treinamento, ou underfitting, onde o modelo não consegue capturar a complexidade dos dados.

Estes são os hiperparâmetros para controle de árvores de gradient boosted:

| Hiperparâmetro | Função | Impacto |
| :--- | :--- | :--- |
``learning_rate`` | Conhecido como "eta", define o "tamanho do passo" de correção de cada árvore. | Variando entre 0 e 1. Menores valores exigem mais árvores, mas tornam o modelo mais robusto. |
``n_estimators`` | Número de árvores. | Mais árvores aumentam a capacidade, mas também a complexidade do modelo, levando também ao aumento do tempo de treinamento quanto a capacidade do modelo. Árvores em excesso podem levar ao overfitting |
``max_depth`` | Profundidade individual de cada árvore. | Captura relações mais complexas, mas é o principal causador de overfitting. Por convenção o valor *default* é 6 |
``gamma`` | Conhecido como *multiplicador de Lagrange*, controla a quantidade mínima de redução de perda necessária para realizar uma nova divisão em um nó folha das árvores. | Quanto menor o valor, evita divisões desnecessárias e mais rápido é o treinamento, porém podendo não encontrar uma solução suficientemente adequada.
``subsample``| Porcentagem dos dados usados para treinar cada árvore. |	Adiciona aleatoriedade e ajuda a evitar o "vício" nos dados de treino. |

## ⚠️ Atenção aos erros de principiante!
* **Early stopping:** Recomenda-se observar o erro durante o treinamento, visto que, treinar 1000 árvores se o erro parou de cair na árvore 200 é desperdício de recurso computacional e tempo. Para isso, o  ``early_stopping_rounds`` permite a parada do treinamento do modelo, caso não tenha evolução significativa durante um número específico de rodadas;

* **Learning rate muito alta:** Recomenda-se utilizar valores entre 0.01 até 0.1, já que valores como 0.3 ou 0.5 avançam muito rápido e tornam o treinamento instavel. Enquanto valores muito baixos, podem levar muito tempo para convergir. Para compensar, pode-se aumentar ``n_estimators`` para manter o desempenho do modelo sem sacrificar a estabilidade do treinamento;

* **Ignorar a escala das labels em regressão:** O XGBoost é robusto em lidar problemas de regressão com valores muito discrepantes. No entanto, recomenda-se aplicar escalonamento ou padronização, afim de evitar viéses na importância das features. Para isso, frameworks como ``StandardScaler`` e ``MinMaxScaler`` podem ter impacto positivo no desempenho do XGBoost ao lidar com valores de entrada grandes;

## 📈 Vantagens & Limitações

| ✅ Vantagens | ❌ Limitações |
|:--- | :--- |
**Velocidade:** Processamento paralelo e otimização de cache de CPU. | **Black box:** Difícil para explicar visualmente o caminho e a lógica de diversas árvores sequenciais.  |
**Robustez para valores faltantes:** Com um algoritmo que reconhece a esparsidade dos dados, mantendo um bom desempenho se houver valores nulos no dataset. | **Memória:** Pode consumir muita RAM se o dataset for massivo e não houver otimização de tipos ou técnicas para adaptar o desempenho. |
**Regularização nativa:** Apresenta uma menor tendência a "decorar" o ruído. | **Curva de aprendizado mais alta:** Devido a alta personalização, pode ser mais difícil de ajustar e configurar corretamente em comparação com outros algoritmos. |


## 🧩 Quando usar?
* **Performance máxima e competições:** Quando as prioridades são as métricas de eficiência e acurácia, como em competições no [Kaggle](https://www.kaggle.com/). No entando, será importante considerar a disponibilidade de recursos computacionais e se a velocidade do tempo de treinamento é justificável dado o poder preditivo;

### 📋 Aplicações
* **Previsão de vendas:** Utilizado para modelagem preditiva, tendo em vista o bom desempenho para capturar sazonalidades e tendências complexas em dados históricos de vendas;

* **Risco de crédito:** Identificar padrões em comportamentos de crédito de clientes e prever o risco de operações bancárias;


## 🎮 Implementação Rápida (Python)
``` python
import xgboost as xgb
from sklearn.model_selection import train_test_split

# 'binary:logistic' para classificação
# 'reg:squarederror' para regressão

model = xgb.XGBClassifier(
    n_estimators=500,
    learning_rate=0.05,
    max_depth=6
)

# Treino com early stopping
model.fit(
    X_train, y_train,
    eval_set=[(X_test, y_test)],
    verbose=False
)

# Predição
previsoes = model.predict(X_test)
```

## 🔗 Referências e Links Adicionais
* [Documentação Oficial do XGBoost](https://xgboost.readthedocs.io/en/stable/#)
* [Documentação do Scikit Learn para XGBoost de Classificação (GradientBoostingClassifier)](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html)
* [Documentação do Scikit Learn para XGBoost de Regressão (GradientBoostingRegressor)](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)
* [Fórum de XGBoost](https://xgboosting.com/)