# 🌳 Regressão Logística

> **Status:** 🟨 Em revisão     
> **Tags:** #Supervisionado #Classificacao #Probabilidade #Linear


---


## 📝 O que é o modelo?

A **Regressão Logística** é um algoritmo de aprendizado *supervisionado* e de *classificação*, usado para prever a probabilidade de uma amostra pertencer a uma classe específica ou de um evento ocorrer, geralmente binária, como "Sim/Não" ou "0/1, ajudando a tomar decisões baseadas em dados

Diferente da [Regressão Linear](/docs/03-base-conhecimento/estatistica/regressao-linear.md), que prevê números contínuos, a Regressão Logística utiliza uma função matemática para "achatar" qualquer valor numérico para um intervalo entre 0 e 1.


![Regressão Logística]()


## 💡 Como funciona?

> analogia didática

### Lógica do modelo
O modelo consiste em base na aleatoriedade, obtida do seguinte modo:

O modelo utiliza a **Função Sigmóide** para transformar a saída da equação linear.

- **Combinação Linear:** O modelo calcula um score baseado nos pesos das variáveis, exemplo:
$$
z = w1x1 + w2x2 + b
$$

- **Função Logística Sigmóide:** Esse score $z$, gera um valor entre 0 e 1, passado pela função:
$$
1 / (1 + e^{-z})
$$

- **Fronteira de Decisão:** Define-se um limite, ou *threshold*. Se a probabilidade for $\ge 0.5$, classe A; se for $< 0.5$, classe B.

- **Gráfico Sigmóide:** Plotando a equação de regressão logística, obtem o gráfico abaixo:

![Função Sigmóide](https://d1.awsstatic.com/S-curve.36de3c694cafe97ef4e391ed26a5cb0b357f6316.png)

### Binária
O modelo de regressão logística binário é utilizado em problemas de classificação onde só existam dois resultados, verdadeiro ou falso, sim ou não, 0 ou 1. Nesse caso,como o modelo entrega resultados contínuos entre 0 e 1, utiliza-se o *treshold* arredondando para um resultado binário;

### Multinomial
O modelo de regressão logística multinomial é utilizado em problemas onde existam diversos resultados possíveis. Desse modo, os valores dentro de intervalo de 0 e 1 são mapeados, e o modelo agrupa os resultados mais próximos desses valores;

### Ordinal
Esse é um modelo de regressão logística multinomial, mas utilizado para problemas com resentações de classes, onde não existe uma distância explicita entre as categorias, por exemplo, pesquisas de satisfação que avaliam o atendimento como: "ruim", "regular" e "ótimo";


## ⚙ Principais Hiperparâmetros

Os hiperparâmetros são configurações de um modelo que podem alterar seu desempenho e eficácia. Diferente dos parâmetros do modelo, que são ajustados automaticamente durante o treinamento, os hiperparâmetros devem ser definidos antes do processo de aprendizado.

Hiperparâmetros mal ajustados podem levar a problemas como overfitting, onde o modelo se ajusta excessivamente aos dados de treinamento, ou underfitting, onde o modelo não consegue capturar a complexidade dos dados.

Na Regressão Logística, os hiperparâmetros focam em evitar que o modelo "vicie" em certas variáveis, utilizando técnicas para regularização:

| Hiperparâmetro | Função | Impacto |
| :--- | :--- | :--- |
| `penalty` | Tipo de reguralização, `l1`, `l2`, `elsticnet` ou `None`. | Ajuda a evitar o overfitting punindo coeficientes muito altos. Deve-se verificar a compatibilidade com o `solver`.|
| `C` | Inverso da força da reguralização. | Valores menores criam uma regularização mais forte, simplificando a penalização do modelo. |
| `solver` | Algoritmo utilizado para otimizar os pesos, `liblinear`, `lbfgs`. | Para conjuntos de dados menores `liblinear` é recomendável, mas só lida com classificação binária. Enquanto `lbfgs` é recomendável para problemas multiclasse $\ge 3$ |
| `max_iter` | Número máximo de tentativas para o modelo convergir. | É necessário aumentar se o modelo não encontrar uma solução aceitavel,no entanto pode levar mais tempo. |

## ⚠️ Atenção aos erros de principiante!
* **Multicolinearidade:** É recomendável remover variáveis com alta correlação, o modelo pode ficar instável;

* **Relações não-lineares:** O modelo assume que a relação entre as variáveis independentes e o logarítmo das probabilidades da variável dependente é linear. Se os dados tiverem padrões complexos, como curvas e círculos, um modelo de regressão logística puro pode não ser o ideal;

* **Sensibilidade a outliers:** Como o modelo utiliza a curva sigmóide, valores fora do padrão podem alterar a curva desbalanceado a equação, prejudicando a probabilidade dos outros pontos;


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

* **Gestão da manutenção:** Com a análise de regressão logística é utilizada em industrias para prever falhas em peças e máquinas, com isso é possível planejar paradas no chão de fábrica para manutenções preventivas e reduzir prejuízos por paradas inesperadas;

* **Prevenção de doenças:** Com o modelo de regressão logística aplicado em histórico de exames, doenças familiares e genes, é possivel estimar a probabilidade de doenças em pacientes;

## 🎮 Implementação Rápida (Python)
```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

# Inicializando o modelo
# C=1.0 é o padrão;
# penalty='l2' é o padrão
model = LogisticRegression(
    C=1.0, 
    solver='lbfgs', 
    max_iter=1000
)

# Treino e Predição
model.fit(X_train, y_train)
previsoes = model.predict(X_test)

# Para ver as probabilidades em vez da classe final
probabilidades = model.predict_proba(X_test)
```


## 🔗 Referências e Links Adicionais
- [Documentação Oficial Scikit-Learn (LogisticRegression)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)