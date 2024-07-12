# Índice

1. [Definição do Problema](#definição-do-problema)
2. [Objetivo](#objetivo)
3. [Observações](#observações)
4. [O Projeto](#o-projeto)
    - [1. Coleta_de_Dados](#1-coleta-de-dados)
    - [2. Plataforma para Execução das Tarefas](#2-plataforma-para-execução-das-tarefas)
    - [3. Formato e Armazenamento](#3-formato-e-armazenamento)
    - [4. Camadas Bronze](#4-camada_bronze)
    - [5. Camadas Prata](#5-camada-prata)
       - [5.1. bairros prata](#51-bairros-prata)
       - [5.2. chamados1746 prata](#52-chamados1746-prata)
       - [5.3. eventoss prata](#53-eventos-prata)
    - [6. Camada Ouro](#6-camada-ouro)
5. [Qualidade dos Dados](#qualidade-dos-dados)
6. [Análises e Resultados](#análises-e-resultados)
7. [ Autoavaliação](#autoavaliação)

## Definição do Problema

O Rio de Janeiro possui uma central de atendimento digital para realização de reclamações referente à cidade. A central 1746
fornece um canal aberto com informações referentes à cada chamado. A fim de melhorar a cidade é necessário observar certas informações
nos dados para a tomada de decisão.

## Objetivo

Esse projeto tem como objetivo criar uma plataforma para análise de dados referente aos chamados à central 1746 do
Janeiro. Essa plataforma inclui à extração dos dados, processamento e visualização de certas informações sobre os dados.
Dessa forma seria possível à tomada de decisão a partir das informações obtidas. As seguintes perguntas foram desenvolvidas
para isso:

- Quais os bairros com maior número de chamados abertos?
- Houve um aumento do número de chamados de 2022 à 2023 relativo a reclamação de pertubação do sossego?
- Há uma diferença significativa no número de chamados de pertubação do sossego em dias de evento (Rock in Rio, Reveillon, Carnaval)?

## Observações

A estrutura do projeto foi divida em camadas Bronze, Prata e Ouro através do desenvolvimento de notebooks.

- Nas camadas bronze são carregados os dados e logo em seguida são salvos.
- Nas camadas prata é feita a limpeza, caso necessário, atualização do schema e transformação dos dados.
- Na camada Ouro são respondias a respectivas perguntas

## O Projeto

### 1. Coleta de Dados

Os dados foram obtidos do site do [DATA.RIO](https://www.data.rio/). Esse site é um portal de dados aberto da prefeitura do Rio
de Janeiro. Nele foram obtidos os dados relativos aos chamados à central 1746 do rio e também uma tabela de eventos do Rio de Janeiro entre os
anos de 2022 e 2023. Optei por baixar os dados em Dados em CSV e adiciona-los a plataforma do databricks para futuras análises.

### 2. Plataforma para Execução das Tarefas

A plataforma escolhida para realização das tarefas de ETL foi o Databricks Community. A escolha dele se deu devido ao uso gratuito da plataforma,
o que é ideal para o aprendizado do MVP sem correr o risco de pagar a mensalidade. Com ele é possível utilizar um micro-cluster para realização de
toda computação e análise de dados em grande escala.

### 3. Carga e Modelagem

Os .csv estão armazenados na pasta data. E exportados para a plataforma do databricks. Nela foi optado por se utilizar a aquitetura Medallion,
onde na camada bronze será feita o armazenamento direto dos dados. Na camada prata será feita a limpeza desses dados. E na última camada os dados
estão prontos para análises de BI.

### 4. Camadas Bronze

Os arquivos notebooks com sufixo bronze presentes no diretório src fazem referência a camada bronze. Nessa camada os arquivos .csv foram lidos e 3 Tabelas
foram criadas, a tabela com [chamados](scr/Chamados1746_Bronze.ipynb) ao 1746(chamados1746_bronze), a tabela com os [bairros](scr/Bairro_Bronze.ipynb) do Rio (bairros_bronze) e a tabela com os [eventos](scr/Eventos_Bronze.ipynb) realizados no período de 2022 à 2023 no Rio de Janeiro.

### 5. Camadas Prata

Os arquivos notebooks com sufixo prata presentes no diretório scr fazem referência a camada prata. Nessa camada as tabelas geradas na camada bronze foram lidas e 3 Tabelas
foram criadas, a tabela com [chamados](scr/Chamados1746_Prata.ipynb)ao 1746(chamados1746_prata), a tabela com os [bairros](scr/Bairro_Prata.ipynb) do Rio (bairros_prata) e a tabela com os 
[eventos](scr/Eventos_Prata.ipynb) realizados no período de 2022 à 2023 no Rio de Janeiro.
Nessas camadas foram realizadas a retirada de dados com o id e data_inicio faltantes e colunas desnecessárias para futuras consultas. Assim como atualização do schema
de cada tabela com os tipagem dos dados corretas. Os schemas de cada tabela estão disponíveis na pasta images e uma tabela representando o mesmo esta disponivel abaixo.

#### 5.1. [bairro_prata](images/schema_bairros.jpeg)

| Coluna        | Tipo   | Descrição                                               |
|---------------|--------|---------------------------------------------------------|
| id_bairro     | string | Código do bairro dado pela prefeitura do Rio de Janeiro.|
| nome          | string | Nome do bairro                                          |
| subprefeitura | string | Nome da subprefeitura a que pertence o bairro.          |

#### 5.2. [chamados1746_prata](images/schema_chamados.jpeg)

| Coluna      | Tipo   | Descrição                                                                                                                              |
|-------------|--------|----------------------------------------------------------------------------------------------------------------------------------------|
| id_chamado  | string | Identificador de cada chamado
| data_inicio | date   | Data de abertura do chamado                                                                                                            |
| data_fim    | date   | Data de fechamento do chamado. O chamado é fechado quando o pedido é atendido ou quando se percebe que o pedido não pode ser atendido. |
| subtipo     | string | Subtipo do chamado                                                                                                                     |
| categoria   | string | Categoria do chamado. Exemplo: Serviço, informação, sugestão, elogio, reclamação, crítica.                                             |
| id_bairro   | string | Identificador único, no banco de dados, do bairro onde ocorreu o fato que gerou o chamado.                                             |

#### 5.3. [eventos_prata](images/schema_eventos.jpeg)

| Coluna       | Tipo   | Descrição                 |
|--------------|--------|---------------------------|
| evento       | string | Nome do evento            |
| data_inicial | date   | Data de inicio do evento  |
| data_final   | date   | Data de termino do evento |


### 6. Camada Ouro

Nessa [camada(Ouro.ipynb)](scr/Ouro.ipynb) foram realizadas as consultas às tabelas da camada prata onde foram respondidas as dúvidas relativas ao objetivo do projeto.

## Qualidade dos Dados

Os dados já possuiam, à priori, uma qualidade relativamente boa, os dados com valores null de identificadores e de data_inicio das tabelas foram retirados.

## Análises e Resultados

Observando às consultas feitas na camada [Ouro](scr/Ouro.ipynb) podemos responder as perguntas feitas no Objetivo do Trabalho. Os seguintes resultados foram obtidos:

- Os bairros com maiores número de reclamações são, respectivemante, Cocapabana, Botafogo e Tijuca.
- O número de chamados abertos de 2022 para 2023 dimunuiram de 31124 para 11706.
- A média diária de reclamações relativo à pertubação do sossego foram maiores em dias de evento. A média em dias de evento é 86.7, enquanto
a média diária normalmente é de 61.9. Mais ou menos 15 reclamações à mais. O que era de se esperar, pois o volume do som produzidos nesses eventos são mais
altos do que em dias comuns.
 
## Autoavaliação

A parte mais desafiadora desse projeto sem dúvida foi como utilizar a plataforma do databricks e o pyspark. Inicialmente minha ideia era conectar o Bigquery
com os dados da prefeitura na plataforma do databricks community, porém não consegui adcionar minhas credênciais de forma efetiva, então optei por baixar os
dados em arquivos csv.

Apesar desses desafios, eu consegui de realizar com sucesso os objetivos traçados no inicio desse projeto de forma satisfatória. 

Uma forma de enriquecer o projeto seria automatizar a inserção de dados direto no databricks sem a necessidade de baixar os arquivos csv. Além disso acredito que a inserção de diferentes tabelas poderiam gerar insights mais valiosos, como seria o caso se fosse adicionado informações sobre violência na cidade. Nesse caso poderiamos fazer uma análise da violência no Rio. 

Ainda a utilização de uma conta paga no databricks poderia deixar o projeto mais automatizado com a utilização de workflows.
