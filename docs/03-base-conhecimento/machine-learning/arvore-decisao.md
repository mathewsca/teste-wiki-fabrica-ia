# 🌳 Árvore de Decisão (Decision Tree)

> **Status:** 🟨 Em revisão     
> **Tags:** #Supervisionado #Classificacao #Regressao #Interpretabilidade


---


## 📝 O que é o modelo?

A Árvore de Decisão é um algoritmo de aprendizado **supervisionado**, utilizado tanto para **classificação** quanto para **regressão**. Ele estrutura o processo de decisão em uma série de perguntas binárias (sim/não), criando uma estrutura hierárquica que se assemelha a um fluxograma.

## 💡 Como funciona?

> No jogo **20 Perguntas**, para adivinhar um algo, você faz perguntas estratégicas: "É um animal?", "Ele voa?", "É maior que uma bola de basquete?". Cada resposta elimina várias possibilidades até que você chegue a um conjunto limitado de possibilidades, levando a uma decisão final.


### Lógica do modelo
O modelo funciona dividindo os dados repetidamente:
1. **Nó Raiz:** Escolhe a característica, ou *feature* que melhor divide os dados inicialmente, usando métricas como *Gini* ou *Entropy*;
2. **Ramos:** São os caminhos que os dados tomam dependendo da resposta à pergunta;
3. **Nós Internos**: Pontos onde as decisões são tomadas e os dados se distribuem;
4. **Nós Folha ou Folha:** São os nós finais que representam a previsão, a classe ou o valor numérico, decisão final;

!["Árvore de Decisão"](https://cdn-wcsm.alura.com.br/2025/04/arvore-gif.gif)

### Classificação

Como mencionado no início, os modelos de árvore de decisão podem ser utilizados tanto para **classificação** como também para **regressão**. Nos modelos de classificaão a intenção é agrupar dados em classes diferentes ou conjuntos predefinidos.

### Regressão

Nas árvores de regressão, o objetivo é prever valores numéricos, ou seja, preços, temperatura, quantidade, etc., que podem variar em um intervalo.


## ⚙ Principais Hiperparâmetros

Os hiperparâmetros são configurações de um modelo que podem alterar seu desempenho e eficácia. Diferente dos parâmetros do modelo, que são ajustados automaticamente durante o treinamento, os hiperparâmetros devem ser definidos antes do processo de aprendizado.

Hiperparâmetros mal ajustados podem levar a problemas como overfitting, onde o modelo se ajusta excessivamente aos dados de treinamento, ou underfitting, onde o modelo não consegue capturar a complexidade dos dados.

Estes são os parâmetros de controle, que evitam que a árvore cresça demais ou memorize os dados de treino:

| Hiperparâmetro | Função | Impacto |
| :--- | :--- | :--- |
| `max_depth` | Profundidade máxima da árvore. | ⬆️ Mais complexidade, aumentando o risco de Overfitting. |
| `min_samples_split` | Mínimo de amostras para criar uma nova divisão. | ⬇️ Divisões mais específicas, maior risco de Overfitting. |
| `min_samples_leaf` | Mínimo de amostras que uma "folha" deve ter. | ⬆️ Suaviza o modelo, evita folhas com apenas 1 dado. |
| `criterion` | Função que mede a qualidade da divisão. | Opção de `gini`, para ser mais rápido, ou `entropy`, para ser mais rigoroso |

## ⚠️ Atenção aos erros de principiante!
* **A árvore "infinita":** Estabeleça um limite para o crescimento da árvore, defina um `max_depth`. Isso garante que ela aprenda padrões e não ruídos;

* **Dados desbalanceados:** Se você tem 90% de uma classe e 10% de outra, a árvore pode simplesmente ignorar a minoritária. Devido a isso recomenda-se o uso de `class_weight='balanced'`;

* **Variáveis com muitas categorias:** Colunas tipo "ID", nomes ou códigos únicos devem ser evitados, pois é provavel que a árvore tente criar um ramo para cada um desses valores;

## 📈 Vantagens & Limitações

| ✅ Vantagens | ❌ Limitações |
|:--- | :--- |
| **Alta interpretabilidade:** É fácil explicar por que o modelo tomou certa decisão | **Instabilidade:** Pequenas mudanças nos dados podem gerar uma árvore completamente diferente |
| **Sem pré-processamento:** Não exige normalização ou padronização de escalas dos dados | **Overfitting:** Se não for limitada, a árvore tentará memorizar o dataset de treino, não conseguindo prever padrões não aprendidos |
| **Suporta diversos tipos de dados:** Aceita variáveis numéricas e categóricas simultaneamente | **Viés de classe:** Caso os dados estejam desbalanceados, tende a favorecer a classe majoritária |


## 🧩 Quando usar?
* **Baselines Rápidos:** Para começar um projeto e entender quais variáveis são mais importantes;

* **Transparência Requerida:** Projetos onde o usuário final precise entender a lógica por trás da IA;


### 📋 Aplicações

* **Detecção de Fraude:** O algoritmo pode analisar transações, valores, localização, histórico do cliente, etc. e classificar as transações com "fradulentas" ou "não fraudulentas";

* **Aprovação de Crédito:** Definir se um cliente é "bom pagador" com base nos dados disponíveis desse cliente, renda, histórico de atrasos em pagamentos, adesão à programas de fidelidade do banco;

* **Diagnóstico Médico:** Árvores de decisão baseadas em sintomas do paciente, como: Febre? Tosse? Manchas na pele? Falta de ar? etc., ajudam a limitar quais as patologias provaveis do paciente;


## 🎮 Implementação Rápida (Python)
```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split

# Inicializando o modelo com limite de profundidade
model = DecisionTreeClassifier(max_depth=5, random_state=42)

# Treino e Predição
model.fit(X_train, y_train)
previsoes = model.predict(X_test)

# Dica: Visualize a árvore gerada
# from sklearn.tree import plot_tree
# plot_tree(model)
```


## 🔗 Referências e Links Adicionais
- [Documentação Oficial Scikit-Learn (Trees)](https://scikit-learn.org/stable/modules/tree.html)