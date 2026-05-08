#Visão Geral do Sistema

##1. Contexto do Sistema

O ScadaBR-CTI é uma solução de monitoramento e análise de dados operacionais baseada em dados provenientes do sistema supervisório ScadaBR. O sistema foi desenvolvido para suportar análise histórica de variáveis operacionais, com foco em eficiência energética, desempenho de infraestrutura e suporte à tomada de decisão técnica.

A arquitetura integra coleta, persistência e processamento de dados estruturados, permitindo exploração analítica em ambiente R.

##2. Objetivo Técnico

O sistema tem como objetivo principal a transformação de dados operacionais brutos em indicadores analíticos estruturados, permitindo:

Monitoramento temporal de variáveis energéticas e operacionais
Análise de séries temporais de consumo e carga
Avaliação de desempenho de equipamentos e sistemas
Identificação de padrões sazonais e comportamentais
Suporte à detecção de anomalias operacionais
Geração de indicadores para eficiência energética

##3. Arquitetura do Sistema

A arquitetura é composta por três camadas funcionais:

###3.1 Camada de Aquisição de Dados

Dados são coletados via sistema ScadaBR, responsável pela leitura de sensores e dispositivos em campo, operando como interface entre o ambiente físico e o sistema de informação.

###3.2 Camada de Persistência

Os dados são armazenados em banco de dados relacional, estruturados em séries temporais e tabelas normalizadas, permitindo consultas históricas e agregações por diferentes granularidades temporais.

###3.3 Camada de Processamento e Visualização

O processamento é realizado em R, com pipeline de transformação, limpeza e agregação dos dados. A visualização é implementada via Shiny, com suporte a gráficos dinâmicos e consultas interativas.

##4. Fluxo de Dados

O pipeline de dados segue a seguinte sequência:

Aquisição de sinais via ScadaBR
Registro dos dados em banco relacional
Extração via queries SQL em R
Pré-processamento (limpeza, normalização e tratamento de missing data)
Agregação temporal e construção de métricas
Geração de indicadores operacionais
Visualização via dashboard interativo
5. Modelagem Analítica

O sistema opera principalmente sobre séries temporais estruturadas, permitindo:

Agregações por minuto, hora, dia e semana
Comparações interperíodo (baseline vs atual)
Análise de tendência e sazonalidade
Segmentação por pontos de medição
Correlação entre variáveis operacionais
6. Indicadores Derivados

Os principais indicadores gerados incluem:

Consumo energético agregado e segmentado
Perfil de carga por período operacional
Fator de utilização de equipamentos
Variabilidade de consumo (desvio e dispersão)
Eficiência relativa entre unidades monitoradas
7. Stack Tecnológico
ScadaBR (aquisição e supervisão industrial)
MySQL / banco relacional (persistência de dados)
R (data wrangling e análise estatística)
tidyverse (transformação de dados)
lubridate (tratamento temporal)
ggplot2 / plotly (visualização)
Shiny (interface analítica interativa)
8. Integração com o Repositório

Este repositório centraliza:

Scripts de extração e tratamento de dados
Modelos de análise em R
Dashboards interativos
Documentação técnica do pipeline
Estrutura do banco de dados e consultas

## Diagrama de Blocos
<p align="center">
  <img src="img/Daigrama de Blocos.jpeg" alt="Fluxograma ScadaBR CTI" width="100%">
</p>
