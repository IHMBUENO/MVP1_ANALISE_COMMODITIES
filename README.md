# MVP1_ANALISE_COMMODITIES

## **INTRODUÇÃO** 

#### As commodities são mercadorias primárias produzidas em larga escala que fornecem matéria prima para diferentes setores da sociedade, sendo que essas mercadorias têm grande importância econômica e estratégica em razão da sua utilização por diversos agentes.
#### O Brasil é um grande exportador de Soft commodities, que são produtos agropecuários que podem ser consumidos ou usados como matéria-prima, temos como exemplos: Soja, milho, açúcar, trigo, café e carne. O Brasil lidera a posição global na exportação de soja e carne bovina, sendo que o milho, café e carne suína possuem grande representatividade na economia.

## **DESCRIÇÃO DO PROBLEMA**

#### Sabendo da grande representatividade das commodities agrícolas na economia brasileira detectar quando e quanto foi o preço do máximo e o mínimo de cada uma das commodities representa uma grande oportunidade para a venda e compra destes ativos.

## **PERGUNTAS A SEREM RESPONDIDAS**

#### •	Quando e qual foi a máxima do preço de fechamento médio mensal para as commodities boi gordo, porco magro, soja e milho entre janeiro de 2010 e julho de 2023? 
#### •	Quando e qual foi a mínima do preço de fechamento médio mensal para as commodities boi gordo, porco magro, soja e milho entre janeiro de 2010 e julho de 2023?  
#### •	Existe correlação entre as commodities boi gordo, porco magro, soja e milho?
#### •	É possível detectar alguma tendência ou sazonalidade de forma gráfica nos ativos boi gordo, porco magro, soja e milho.

## **METODOLOGIA**
### **DOWNLOAD DOS DADOS**

#### Os dados foram retirados da fonte abaixo, onde a base de dados constituí a grande maioria das commodities negociadas mundialmente, sendo que seus valores estão expressos em dólar americano.

FIGURA 1: Local de extração dos dados.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/26469f79-f374-4a64-898c-1d5e2547fdb5)

Fonte: https://www.kaggle.com/datasets/guillemservera/commodities-futures-collection

### **PLATAFORMA UTILIZADA**

#### Para a realização do job foi utilizado a plataforma de serviços de computação em nuvem da fornecida pela Amazon, também conhecida como AWS (Amazon Web Services).
### **CRIAÇÃO DO BUCKET NO AMAZON S3**

#### O Amazon Simple Storage Service (Amazon S3) é um serviço de armazenamento de objetos que armazena dados como objetos em buckets. Um objeto é um arquivo e quaisquer metadados que descrevam o arquivo. Um bucket é um contêiner de objetos.
#### Para armazenar seus dados no Amazon S3, crie um bucket e especifique um nome de bucket e a Região da AWS. Em seguida, carregue seus dados para esse bucket como objetos no Amazon S3. Cada objeto tem uma chave (ou nome de chave), que é um identificador exclusivo do objeto no bucket.
#### Nas imagens abaixo a demonstração da criação do bucket e upload do arquivo em CSV.

FIGURA 2: Criação do Bucket.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/3bfb2cac-ac37-484f-9745-e22373e6732b)

 
FIGURA 3: Criação da Pasta e upload do arquivo.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/2ed598c7-61d9-4cda-9713-12241e09cab2)

 
FIGURA 4: Arquivo Armazenado.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/7c91abf6-2bc3-42a3-b9c4-6072194721d8)

### **ETL NO AMAZON GLUE**
#### O AWS Glue Studio é uma interface gráfica que facilita a criação, a execução e o monitoramento de trabalhos de integração de dados no AWS Glue. Você pode compor visualmente fluxos de trabalho de transformação de dados e executá-los perfeitamente no mecanismo de ETL com tecnologia sem servidor baseado no Apache Spark do AWS Glue.
#### Abaixo imagens que demonstram a seleção e ETL dos dados utilizados:

FIGURA 5: Importação dos dados do Amazon S3 para o Amazon Glue.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/1ab26dd1-aac7-47d5-b39e-fc5249aefe15)

#### Os dados utilizados possuem 9 colunas: Ticker, commodities, category, date, open, high, low, close e volume, sendo que os dados são informações diárias do preço das commodities do dia 04/03/2002 a 04/09/2023.
#### Para responder as nossas perguntas podemos excluir as colunas ticker, open, high e low, selecionando-as nas flags do drop a direita.

FIGURA 6. Realização do Drop nas colunas que não iremos utilizar.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/f51b4957-2a75-4458-b45a-56b317e85a2e)

### HABILITANDO O AMAZON REDSHIFT

#### Para usar clusters do Amazon Redshift noAWS Glue, você precisará de alguns pré-requisitos:
#### •	Um diretório do Amazon S3 a ser usado para armazenamento temporário ao ler e gravar no banco de dados. AWS O Glue move dados por meio do Amazon S3 para atingir a taxa de transferência máxima, usando o SQLCOPY eUNLOAD os comandos do Amazon Redshift.
#### •	Um Amazon VPC que permite a comunicação entre seu cluster Amazon Redshift, seu trabalhoAWS Glue e seu diretório Amazon S3.
#### •	Permissões apropriadas do IAM no trabalhoAWS Glue e no cluster Amazon Redshift.
#### Abaixo um passo a passo com as imagens para gerar os clusters.

FIGURA 7: Configurações iniciais.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/82b9ae62-f376-4396-a127-c2eb6ac1a0d9)

FIGURA 8: Painel inicial do Amazon Redshift.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/c598fab2-1cfd-4ea4-8e5b-042cc8de97c6)

#### Como não há conexão é necessário que se crie para conectar diferentes base de dados dentro do seu Glue.

FIGURA 9, 10, 11, 12, 13, 14, 15 e 16: Passo a passo para a criação da conexão.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/2abba68a-6e43-468e-9664-b6c6c673459b)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/2c0ebc43-93dc-40eb-b0e9-821271cbb859)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/380d6cf7-fdf4-4042-9809-b8808c85ad3a)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/28eed67d-b0ad-4a52-99de-7f9a714f2660)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/de8e3b73-635c-44d1-88be-678c0bd9d705)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/c7b02ddc-5079-439f-b15c-13ed80a3e958)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/87b6e4da-675e-4c64-89b2-e8b79629e1e0)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/9feec4b6-fc55-45d7-a1f0-02bfa8f4360f)

FIGURA 17: Conexão com a VPC Padrão

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/67b26aec-493d-42f1-85be-0120c0d40699)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/6e159094-6c6b-40f4-94c1-23a0dbb3aa87)

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/58f9d2a1-b360-4ecd-abc2-1ed909a7cd80)

FIGURA 18: Testando a conexão

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/c18eb452-c4e3-496f-8c13-1c676e76b4fd)

FIGURA 19: Confirmação da conexão no Amazon Glue. É necessário que tenha a flag verde no data target.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/f41f94f2-1135-4cd9-886f-f84e06c30ac0)

FIGURA 20: Será criado um script em python com os passos realizados. É necessário dar o run para o funcionamento do job.

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/71ab42b0-f3c0-4173-afb4-00e38ca95298)

### CRIAÇÃO DA TABELA E AGRUPAMENTO DOS DADOS NO AMAZON REDSHIFT

``` ---------------------------------------- SCRIPT MVP 1
create table public.all_commodities_futures_collection (commodity varchar, category varchar, data date, close DECIMAL(10,2), volume DECIMAL(10,2))
	
-- Visualizando Tabela
select * from all_commodities_futures_collection

-- Filtrando, Agrupando e Ordenando os dados
CREATE TABLE data_project AS SELECT 
commodity, 
category, 
DATE_PART_YEAR(data),
DATE_PART(month, data), 
AVG(close) AS mean,
SUM(volume) AS vol
FROM all_commodities_futures_collection
WHERE
(commodity LIKE ('Lean Hogs') OR commodity LIKE ('Live Cattle') OR commodity LIKE ('Corn') OR commodity LIKE ('Soybean')) AND
(data BETWEEN '2010-01-01' AND '2023-07-31')
GROUP BY (commodity, category, DATE_PART_YEAR(data), date_part(month, data))
ORDER BY date_part_year, pgdate_part;

ALTER TABLE data_project

ADD COLUMN month_year VARCHAR
DEFAULT NULL;
	
---- Preecher coluna
	
UPDATE data_project 
SET month_year = number_month || '-' || number_year;
	
select*from data_project
-- Renomeando colunas
ALTER TABLE data_project
RENAME COLUMN pgdate_part TO number_month;

ALTER TABLE data_project
RENAME COLUMN date_part_year TO number_year;

SELECT*FROM data_project
ORDER BY number_year, number_month, commodity;
```

## RESULTADOS

### VALORES MÁXIMOS E DATA DAS COMMODITIES

```
-- Valor Máximo Mensal Médio

select 
    dp2.commodity, 
    dp2.category, 
    dp.month_year, 
    dp2.max_media 
from data_project dp
Join (
    select 
        commodity, 
        category, 
        max(media) as max_media 
    from data_project
    Group by 1,2) dp2   on dp.commodity = dp2.commodity 
                        and dp.category = dp2.category 
                        and dp.media = dp2.max_media
```

![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/771674ac-8e3a-40c6-b6e4-22193164e66a)

```
-- Valor Mínimo Mensal Médio

select 
    dp2.commodity, 
    dp2.category, 
    dp.month_year, 
    dp2.min_media 
from data_project dp
Join (
    select 
        commodity, 
        category, 
        min(media) as min_media 
    from data_project
    Group by 1,2) dp2   on dp.commodity = dp2.commodity 
                        and dp.category = dp2.category 
                        and dp.media = dp2.min_media
```
![image](https://github.com/IHMBUENO/MVP1_ANALISE_COMMODITIES/assets/145625092/43aed7f5-d3e2-4598-8572-ac905cb7dbde)
























 







