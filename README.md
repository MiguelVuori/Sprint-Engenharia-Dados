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

### 3. Armazenamento

Os .csv estão armazenados na pasta data. E exportados para a plataforma do databricks.

### 4. Camadas Bronze

Os arquivos notebooks com sufixo bronze presentes no diretório scr fazem referência a camada bronze. Nessa camada os arquivos .csv foram lidos e 2 Tabelas
foram criadas, a tabela com chamados ao 1746(chamados1746_bronze) e a tabela com os eventos(eventos_bronze) realizados no período de 2022 à 2023 no Rio de Janeiro.

### 5. Camadas Prata

Os arquivos notebooks com sufixo prata presentes no diretório scr fazem referência a camada prata. Nessa camada as tabelas geradas na camada bronze foram lidas e 2 Tabelas
foram criadas, a tabela com chamados ao 1746(chamados1746_prata) e a tabela com os eventos(eventos_prata) realizados no período de 2022 à 2023 no Rio de Janeiro.
Nessas camadas foram realizadas a retirada de dados com o id e data_inicio faltantes, colunas essas que serão utilizas em consultas posteriores. 


### 6. Camada Ouro

Nessa camada(Ouro.ipynb) foram realizadas as consultas às tabelas da camada prata onde foram respondidas as dúvidas relativas ao objetivo do projeto.

## Qualidade dos Dados

Os dados já possuiam, à priori, uma qualidade relativamente boa, os dados com valores null de identificadores e de data_inicio dos chamados foram retirados.

## Análise e Resultados

Observando às consultas feitas na camada Ouro podemos responder as perguntas feitas no Objetivo do Trabalho. Os seguintes resultados foram obtidos:

- 
- A média diária de reclamações relativo à pertubação do sossego foram maiores em dias de evento. A média em dias de evento é 86.7, enquanto
a média diária normalmente é de 61.9. Mais ou menos 15 reclamações à mais. O que era de se esperar, pois o volume do som produzidos nesses eventos são mais
altos do que em dias comuns.
 
## Autoavaliação

A parte mais desafiadora desse projeto sem dúvida foi como utilizar a plataforma do databricks e o pyspark. Inicialmente minha ideia era conectar o Bigquery
com os dados da prefeitura na plataforma do databricks community, porém não consegui adcionar minhas credênciais de forma efetiva, então optei por baixar os
dados em arquivos csv.

Uma forma de enriquecer o projeto seria automatizar essa inserção de dados direto no databricks sem a necessidade de baixar os arquivos csv. Além disso acredito que a inserção de diferentes tabelas poderiam gerar insights mais valiosos, como seria o caso se fosse adicionado informações sobre os bairros no Rio de Janeiro. 

Ainda a utilização de uma conta paga no databricks poderia deixar o projeto mais automatizado com a utilização de workflows.
