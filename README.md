# Análise de Insatisfação de Clientes da Olist

## Contexto

Este projeto foi desenvolvido durante a formação em **Análise de Dados da EBAC**, a partir de uma proposta acadêmica de projeto aplicado com dados públicos.

Foi utilizado o **Brazilian E-Commerce Public Dataset by Olist**, disponibilizado na plataforma Kaggle, com informações sobre clientes, pedidos, produtos, pagamentos, vendedores, entregas e avaliações dos consumidores.

A problemática escolhida foi a insatisfação dos consumidores no e-commerce, investigando fatores associados às avaliações negativas e a possibilidade de identificar pedidos com maior risco de insatisfação.

O desenvolvimento foi realizado com **Python e Google Colab** para preparação, análise e modelagem dos dados, além do **Looker Studio** para apresentação dos resultados em um dashboard.

## Objetivo

Analisar os fatores relacionados à insatisfação dos consumidores, identificar padrões associados às avaliações negativas e desenvolver modelos preditivos para avaliar a identificação de pedidos com maior probabilidade de insatisfação.

O projeto também teve como objetivo apresentar os resultados em um dashboard, destacando fatores, categorias, regiões e períodos que demandam maior atenção.

## Desenvolvimento

### Coleta e Fontes de Dados

Foi utilizado o conjunto público **Brazilian E-Commerce Public Dataset by Olist**, composto por arquivos CSV com informações sobre clientes, pedidos, itens, produtos, vendedores, pagamentos, entregas e avaliações.

Os arquivos foram obtidos por download na plataforma Kaggle e armazenados no Google Drive para acesso e processamento no Google Colab.

**Fonte:** [Brazilian E-Commerce Public Dataset by Olist — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

### Preparação e Integração dos Dados

A preparação foi realizada em Python, principalmente com **Pandas e NumPy**.

Inicialmente, foram analisados a estrutura das bases, os tipos de dados, os valores ausentes, as duplicidades e os diferentes níveis de granularidade.

Foi definida a seguinte unidade de análise:

**1 linha = 1 pedido.**

Como algumas tabelas continham múltiplos registros para um mesmo pedido, as informações de itens, pagamentos e avaliações foram tratadas e agregadas por `order_id` antes da integração com a base principal.

Essa etapa incluiu:

- Importação e inspeção das bases;
- Análise dos tipos de dados e valores ausentes;
- Verificação de duplicidades e granularidade;
- Tratamento de pedidos com múltiplos itens, pagamentos e avaliações;
- Agregação das informações por pedido;
- Integração das tabelas;
- Tratamento e padronização dos dados;
- Criação de variáveis derivadas;
- Definição da variável-alvo de insatisfação;
- Construção das bases de análise e modelagem.

Foram gerados dois arquivos:

- `olist_analytical_dataset.csv`: utilizado na análise exploratória;
- `olist_modeling_dataset.csv`: utilizado na modelagem preditiva.

### Análise Exploratória de Dados

A análise exploratória foi realizada com **Pandas, NumPy, Matplotlib e Seaborn**, investigando:

- Distribuição entre pedidos classificados como insatisfeitos e não insatisfeitos;
- Tempo e prazo de entrega;
- Ocorrência de atrasos;
- Valores dos produtos, frete e valor total dos pedidos;
- Quantidade de itens e vendedores por pedido;
- Categorias de produtos;
- Distribuição da insatisfação entre os estados;
- Evolução da insatisfação ao longo do tempo.

Os padrões identificados nessa etapa serviram de base para a modelagem preditiva.

### Modelagem Preditiva

A variável-alvo foi dividida entre **Insatisfeito** e **Não insatisfeito**.

A base de modelagem continha **95.824 registros e 34 colunas**. Os dados foram separados em conjuntos de treino e teste, preservando a proporção da variável-alvo.

Foram avaliadas três abordagens:

- Modelo baseline;
- Regressão Logística;
- Random Forest.

A avaliação considerou acurácia, precisão, recall, F1-score e ROC-AUC.

Também foi analisada a importância das variáveis no Random Forest para identificar as características de maior relevância para o modelo.

### Desenvolvimento do Dashboard

Os resultados foram consolidados em um dashboard no **Looker Studio**, organizado em duas páginas.

#### Visão Geral

A primeira página apresenta os indicadores:

- Taxa de insatisfação;
- Total de pedidos analisados;
- Taxa de atraso;
- Tempo médio de entrega;
- Ticket médio.

Também reúne análises sobre:

- Relação entre atraso e taxa de insatisfação;
- Tempo médio de entrega de pedidos classificados como insatisfeitos e não insatisfeitos;
- Categorias de produtos com maiores taxas de insatisfação.

#### Análise Detalhada

A segunda página apresenta:

- Desempenho por estado, considerando quantidade de pedidos, taxa de insatisfação e tempo médio de entrega;
- Evolução mensal da taxa de insatisfação;
- Conclusões e recomendações baseadas nos resultados.

## Resultados

### Insatisfação e Entregas

**12,81% dos pedidos analisados foram classificados como insatisfeitos.**

Os resultados mostraram uma associação entre a insatisfação e características do processo de entrega:

| Indicador | Grupo | Resultado |
|---|---|---|
| Taxa de insatisfação | Pedidos atrasados | 54,07% |
| Taxa de insatisfação | Pedidos entregues dentro do prazo | 9,22% |
| Tempo médio de entrega | Insatisfeitos | 20,21 dias |
| Tempo médio de entrega | Não insatisfeitos | 11,39 dias |

Também foram observadas diferenças na antecedência da entrega em relação ao prazo estimado entre os grupos de satisfação.

### Categorias, Estados e Períodos

Foram identificadas diferenças nas taxas de insatisfação entre categorias de produtos, estados e períodos analisados.

Esses resultados mostraram que a insatisfação não se distribuiu de maneira uniforme no conjunto de dados, permitindo identificar segmentos que demandam maior atenção.

### Desempenho dos Modelos

| Modelo | Acurácia | Precisão | Recall | F1-score | ROC-AUC |
|---|---|---|---|---|---|
| Baseline | 87,20% | 0,00% | 0,00% | 0,00% | 50,00% |
| Regressão Logística | 81,02% | 34,77% | 55,09% | 42,64% | 75,30% |
| Random Forest | 84,26% | 40,89% | 51,43% | 45,56% | 75,95% |

O baseline apresentou a maior acurácia, mas não identificou os pedidos insatisfeitos, obtendo recall e F1-score iguais a zero. Esse resultado destacou a importância de avaliar outras métricas em uma base com classes desbalanceadas.

O **Random Forest** apresentou os maiores valores de F1-score e ROC-AUC entre os modelos avaliados. A **Regressão Logística** apresentou o maior recall.

Na análise de importância das variáveis do Random Forest, destacaram-se:

- Diferença entre a data de entrega e o prazo estimado;
- Ocorrência de atraso;
- Tempo de entrega;
- Quantidade de itens;
- Valor do frete.

Esses resultados reforçaram a relevância das características relacionadas à logística para a classificação da insatisfação na base analisada.

### Entregas do Projeto

O projeto resultou em:

- Bases preparadas para análise exploratória e modelagem;
- Análise dos fatores associados à insatisfação;
- Comparação de três abordagens de modelagem;
- Dashboard com indicadores, análises e recomendações.

### Recomendações Derivadas da Análise

Com base nos resultados, foram apresentadas as seguintes recomendações:

- Priorizar o monitoramento dos prazos de entrega;
- Identificar antecipadamente pedidos com maior risco de atraso;
- Direcionar atenção a categorias e regiões com maiores taxas de insatisfação;
- Acompanhar a evolução da insatisfação ao longo do tempo;
- Utilizar indicadores logísticos como apoio à tomada de decisão;
- Explorar o modelo preditivo como ferramenta de apoio à identificação de pedidos com maior risco de insatisfação.

## Habilidades Demonstradas

- Análise de dados;
- Python;
- Pandas;
- NumPy;
- Matplotlib;
- Seaborn;
- Google Colab;
- Limpeza e preparação de dados;
- Integração de dados;
- Análise exploratória de dados (EDA);
- Engenharia de variáveis;
- Machine Learning;
- Regressão Logística;
- Random Forest;
- Avaliação de modelos preditivos;
- Visualização de dados;
- Looker Studio;
- Criação de dashboards;
- Análise de indicadores;
- Geração de insights para negócios.

## Arquivos do Projeto

### Notebooks

Os notebooks desenvolvidos no Google Colab estão organizados por etapa.

#### [01 — Preparação dos Dados](https://github.com/Jucastilla/analise-insatisfacao-olist/blob/main/notebooks/01_data_preparation.ipynb)

Preparação, tratamento, integração dos dados e construção das bases analíticas.

#### [02 — Análise Exploratória de Dados](https://github.com/Jucastilla/analise-insatisfacao-olist/blob/main/notebooks/02_eda.ipynb)

Investigação dos principais fatores relacionados à insatisfação dos consumidores.

#### [03 — Modelagem Preditiva](https://github.com/Jucastilla/analise-insatisfacao-olist/blob/main/notebooks/03_modelagem_preditiva.ipynb)

Desenvolvimento, comparação e avaliação dos modelos preditivos.

### Dashboard

- [Visualizar Dashboard em PDF](https://github.com/Jucastilla/analise-insatisfacao-olist/blob/main/dashboard/An%C3%A1lise_da_Insatisfa%C3%A7%C3%A3o_dos_Consumidores_Olist.pdf)
- [Acessar Dashboard Interativo no Looker Studio](https://datastudio.google.com/reporting/21cec6d7-f838-4c9c-ac2d-6a284944ebd9)

### Dados

[Acessar Dados do Projeto](https://github.com/Jucastilla/analise-insatisfacao-olist/tree/main/data)

A pasta `data` reúne os arquivos originais do **Brazilian E-Commerce Public Dataset by Olist** utilizados no projeto.

Os arquivos incluem informações sobre clientes, pedidos, itens dos pedidos, pagamentos, avaliações, produtos, vendedores e tradução das categorias de produtos.

O arquivo `olist_geolocation_dataset.csv` não foi incluído no repositório devido ao limite de tamanho para upload pelo GitHub. A base completa pode ser obtida na fonte original:

[Brazilian E-Commerce Public Dataset by Olist — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
