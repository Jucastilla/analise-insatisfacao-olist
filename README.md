# Análise de Dados | E-commerce

## Análise da Insatisfação dos Consumidores com Python

## Sobre o Projeto

Este projeto foi desenvolvido durante a formação em Análise de Dados da EBAC, no contexto do Projeto de Parceria com a Semantix.

A proposta do projeto consiste em identificar uma problemática real e relevante que possa ser investigada por meio da análise de dados, utilizando fontes de dados públicas e não confidenciais. A escolha da problemática e da base de dados ficou a cargo do aluno.

Para o desenvolvimento deste projeto, foi utilizada uma base pública de dados da Olist, empresa brasileira de e-commerce. O conjunto de dados reúne informações sobre clientes, produtos, pagamentos, vendedores, entregas e avaliações dos consumidores.

A problemática escolhida foi a insatisfação dos consumidores no e-commerce. A partir dos dados disponíveis, o projeto busca compreender quais fatores estão relacionados às avaliações negativas dos clientes e identificar padrões que possam auxiliar na tomada de decisões e na melhoria da experiência do consumidor.

## Objetivo

Analisar os fatores relacionados à insatisfação dos consumidores no e-commerce, identificando padrões associados às avaliações negativas e desenvolvendo um modelo preditivo capaz de identificar pedidos com maior probabilidade de resultar em insatisfação.

A análise busca ainda transformar os resultados obtidos em informações úteis para o negócio, permitindo identificar fatores, categorias, regiões e períodos que demandam maior atenção.

## Etapas Desenvolvidas

### 1. Coleta e Fontes de Dados

Para o desenvolvimento do projeto, foi utilizado o conjunto de dados público **Brazilian E-Commerce Public Dataset by Olist**, disponibilizado pela Olist na plataforma Kaggle.

A base é composta por diferentes arquivos estruturados no formato CSV, contendo informações sobre clientes, pedidos, itens, produtos, vendedores, pagamentos, entregas e avaliações dos consumidores.

Os dados foram obtidos por meio de download direto da plataforma Kaggle e posteriormente armazenados no Google Drive para acesso e processamento no Google Colab.

**Fonte dos dados:**  
[Brazilian E-Commerce Public Dataset by Olist - Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

### 2. Tratamento e Preparação dos Dados

A preparação dos dados foi realizada no Google Colab utilizando Python, principalmente com Pandas e NumPy.

Inicialmente, foi analisada a estrutura das diferentes bases, considerando suas colunas, tipos de dados, valores ausentes, duplicidades e diferentes níveis de granularidade.

Foi definida como unidade de análise do projeto:

**1 linha = 1 pedido.**

Como algumas tabelas apresentavam múltiplos registros associados ao mesmo pedido, as informações de itens, pagamentos e avaliações foram tratadas e agregadas por `order_id` antes da integração com a base principal.

Nesta etapa foram realizadas:

- Importação e inspeção das bases;
- Análise dos tipos de dados e valores ausentes;
- Verificação de duplicidades e da granularidade das tabelas;
- Tratamento de pedidos com múltiplos itens, pagamentos e avaliações;
- Agregação das informações por pedido;
- Integração das diferentes tabelas;
- Tratamento e padronização dos dados;
- Criação de variáveis derivadas;
- Definição da variável-alvo de insatisfação;
- Construção da base analítica final;
- Criação de uma base específica para a etapa de modelagem preditiva.

Ao final da preparação, foram gerados os arquivos `olist_analytical_dataset.csv` e `olist_modeling_dataset.csv`, utilizados respectivamente nas etapas de análise exploratória e modelagem preditiva.

### 3. Análise Exploratória de Dados (EDA)

Após a preparação da base analítica, foi realizada a análise exploratória dos dados no Google Colab utilizando Python e bibliotecas como Pandas, NumPy, Matplotlib e Seaborn.

A análise teve como objetivo compreender o comportamento da insatisfação dos consumidores e investigar fatores que poderiam estar relacionados às avaliações negativas.

Foram analisados aspectos como:

- Distribuição entre consumidores insatisfeitos e não insatisfeitos;
- Tempo e prazo de entrega dos pedidos;
- Ocorrência de atrasos;
- Valores dos produtos, frete e valor total dos pedidos;
- Quantidade de itens e vendedores por pedido;
- Categorias de produtos;
- Distribuição da insatisfação entre os estados;
- Evolução da insatisfação ao longo do tempo.

Entre os principais resultados observados, destacam-se:

- 12,81% dos pedidos analisados foram classificados como insatisfeitos;
- Pedidos atrasados apresentaram uma taxa de insatisfação significativamente superior à dos pedidos entregues dentro do prazo;
- Consumidores insatisfeitos apresentaram maior tempo médio de entrega;
- A antecedência da entrega em relação ao prazo estimado apresentou diferenças relevantes entre os grupos de satisfação;
- Foram identificadas diferenças nas taxas de insatisfação entre categorias de produtos, estados e períodos analisados.

Esses resultados permitiram identificar padrões relevantes para a problemática estudada e serviram de base para a etapa de modelagem preditiva.

### 4. Modelagem Preditiva

Após a análise exploratória, foi desenvolvida uma etapa de modelagem preditiva com o objetivo de avaliar a possibilidade de identificar pedidos com maior probabilidade de resultar em insatisfação dos consumidores.

A variável-alvo utilizada foi a classificação de satisfação dos pedidos, dividida entre **Insatisfeito** e **Não insatisfeito**.

A base de modelagem utilizada nesta etapa possui 95.824 registros e 34 colunas. Para o treinamento dos modelos, os dados foram divididos entre conjuntos de treino e teste, preservando a proporção da variável-alvo.

Foram avaliadas três abordagens:

- Modelo baseline;
- Regressão Logística;
- Random Forest.

Os modelos foram avaliados utilizando métricas como acurácia, precisão, recall, F1-score e ROC-AUC.

Os principais resultados foram:

| Modelo | Acurácia | Precisão | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Baseline | 87,20% | 0,00% | 0,00% | 0,00% | 50,00% |
| Regressão Logística | 81,02% | 34,77% | 55,09% | 42,64% | 75,30% |
| Random Forest | 84,26% | 40,89% | 51,43% | 45,56% | 75,95% |

Embora o modelo baseline apresente maior acurácia, ele não consegue identificar os pedidos insatisfeitos, apresentando recall e F1-score iguais a zero. Esse resultado evidencia a importância de considerar outras métricas além da acurácia em uma base com classes desbalanceadas.

Entre os modelos avaliados, o Random Forest apresentou o maior F1-score e ROC-AUC, demonstrando melhor equilíbrio na identificação dos casos de insatisfação.

A análise de importância das variáveis do Random Forest destacou principalmente:

- Diferença entre a data de entrega e o prazo estimado;
- Ocorrência de atraso;
- Tempo de entrega;
- Quantidade de itens;
- Valor do frete.

Os resultados reforçam a relevância das características relacionadas à logística para a identificação de pedidos com maior risco de insatisfação.

### 5. Visualização dos Dados no Looker Studio

Os resultados da análise foram consolidados em um dashboard desenvolvido no Looker Studio, com o objetivo de apresentar os principais indicadores e padrões relacionados à insatisfação dos consumidores de forma visual e acessível.

O dashboard foi estruturado em duas páginas complementares.

#### Visão Geral

A primeira página apresenta os principais indicadores do conjunto de dados:

- Taxa de insatisfação;
- Total de pedidos analisados;
- Taxa de atraso;
- Tempo médio de entrega;
- Ticket médio.

Também são apresentadas análises sobre:

- Impacto do atraso na taxa de insatisfação;
- Tempo médio de entrega de consumidores insatisfeitos e não insatisfeitos;
- Categorias de produtos com maiores taxas de insatisfação.

#### Análise Detalhada

A segunda página complementa a visão geral com análises voltadas à distribuição da insatisfação, incluindo:

- Desempenho por estado, considerando quantidade de pedidos, taxa de insatisfação e tempo médio de entrega;
- Evolução da taxa de insatisfação ao longo dos meses.

A página também apresenta as conclusões da análise e recomendações baseadas nos resultados encontrados, permitindo relacionar os indicadores apresentados a possíveis ações para redução da insatisfação dos consumidores.

#### Dashboard

O dashboard interativo pode ser acessado pelo link abaixo:

[Visualizar Dashboard no Looker Studio](https://datastudio.google.com/reporting/21cec6d7-f838-4c9c-ac2d-6a284944ebd9)


### 6. Conclusões e Recomendações

A análise demonstrou que a insatisfação dos consumidores no e-commerce está fortemente associada a fatores relacionados ao processo logístico, especialmente ao cumprimento dos prazos de entrega.

Entre os pedidos atrasados, a taxa de insatisfação alcançou 54,07%, enquanto nos pedidos entregues dentro do prazo foi de 9,22%. Os consumidores insatisfeitos registraram tempo médio de entrega de 20,21 dias, enquanto entre os não insatisfeitos esse tempo foi de 11,39 dias.

Além dos fatores logísticos, foram identificadas diferenças nas taxas de insatisfação entre categorias de produtos, estados e períodos do ano, demonstrando que o problema não ocorre de maneira uniforme e permitindo identificar segmentos que demandam maior atenção.

A etapa de modelagem preditiva reforçou a importância das variáveis relacionadas à entrega. Entre as variáveis de maior relevância para o modelo Random Forest estão a diferença entre a entrega e o prazo estimado, a ocorrência de atraso e o tempo de entrega.

Com base nos resultados, recomenda-se:

- Priorizar o monitoramento dos prazos de entrega;
- Identificar antecipadamente pedidos com maior risco de atraso;
- Direcionar atenção especial a categorias e regiões com maiores taxas de insatisfação;
- Acompanhar a evolução da insatisfação ao longo do tempo;
- Utilizar indicadores de desempenho logístico como apoio à tomada de decisão;
- Explorar o modelo preditivo como ferramenta de apoio para identificação de pedidos com maior risco de insatisfação.

Os resultados demonstram como a análise de dados pode contribuir para transformar informações sobre pedidos, entregas e avaliações em conhecimento aplicável ao negócio, permitindo identificar fatores associados à insatisfação e apoiar ações voltadas à melhoria da experiência do consumidor.

## Habilidades Demonstradas

- Análise de Dados
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Google Colab
- Limpeza e Preparação de Dados
- Análise Exploratória de Dados (EDA)
- Engenharia de Variáveis
- Machine Learning
- Regressão Logística
- Random Forest
- Avaliação de Modelos Preditivos
- Data Visualization
- Looker Studio
- Criação de Dashboards
- Análise de Indicadores
- Geração de Insights para Negócios

## Arquivos do Projeto

### Notebooks

Os notebooks desenvolvidos no Google Colab estão organizados de acordo com as etapas do projeto:

📓 [01 - Preparação dos Dados](notebooks/01_data_preparation.ipynb)  
Preparação, tratamento, integração dos dados e construção das bases analíticas.

📓 [02 - Análise Exploratória de Dados (EDA)](notebooks/02_eda.ipynb)  
Análise exploratória e investigação dos principais fatores relacionados à insatisfação dos consumidores.

📓 [03 - Modelagem Preditiva](notebooks/03_modelagem_preditiva.ipynb)  
Desenvolvimento, comparação e avaliação dos modelos preditivos.

### Dashboard

📊 [Visualizar Dashboard em PDF](dashboard/dashboard_olist.pdf)

🔗 [Acessar Dashboard Interativo no Looker Studio](https://datastudio.google.com/reporting/21cec6d7-f838-4c9c-ac2d-6a284944ebd9)
