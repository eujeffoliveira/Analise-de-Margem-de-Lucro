# Projeto SSIS e Power BI de Análise de Margem de Lucro
**Autor:** José Jefferson Santos de Oliveira<br>
**Softwares Utilizados:** SQL Server 2019, Visual Studio 2022 e SQL Server Management Studio 19<br>
**Banco de Dados de Exemplo:** ContosoRetailDW e ANALISE-LUCROS<br>

## 1. Projeto no SSIS

O projeto do SSIS foi criado para realizar os procedimentos de ETL e automatização de fluxo de dados.<br>

### Conexões

As conexões com o banco de dados foram realizadas utilizando o SQL Server Native Client 11.0.<br>
Foram criadas duas conexões, uma para o banco de dados de origem (**ContosoRetailDW**) e outra para o banco de dados de destino (**ANALISE-LUCRO**).<br>

### Pacotes

Foram criados dois pacotes no projeto do SSIS, um para a extração dos dados e outro para a carga dos dados.<br>

#### 1. Pacote de Extração

O pacote de extração foi criado para realizar a extração dos dados do banco de dados de origem (**ContosoRetailDW**).<br>
O pacote foi criado com os seguintes passos:<br>

1. **Conexão com o Banco de Dados de Origem:** Foi criada uma conexão com o banco de dados de origem (**ContosoRetailDW**).<br>
1. **Tarefa de Execução de Consulta SQL:** Foi criada uma tarefa para executar uma consulta SQL que realiza a extração dos dados das tabelas **FactSales**, **DimProduct**, **DimDate** e **DimStore**.<br>
1. **Criação de arquivo RAW:** Foi criado um arquivo RAW para armazenar os dados extraídos das tabelas e que serão utilizados na fase de transformação.<br>

#### 2. Pacote de Transformação

O pacote de transformação foi criado para realizar a transformação dos dados extraídos do banco de dados de origem (**ContosoRetailDW**).<br>
Foi criada uma conexão com o arquivo **RAW** que armazena os dados extraídos das tabelas do banco de dados de origem, a partir dele foi feito o processo de transformação descrito abaixo:<br>

##### 2.1. Tradução do nome das colunas

Foi criada uma tarefa para traduzir o nome das colunas das tabelas.<br>

##### 2.2. Remoção de valores nulos

Foi criada uma tarefa para remover os valores nulos das tabelas.<br>







## Tabela FactSales:

A tabela FactSales geralmente contém informações sobre as vendas realizadas. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável       | Descrição                                            |
|----------------|------------------------------------------------------|
| SalesID        | Identificador único da venda                         |
| ProductID      | Identificador único do produto vendido               |
| CustomerID     | Identificador único do cliente que realizou a compra |
| StoreID        | Identificador único da loja onde a venda ocorreu     |
| SalesAmount    | Valor total da venda                                 |
| Quantity       | Quantidade de produtos vendidos                      |
| DiscountAmount | Valor do desconto aplicado na venda                  |
| SalesDateKey   | Chave estrangeira para a tabela DimDate              |


## Tabela DimProduct:

A tabela DimProduct contém detalhes sobre os produtos vendidos. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável        | Descrição                                        |
|-----------------|--------------------------------------------------|
| ProductID       | Identificador único do produto                   |
| ProductName     | Nome do produto                                  |
| Category        | Categoria do produto                             |
| Subcategory     | Subcategoria do produto                          |
| Manufacturer    | Fabricante do produto                            |
| ListPrice       | Preço de lista do produto                        |
| StandardCost    | Custo padrão de produção do produto             |
| SellStartDate   | Data de início das vendas do produto             |
| SellEndDate     | Data de término das vendas do produto (se houver)|
| DiscontinuedDate| Data em que o produto foi descontinuado (se houver)|
| ProductDescription | Descrição do produto                           |


## Tabela DimDate:

A tabela DimDate contém informações sobre datas. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável        | Descrição                                        |
|-----------------|--------------------------------------------------|
| DateKey         | Chave primária que representa a data             |
| FullDate        | Data completa (ano-mês-dia)                      |
| DayOfWeek       | Dia da semana (1-7, onde 1 é domingo)            |
| DayOfMonth      | Dia do mês                                       |
| Month           | Mês                                             |
| Quarter         | Trimestre                                       |
| Year            | Ano                                              |
| HolidayFlag     | Indicador se a data é um feriado (1 para sim, 0 para não)|
| FiscalQuarter   | Trimestre fiscal                                 |
| FiscalYear      | Ano fiscal                                       |


## Tabela DimStore:

A tabela DimStore contém informações sobre as lojas onde as vendas ocorrem. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável       | Descrição                                            |
|----------------|------------------------------------------------------|
| StoreID        | Identificador único da loja                          |
| StoreName      | Nome da loja                                         |
| StoreType      | Tipo de loja (por exemplo, varejo, online, etc.)     |
| StoreManager   | Nome do gerente da loja                              |
| Address        | Endereço da loja                                     |
| City           | Cidade onde a loja está localizada                   |
| StateProvince  | Estado ou província onde a loja está localizada      |
| CountryRegion  | País ou região onde a loja está localizada           |
| PostalCode     | Código postal da loja                                |
