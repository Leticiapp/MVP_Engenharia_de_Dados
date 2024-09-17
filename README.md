## MVP de Engenharia de Dados

### Descrição
Este projeto analisa dados de cotações do mercado financeiro de grandes empresas de tecnologia usando Spark e Python. O objetivo é extrair insights sobre o desempenho dessas empresas ao longo do tempo, com foco especial nos últimos anos, incluindo o período da pandemia de Covid-19.

### Objetivo
O projeto busca responder às seguintes perguntas de negócio:

* Quais os valores mínimos e máximos das cotações das empresas nos últimos anos?
* A pandemia impactou o valor das ações?
* Qual a valorização das ações em 10 anos?
* Qual o volume médio de transações das empresas com maior e menor crescimento em 10 anos?
* Quais empresas são mais novas no mercado e suas cotações médias no último ano?

### Ferramentas e Tecnologias
O projeto utiliza uma gama de ferramentas modernas de análise de dados e computação em nuvem:

* **Microsoft Azure:**
    * **Databricks:** plataforma de análise de dados baseada em Spark para processamento e análise de big data.
    * **Data Factory:** serviço de integração de dados para criar, agendar e gerenciar pipelines de ETL.
    * **Azure SQL Database:** serviço de banco de dados relacional na nuvem para armazenamento e gerenciamento de dados.
    * **Azure Data Lake Storage Gen2:** serviço de armazenamento de dados em larga escala para análise avançada. 
* **Spark:** framework de processamento de dados distribuído de código aberto para análise em larga escala.
* **Python:** linguagem de programação versátil e poderosa usada para análise de dados e visualização.
    * **Pandas:** biblioteca para manipulação e análise de dados.
    * **Matplotlib:** biblioteca para criação de gráficos e visualizações estáticas, interativas e animadas em Python.
    * **Seaborn:** biblioteca para criação de visualizações estatísticas atraentes e informativas.

### Conjunto de Dados
Os dados utilizados foram obtidos do Kaggle, uma plataforma que disponibiliza conjuntos de dados para projetos de ciência de dados. O conjunto de dados escolhido contém informações sobre os preços diários de ações e volumes de 14 empresas de tecnologia, abrangendo o período de janeiro de 2010 a janeiro de 2023.

As empresas incluídas na análise são:

* Apple
* Amazon
* Alphabet (Google)
* Meta (Facebook)
* Adobe
* Cisco Systems
* IBM
* Intel Corporation
* Netflix
* Tesla
* Salesforce
* Microsoft Corporation
* Oracle 
* NVIDIA

### Modelagem de Dados
Para garantir a organização e estrutura dos dados, foi utilizado o **Modelo Estrela**, um modelo de dados multidimensional amplamente utilizado em Data Warehouses.

* **Tabela Fato:** `stock_prices` - Contém dados sobre as cotações das empresas, incluindo:
    * Símbolo da ação
    * Data
    * Preço de abertura
    * Preço mais alto
    * Preço mais baixo
    * Preço de fechamento
    * Preço de fechamento ajustado
    * Volume de transações
* **Tabelas Dimensão:**
    * `companies` - armazena informações sobre as empresas, como:
        * Símbolo da ação 
        * Nome da empresa
    * `dates` - contém informações sobre as datas das cotações, incluindo:
        * ID da data (no formato YYYYMMDD)
        * Ano
        * Mês
        * Data completa

### Pipeline ETL
Para automatizar a ingestão, transformação e carregamento dos dados no Azure SQL Database, foi criado um pipeline ETL utilizando o Azure Data Factory.

**Etapas do Pipeline:**

1. **Extração:** Os dados brutos são extraídos do Azure Data Lake Storage Gen2, onde foram inicialmente carregados.
2. **Transformação:**  
    * Formatação do campo de data para o formato YYYYMMDD, necessário para a chave da tabela de datas.
    * Remoção de datas duplicadas na tabela `dates`, garantindo a unicidade das datas.
    * Criação de campos adicionais na tabela `dates`, como "mês", "ano" e "data completa" a partir do campo "ID da data". 
3. **Carga:** Os dados transformados são carregados no Azure SQL Database, nas tabelas `stock_prices`, `companies` e `dates`.

### Análise de Dados
A análise de dados foi realizada no Databricks, utilizando o Spark para processamento de big data e Python para análise exploratória e visualização de dados.

**Etapas da Análise:**

1. **Validação da Qualidade dos Dados:**
    * Verificação das primeiras linhas de cada tabela para garantir a correta importação dos dados.
    * Validação da quantidade de linhas nas tabelas `companies` e `stock_prices`.
    * Verificação de valores nulos em todas as colunas das três tabelas.
    * Validação da quantidade de linhas na tabela `dates` em relação à quantidade de datas distintas na tabela `stock_prices`.
    * Verificação da faixa de datas disponível para cada empresa.
2. **Análise Exploratória e Respostas às Perguntas de Negócio:**
    * **Pergunta 1:** Os valores mínimos e máximos das cotações das empresas nos últimos anos foram consultados e visualizados em um gráfico de barras, mostrando a variação dos preços para cada empresa ao longo dos anos.
    * **Pergunta 2:** O impacto da pandemia de Covid-19 foi avaliado comparando o valor médio das ações em 2019 (pré-pandemia) e 2020. Os resultados foram visualizados em um gráfico de barras, mostrando o impacto da pandemia no preço médio das ações de cada empresa.
    * **Pergunta 3:** A valorização das ações em 10 anos foi analisada comparando o valor das ações no último dia de janeiro de 2010 e 2020, calculando o percentual de crescimento ("growth"). Os resultados foram plotados em um gráfico de barras para visualização. 
    * **Pergunta 4:** O volume médio mensal de transações das empresas com maior (Netflix e NVIDIA) e menor (Oracle e IBM) crescimento em 10 anos foi calculado e visualizado em um gráfico de linhas, mostrando a evolução do volume de transações ao longo do tempo.
    * **Pergunta 5:** O desempenho diário das empresas mais novas no mercado (Meta e Tesla) foi analisado em 2022, com foco no valor médio das cotações. Os resultados foram visualizados em um gráfico de linhas, permitindo observar as oscilações no preço das ações ao longo do ano.

### Resultados
Os resultados da análise de dados são apresentados em um relatório detalhado, incluindo gráficos e tabelas. O relatório fornece insights valiosos sobre o desempenho das empresas de tecnologia no mercado financeiro, especialmente nos últimos anos.

### Conclusões
O projeto demonstra a importância da análise de dados no mercado financeiro e como ferramentas modernas de computação em nuvem podem ser utilizadas para extrair insights relevantes. A utilização do Azure Databricks, Data Factory e Azure SQL Database permitiu a criação de um pipeline de dados eficiente para análise de grandes volumes de dados. A combinação do Spark com Python se mostrou poderosa para processar, analisar e visualizar os dados de forma eficaz.

## Próximos Passos
Para trabalhos futuros, algumas sugestões são:
* Integrar dados mais recentes de cotações, incluindo os anos de 2023 e 2024.
* Incluir informações adicionais sobre as empresas de tecnologia, como indicadores financeiros, para aprofundar a análise.
* Explorar modelos de Machine Learning para previsão de preços de ações.
  
