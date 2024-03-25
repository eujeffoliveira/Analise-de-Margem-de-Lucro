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
1. **Criação de arquivo RAW:** Foi criado um arquivo RAW para armazenar os dados extraídos das tabelas e que serão utilizados na fase de transformação¹.<br>

**¹** Foi necessário criar uma pré transformação dos dados da tabela **DimStore** tendo em vista que as váriaveis 'GeoLocation' e 'Geometry' estavam em um formato que não era compatível com o tipo de arquvo RAW.<br>

#### 2. Pacote de Transformação

O pacote de transformação foi criado para realizar a transformação dos dados extraídos do banco de dados de origem (**ContosoRetailDW**).<br>
Foi criada uma conexão com o arquivo **RAW** que armazena os dados extraídos das tabelas do banco de dados de origem, a partir dele foi feito o processo de transformação descrito abaixo:<br>

##### 2.1. Tradução do nome das colunas

Foi criada uma tarefa para traduzir o nome das colunas das tabelas.<br>

##### 2.2. Remoção de valores nulos

Foi criada uma tarefa para remover os valores nulos das tabelas.<br>







## Tabela FactSales:

A tabela FactSales geralmente contém informações sobre as vendas realizadas. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável       | Variável Traduzida | Tipo de Dados | Descrição                                         |
|----------------|---------------------|---------------|---------------------------------------------------|
| SalesKey       | VendaID             | int           | Chave única para cada venda                       |
| DateKey        | DataID              | datetime      | Chave para a data da venda                        |
| ChannelKey     | CanalID             | int           | Chave para o canal de vendas                      |
| StoreKey       | LojaID              | int           | Chave para a loja onde a venda ocorreu            |
| ProductKey     | ProdutoID           | int           | Chave para o produto vendido                      |
| PromotionKey   | PromocaoID          | int           | Chave para a promoção aplicada na venda           |
| CurrencyKey    | MoedaID             | int           | Chave para a moeda utilizada na transação         |
| UnitCost       | Custo_Unitario      | money         | Custo unitário do produto vendido                 |
| UnitPrice      | Preco_Unitario      | money         | Preço unitário do produto vendido                 |
| SalesQuantity  | QuantidadeVendas    | int           | Quantidade de produtos vendidos                   |
| ReturnQuantity | QuantidadeDevolucao | int           | Quantidade de produtos devolvidos                 |
| ReturnAmount   | MontanteDevolvido   | money         | Montante de dinheiro devolvido                    |
| DiscountQuantity | QuantidadeDesconto | int         | Quantidade de produtos com desconto                |
| DiscountAmount | MontanteDesconto    | money         | Montante total de desconto aplicado               |
| TotalCost      | CustoTotal          | money         | Custo total da venda (considerando devoluções)    |
| SalesAmount    | MontanteVendas      | money         | Montante total da venda                           |
| ETLLoadID      | CargaETLID      | int           | Identificador do processo de carga do ETL         |
| LoadDate       | DataCarregamento    | datetime      | Data de carga dos dados                           |
| UpdateDate     | DataAtualizacao     | datetime      | Data de atualização dos dados                     |



## Tabela DimProduct:

A tabela DimProduct contém detalhes sobre os produtos vendidos. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

|    Variável         | Variável Traduzida    | Tipo de Dados | Descrição                                         |
|---------------------|-----------------------|---------------|---------------------------------------------------|
| ProductKey          | ProdutoID          | int           | Chave única para cada produto                    |
| ProductLabel        | RotuloProduto         | nvarchar      | Rótulo do produto                                |
| ProductName         | NomeProduto           | nvarchar      | Nome do produto                                  |
| ProductDescription  | DescricaoProduto      | nvarchar      | Descrição do produto                             |
| ProductSubcategoryKey | SubcategoriaDoProdutoID  | int           | Chave para a subcategoria do produto             |
| Manufacturer        | Fabricante            | nvarchar      | Fabricante do produto                            |
| BrandName           | NomeMarca             | nvarchar      | Nome da marca do produto                         |
| ClassID             | ClasseID              | nvarchar      | ID da classe do produto                          |
| ClassName           | NomeClasse            | nvarchar      | Nome da classe do produto                        |
| StyleID             | EstiloID              | nvarchar      | ID do estilo do produto                          |
| StyleName           | NomeEstilo            | nvarchar      | Nome do estilo do produto                        |
| ColorID             | CorID                 | nvarchar      | ID da cor do produto                             |
| ColorName           | NomeCor               | nvarchar      | Nome da cor do produto                           |
| Size                | Tamanho               | nvarchar      | Tamanho do produto                               |
| SizeRange           | FaixaTamanho          | nvarchar      | Faixa de tamanho do produto                      |
| SizeUnitMeasureID   | UnidadeDeMedidaTamanhoID       | nvarchar      | ID da unidade de medida de tamanho do produto    |
| Weight              | Peso                  | float         | Peso do produto                                  |
| WeightUnitMeasureID | UnidadeDeMedidaPesoID          | nvarchar      | ID da unidade de medida de peso do produto       |
| UnitOfMeasureID     | UnidadeMedidaID       | nvarchar      | ID da unidade de medida do produto               |
| UnitOfMeasureName   | NomeUnidadeMedida     | nvarchar      | Nome da unidade de medida do produto             |
| StockTypeID         | TipoEstoqueID         | nvarchar      | ID do tipo de estoque do produto                 |
| StockTypeName       | NomeTipoEstoque       | nvarchar      | Nome do tipo de estoque do produto               |
| UnitCost            | CustoUnitario         | money         | Custo unitário do produto                        |
| UnitPrice           | PrecoUnitario         | money         | Preço unitário do produto                        |
| AvailableForSaleDate| DataDisponivelVenda   | datetime      | Data disponível para venda do produto            |
| StopSaleDate        | DataFimVenda          | datetime      | Data de término de venda do produto              |
| Status              | Status                | nvarchar      | Status do produto                                |
| ImageURL            | URLImagem             | nvarchar      | URL da imagem do produto                         |
| ProductURL          | URLProduto            | nvarchar      | URL do produto                                   |
| ETLLoadID           | CargaETLID        | int           | Identificador do processo de carga do ETL        |
| LoadDate            | DataCarregamento      | datetime      | Data de carga dos dados                          |
| UpdateDate          | DataAtualizacao       | datetime      | Data de atualização dos dados                    |

## Tabela DimDate:

A tabela DimDate contém informações sobre datas. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável             | Variável Traduzida  | Tipo de Dados | Descrição                                           |
|----------------------|---------------------|---------------|-----------------------------------------------------|
| DateKey              | DataID              | datetime      | Chave para a data                                   |
| FullDateLabel        | RotuloDataCompleta  | nvarchar      | Rótulo da data completa                             |
| DateDescription      | DescricaoData       | nvarchar      | Descrição da data                                   |
| CalendarYear         | AnoCalendario       | int           | Ano do calendário                                   |
| CalendarYearLabel    | RotuloAnoCalendario | nvarchar      | Rótulo do ano do calendário                         |
| CalendarHalfYear     | SemestreCalendario  | int           | Semestre do calendário                              |
| CalendarHalfYearLabel| RotuloSemestreCalendario | nvarchar | Rótulo do semestre do calendário                    |
| CalendarQuarter      | TrimestreCalendario | int           | Trimestre do calendário                             |
| CalendarQuarterLabel | RotuloTrimestreCalendario | nvarchar | Rótulo do trimestre do calendário                   |
| CalendarMonth        | MesCalendario       | int           | Mês do calendário                                   |
| CalendarMonthLabel   | RotuloMesCalendario | nvarchar      | Rótulo do mês do calendário                         |
| CalendarWeek         | SemanaCalendario    | int           | Semana do calendário                                |
| CalendarWeekLabel    | RotuloSemanaCalendario | nvarchar   | Rótulo da semana do calendário                      |
| CalendarDayOfWeek    | DiaSemanaCalendario | int           | Dia da semana do calendário                         |
| CalendarDayOfWeekLabel | RotuloDiaSemanaCalendario | nvarchar | Rótulo do dia da semana do calendário               |
| FiscalYear           | AnoFiscal           | int           | Ano fiscal                                          |
| FiscalYearLabel      | RotuloAnoFiscal     | nvarchar      | Rótulo do ano fiscal                                |
| FiscalHalfYear       | SemestreFiscal      | int           | Semestre fiscal                                     |
| FiscalHalfYearLabel  | RotuloSemestreFiscal| nvarchar     | Rótulo do semestre fiscal                           |
| FiscalQuarter        | TrimestreFiscal     | int           | Trimestre fiscal                                    |
| FiscalQuarterLabel   | RotuloTrimestreFiscal | nvarchar   | Rótulo do trimestre fiscal                          |
| FiscalMonth          | MesFiscal           | int           | Mês fiscal                                          |
| FiscalMonthLabel     | RotuloMesFiscal     | nvarchar      | Rótulo do mês fiscal                                |
| IsWorkDay            | EDiaUtil            | nvarchar      | Indica se é um dia útil ou não                     |
| IsHoliday            | Eferiado            | int           | Indica se é um feriado (1 para sim, 0 para não)    |
| HolidayName          | NomeFeriado         | nvarchar      | Nome do feriado                                     |
| EuropeSeason         | EstacaoEuropa       | nvarchar      | Estação do ano na Europa                            |
| NorthAmericaSeason   | EstacaoAmericaNorte | nvarchar     | Estação do ano na América do Norte                  |
| AsiaSeason           | EstacaoAsia         | nvarchar      | Estação do ano na Ásia                              |

## Tabela DimStore:

A tabela DimStore contém informações sobre as lojas onde as vendas ocorrem. Aqui estão algumas das variáveis comuns encontradas nesta tabela:

| Variável           | Variável Traduzida  | Tipo de Dados | Descrição                                           |
|--------------------|---------------------|---------------|-----------------------------------------------------|
| StoreKey           | LojaID              | int           | Chave única para cada loja                          |
| GeographyKey       | ChaveGeografica      | int           | Chave para a geografia da loja                      |
| StoreManager       | GerenteLoja         | int           | Gerente da loja                                     |
| StoreType          | TipoLoja            | nvarchar      | Tipo da loja                                        |
| StoreName          | NomeLoja            | nvarchar      | Nome da loja                                        |
| StoreDescription   | DescricaoLoja       | nvarchar      | Descrição da loja                                   |
| Status             | Status              | nvarchar      | Status da loja                                      |
| OpenDate           | DataAbertura        | datetime      | Data de abertura da loja                            |
| CloseDate          | DataFechamento      | datetime      | Data de fechamento da loja                          |
| EntityKey          | ChaveEntidade       | int           | Chave da entidade da loja                           |
| ZipCode            | CodigoPostal                 | nvarchar      | CEP da loja                                         |
| ZipCodeExtension   | ComplementoCodigoPostal      | nvarchar      | Complemento do CEP da loja                          |
| StorePhone         | TelefoneLoja        | nvarchar      | Número de telefone da loja                          |
| StoreFax           | FaxLoja             | nvarchar      | Número de fax da loja                               |
| AddressLine1       | EnderecoLinha1      | nvarchar      | Linha de endereço 1 da loja                         |
| AddressLine2       | EnderecoLinha2      | nvarchar      | Linha de endereço 2 da loja                         |
| CloseReason        | MotivoFechamento    | nvarchar      | Motivo do fechamento da loja                        |
| EmployeeCount      | QuantidadeFuncionarios | int        | Contagem de funcionários da loja                    |
| SellingAreaSize    | TamanhoAreaVendas   | float         | Tamanho da área de vendas da loja                   |
| LastRemodelDate    | DataUltimaRemodelacao | datetime  | Data da última remodelação da loja                  |
| GeoLocation        | GeoLocalizacao | geography | Localização geográfica da loja                      |
| Geometry           | Geometria           | geometry      | Geometria da loja                                   |
| ETLLoadID          | CargaETLID      | int           | Identificador do processo de carga do ETL           |
| LoadDate           | DataCarregamento    | datetime      | Data de carga dos dados                             |
| UpdateDate         | DataAtualizacao     | datetime      | Data de atualização dos dados                       |
