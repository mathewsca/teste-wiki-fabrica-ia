# 📈 Regressão Lineal (Simples e Múltipla)

> **Status:** 🟨 Em revisão 
> **Tags:** #Supervisionado #Regressao #Estatistica #Parametrico #Interpretavel


---


## 📝 O que é o modelo?

A **Regressão Linear** é um modelo estatístico **supervisionado** que busca estabelecer uma relação matemática entre uma variável dependente ou variável alvo, como o que você quer prever, o $Y$, e uma ou mais variáveis independentes, que são as variáveis preditoras, o $X$. O objetivo central é encontrar a reta, ou plano no caso de múltiplas variáveis, que melhor descreve a tendência dos dados, minimizando a distância entre os pontos reais e as previsões do modelo.

![Gráfico de Regressão Linear](https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/LinearRegression.svg/330px-LinearRegression.svg.png)

## 💡 Como funciona?

> 

### Lógica do modelo

O modelo assume que a relação entre as variáveis pode ser resumida pela equação da reta:
$$y = \beta_0 + \beta_1x + \epsilon$$

* **Variável dependente ($y$):** É a variável afetada por outras variáveis em um experimento ou estudo. A característica que esta sendo observada para entender relações de causa e efeito;

* **Variável independe ($x$):** É a variável explicativa, ou seja, a variável controlada em um experimento para observar seu efeito sobre a variável dependente;

* **Intercepto ($\beta_0$):** Define onde a reta cruza o eixo Y, ou seja, onde o valor de $y$ quando $x$ é zero;

* **Coeficiente ($\beta_1$):** Define a inclinação da reta e indica o quanto $y$ aumenta para cada unidade extra de $x$;

* **Erro ($\epsilon$):** É a diferença entre o que o modelo previu e o que realmente aconteceu. O modelo utiliza o método dos **Mínimos Quadrados** para reduzir a soma desses erros ao quadrado;

### Regressão Linear Simples
Existem dois tipos, a simples e a múltipla. A Regressão Linear Simples modela a relação entre uma **única variável independente** e uma variável dependente. Utilizada em casos onde existe uma hipótese de relação direta entre duas variáveis.

### Regressão Linear Múltipla
Nesse tipo, é considerado **várias variáveis independentes** para prever uma variável dependente. Utilizada em situações onde múltiplos fatores podem interferir no resultado, por exemplo: prever a quantidade de pessoas em um parque de diversões, pode-se considerar fatores como datas comemorativas ou feriados, fatores climáticos como índices pluviométricos, temperatura, outros eventos ocorrendo no mesmo dia, etc.


## 📉 Avaliação do Modelo
Para avaliar um modelo de Regressão Linear, deve-se considerar métricas específicas para avaliar a consistência do modelo:

* **Mean Squared Error (MSE) ou Erro Quadrático Médio (EQM):** 
Onde observa-se a média das diferenças quadradas entre o valor real ($y_r$) e o valor previsto ($y_p$). Uma métrica estatística que mede a precisão de modelos preditivos, definida pela fórmula:

$$
MSE = \frac1n\sum_{i=1}^{n}(y_r – y_p)^2
$$

* **Erro Absoluto Médio (MAE):** Onde é calculado a média das diferenças absolutas entre as previsões e os valores reais. Com essa métrica é possível observar a média dos erros na previsão utilizando a fórmula:

$$
MAE = \frac1n\sum_{i=1}^{n}|y_r – y_p|
$$

* **Coeficiente de Determinação ($R^2$):** É uma métrica de ajuste do modelo, que indica a proporção da variabilidade da variável dependente que é explicada pelo modelo. Com valores de 0 a 1, podendo ser expresso em valores percentuais, quanto mais próximo de 1, mais adequando o modelo está. Exemplo: $R^2 = 0,9145$, indica que o modelo explica $91,45\%$ das variáveis independentes e se ajusta bem aos dados. Com a fórmula:

$$
R^2 = 1 - \frac{\sigma_r^2}{\sigma^2} = 1 - \frac{\sum_{i=1}^n(y_i - \widehat{y}_i)^2}{\sum_{i=1}^n(y_i - \overline{y}_i)^2}
$$

- $R^2$: Coeficiente de determinação.
- $\sigma_r^2$: Variância residual.
- $\sigma^2$: Variância da variável dependente $y$.
- $y_{i}$: Valor da variável dependente da observação $i$.
- $\widehat{y}_{i}$: Valor aproximado pelo modelo para observação $i$.
- $\overline{y}$: Média da variável dependente em todas as observações.


## ⚠️ Atenção aos erros de principiante!

* **Correlação não é causalidade:** Se a reta cresce, não significa que $X$ causa $Y$. Pois pode haver outras variáveis ocultas que influênciam esse comportamento da equação;

* **Extrapolação de longo prazo:** A extrapolação busca prever valores de uma função fora de um intervalo conhecido, baseado no comportamento conhecido dentro desse intervalo. Desse modo, pressupõe que o futuro terá um comportamento semelhante a o passado, no entanto, não uma suposição segura. Recomenda-se prever valores de $x$ para intervalos de curto prazo,não muito além do que existe no dados de treinamento;

* **Colinearidade:** Quando variáveis independentes estão altamente correlacionadas, impactando negativamente no desempenho do modelo. Podendo ser corrigido com uma simplificação, como remover variáveis redundantes, irrelevantes ou agregar variáveis;


## 📈 Vantagens & Limitações

| ✅ Vantagens | ❌ Limitações |
|:--- | :--- |
**Transparência:** Possibilita explicar exatamente o peso de cada variável no resultado.| **Simplicidade:** Não consegue capturar relações complexas ou equações e comportamentos não lineares.
**Velocidade:** É um dos modelos mais leves e rápidos para treinamento e interpretação. | **sensibilidade a outliers:** Pontos extremos e discrepantes distorcem os valores da equação reta facilmente.
**Baseline:** Recomendado para identificar o quão previsível é um problema antes de usar modelo mais complexos. | **Requisitos:** Requer que os dados sigam os pressupostos estatísticos para ser válido e aplicável.

## 🧩 Quando usar?

* **Suposições estatísticas lineares:** Para realizar uma análise por modelo de **Regressão Linear** existem suposições, ou seja, regras pelas quais os dados devem se adequar para serem analisados:
    * Valores contínuos e com baixa discrepância entre si
    * Observações independentes uma das outras
    * Os erros devem seguir uma distribuição normal

* **Análise Exploratória de Dados:** Muito recomendado para avaliar as relações e correlações entre as variáveis, bem como tendências ou padrões, alem de ser importante para identificar e priorizar variáveis para modelos mais complexos por meio da *análise de sensibilidade*;

### 📋 Aplicações

* **Previsão e especulação imobiliária:** Utilizando variáveis do imóvel, exemplo, quantidade de banheiros, quantidade de quartos e suítes, metros quadrados, etc. É possíver prever os valores dos imóveis tendo como base o valor de outros imóveis na região;

* **Previsão de demanda:** Com base no histórico de vendas, além de outras variáveis é possível desenvolver um modelo de regressão linear para prever valores de vendas futuras de curto prazo;

## 🎮 Implementação Rápida
A **Regressão Linear** é um modelo simples e bem difundido, desse modo, pode ser implementado em diversos formatos, utilizando Excel, R, MATLAB, etc. Porém o exemplo a seguir será implementado em **Python** utilizando a biblioteca do **Scikit Learn**.

``` Python
# Importando bibliotecas necessárias from sklearn.

model_selection import train_test_split from sklearn.linear_model import LinearRegression from sklearn.metrics import mean_squared_error, r2_score import pandas as pd # 

Carregando os dados data = pd.read_csv('caminho_para_o_arquivo.csv') 

# Separando variáveis independentes e dependentes 
X = data[['variavel_independente_1', 'variavel_independente_2']] 

# Exemplo de múltiplas variáveis 
y = data['variavel_dependente'] 

# Dividindo os dados em treino e teste 
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42) 

# Criando o modelo de regressão linear 
model = LinearRegression()
model.fit(X_train, y_train) 

# Fazendo previsões 
y_pred = model.predict(X_test) 

# Avaliando o modelo 
mse = mean_squared_error(y_test, y_pred) 
r2 = r2_score(y_test, y_pred) 
print(f'Erro quadrado médio: {mse:.2f}') print(f'Coeficiente de determinação R^2: {r2:.2f}')
```


## 🔗 Referências e Links Adicionais
- [Documentação Oficial do Scikit Learn (Linear Models)](https://scikit-learn.org/stable/modules/linear_model.html)
- [Documentação Oficial da Microsoft Excel para Regressão Linear](https://support.microsoft.com/pt-br/office/proj-lin-fun%C3%A7%C3%A3o-proj-lin-84d7d0d9-6e50-4101-977a-fa7abf772b6d)
- [Aplicação prática da Regressão Linear em Linguagem R pelo Instituto de Pesquisa Econômica Aplicada (Ipea)](https://ipeadata-lab.github.io/curso_r_intro_202409/08_regressao_linear.html)
- [Documentação Oficial do MATLAB para Regressão Linear](https://www.mathworks.com/help/matlab/data_analysis/linear-regression.html)