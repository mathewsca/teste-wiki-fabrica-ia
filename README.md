# 🏭 Wiki da Fábrica de IA 🤖

Bem-vindo à wiki do projeto **Fábrica de IA**, uma iniciativa voltada à aplicação de inteligência artificial para impulsionar a **transformação digital no governo do Estado do Piauí**.

Esta wiki está estruturada para fornecer uma visão completa da organização metodológica, técnica e operacional da Fábrica de IA. Cada seção aborda um aspecto fundamental do ciclo de vida de projetos de IA, desde a concepção até a entrega contínua com práticas de MLOps e transformação digital.

---

## 🧭 Guia de Navegação

### 🗂 Projeto e Negócio
*Documentação institucional, metodológica e organizacional.*
* [Visão geral](docs/01-projeto/visao-geral.md)
* [Comunicação](docs/01-projeto/comunicacao.md)
* [Metodologias](docs/01-projeto/metodologia.md)
* [Organograma](docs/01-projeto/organograma.md)
* [Projetos desenvolvidos](docs/01-projeto/.md)

---

### ⚙️ Eng. de Software e MLOps
*Processos de desenvolvimento e governança de código*

* [Git & Branching](docs/02-engenharia-mlops/git-flow.md) 
* [Ciclo de Vida de ML](docs/02-engenharia-mlops/ciclo-vida-ml.md)
* [Guias Técnicos](docs/02-engenharia-mlops/ciclo-vida-ml.md)

---

### 🧠 Base de Conhecimento
*Fundamentação teórica, pesquisa de modelos e referências científicas.*

* **Estatística:** 
    * [Regressão Linear](docs/03-base-conhecimento/estatistica/teste-hipotese.md)

* **Machine Learning:** 
    * [Árvore de Decisão](docs/03-base-conhecimento/machine-learning/arvore-decisao.md)
    * [Random Forest](docs/03-base-conhecimento/machine-learning/random-forest.md) 
    * [Regressão Logística](docs/03-base-conhecimento/machine-learning/regressao-logistica.md)
    * [XGBoost](docs/03-base-conhecimento/machine-learning/xgboost.md) 

* **Deep Learning:** 
    * [Autoencoder](docs/03-base-conhecimento/deep-learning/autoencoder.md)
    * [LSTM (Long Short-Term Memory)](docs/03-base-conhecimento/deep-learning/lstm.md)
    * [MLP (Multi-Layer Perceptron)](docs/03-base-conhecimento/deep-learning/mlp.md)
    * [Transformers](docs/03-base-conhecimento/deep-learning/transformer.md)


* [**Referências e leituras complementares**](docs/03-base-conhecimento/leituras-complementares.md)
    * [Glossário](docs\03-base-conhecimento\glossario.md)

---

### 🛠️ Ferramentas e Infraestrutura
*Guias práticos sobre o stack tecnológico e ambiente computacional.*

- **Stack de Ferramentas**

    Ferramenta | Função
    | :---: | :--- |
    | [Airflow](docs/04-ferramentas/airflow.md) | Orquestração de DAGs e pipelines de ETL. |
    | [Docker](docs/04-ferramentas/docker.md) | Containerização do ambiente de treino. |
    | [MLflow](docs/04-ferramentas/mlflow.md) | Tracking de experimentos e registro de modelos. |


- **Guia de Frameworks e Bibliotecas**

- **Infraestrutura Computacional**

---

### 📖 Como Contribuir?
Para manter a Wiki organizada, siga estes passos ao adicionar um novo arquivo:
1. Verifique a existência de modelos prontos para o arquivo que deseja contribuir:
    - [Template para apresentações](docs/00-templates/template-apresentacao.md)
    - [Template para relatórios](docs/00-templates/template-relatorio.md)
    - [Template para base de conhecimento](docs/00-templates/template-modelo.md)

2. Adicione o link do novo arquivo na tabela correspondente acima.
3. Abra um **Pull Request** para revisão do conteúdo.
