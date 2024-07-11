# Índice

1. [Definição do Problema](#definição-do-problema)
2. [Objetivo](#objetivo)
3. [Observações](#observações)
4. [O Projeto](#o-projeto)
    - [1. Coleta_de_Dados](#1-coleta-de-dados)
    - [2. Plataforma para Execução das Tarefas](#2-plataforma-para-execução-das-tarefas)
    - [3. Formato e Armazenamento](#3-formato-e-armazenamento)
    - [4. Camadas Bronze](#4-catálogo-de-dados-da-camada-bronze)
        - [6.1. age](#61-age)
        - [6.2. home_away](#62-home_away)
        - [6.3. price](#63-price)
        - [6.4. round](#64-round)
    - [5. Camadas Prata](#5-transformações-para-a-camada-silver)
        - [7.1. age](#71-age)
        - [7.2. home_away](#72-home_away)
        - [7.3. price](#73-price)
        - [7.4. round](#74-round)
    - [8. Camada Ouro](#7-transformações-para-a-camada-silver)
- [5. Qualidade dos Dados](#qualidade-dos-dados)
- [6. Análises e Insights](#análises-e-insights)
  - [6.1. Qual a pontuação média para escapar do rebaixamento nos últimos anos?](#61-qual-a-pontuação-média-para-escapar-do-rebaixamento-nos-últimos-anos)
  - [6.2. O quão desesperador é a situação atual do Fluminense?](#62-o-quão-desesperador-é-a-situacao-atual-do-fluminense)
  - [6.3. A idade média dos jogadores influencia no desempenho dos clubes?](#63-a-idade-média-dos-jogadores-influencia-no-desempenho-dos-clubes)
  - [6.4. O valor de mercado dos clubes está relacionado com a sua classificação no campeonato?](#64-o-valor-de-mercado-dos-clubes-está-relacionado-com-a-sua-classificação-no-campeonato)
- [7. Autoavaliação](#autoavaliação)

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

A estrutura do projeto foi divida em camadas Bronze, Prata e Ouro

- Nas camadas bronze são carregados os dados e logo em seguida são  salvos.
- Nas camadas prata é feita a limpeza, caso necessário, atualização do schema e transformação dos dados.
- Na camada Ouro são respondias a respectivas perguntas

## O Projeto

### 1. Coleta de Dados

### 2. Plataforma para Execução das Tarefas

### 3. Armazenamento

### 4. Camadas Bronze

### 5. Camadas Prata

### 6. Camada Ouro

### 7. Qualidade dos Dados

### 8. Insights
