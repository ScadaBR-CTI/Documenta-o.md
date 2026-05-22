# Documentação do Sistema

## 1. Contexto do Sistema

O ScadaBR-CTI é uma solução de monitoramento e análise de dados operacionais baseada em dados provenientes do sistema supervisório ScadaBR. O sistema foi desenvolvido para suportar análise histórica de variáveis operacionais, com foco em eficiência energética, desempenho de infraestrutura e suporte à tomada de decisão técnica.

### 1.1 Hierarquia de Distribuição

Para entender como os dados são coletados, é fundamental visualizar a topologia elétrica do CTI Renato Archer. O diagrama abaixo representa o fluxo de energia, desde a entrada pelo Sistema Interligado Nacional e concessionária (CPFL), passando pelos transformadores e geradores, até chegar às cargas críticas.

Este mapeamento é o que permite ao ScadaBR-CTI:

* Rastrear perdas: Identificar em qual estágio da distribuição ocorre maior consumo ou desperdício.

* Setorizar o consumo: Separar o que é gasto com infraestrutura básica (iluminação/tomadas) do que é consumo de processos críticos (Chillers, Nobreaks, Salas Limpas e Impressoras 3D).

* Gerir Contingências: Monitorar a entrada dos geradores e a saúde dos sistemas de backup em tempo real.

<p align="center">
  <img src="img/Daigrama de Blocos.jpeg" alt="Fluxograma ScadaBR CTI" width="100%">
</p>

---

## 2. Objetivo Técnico

O sistema tem como objetivo principal a transformação de dados operacionais brutos em indicadores estruturados, permitindo:

* Monitoramento temporal de variáveis energéticas e operacionais
* Análise de séries temporais de consumo e carga
* Avaliação de desempenho de equipamentos e sistemas
* Identificação de padrões sazonais e comportamentais
* Suporte à detecção de anomalias operacionais
* Geração de indicadores para eficiência energética

---

## 3. Arquitetura do Sistema

A arquitetura é composta por três camadas funcionais:

### 3.1 Camada de Aquisição de Dados

Dados são coletados via sistema ScadaBR, responsável pela leitura de sensores e dispositivos em campo, operando como interface entre o ambiente físico e o sistema de informação.

### 3.2 Camada de Armazenamento

Os dados são armazenados em banco de dados, estruturados em séries temporais e tabelas normalizadas, permitindo consultas históricas e agregações por diferentes granularidades temporais.

### 3.3 Camada de Processamento e Visualização

O processamento é realizado em R, com pipeline de transformação, limpeza e agregação dos dados. A visualização é implementada via Shiny, com suporte a gráficos dinâmicos e consultas interativas.

---

## 4. Fluxo de Dados

O *pipeline* de dados segue a seguinte sequência:

* Aquisição de sinais via ScadaBR
* Registro dos dados em banco relacional
* Extração via *queries* SQL em R
* Pré-processamento (limpeza, normalização e tratamento de *missing data*)
* Geração de indicadores operacionais
* Visualização via dashboard interativo

### Fluxograma do sistema

  <p align="center">
  <img src="img/Fluxo_Geral.png" alt="Fluxo Geral" width="90%">
  </p>

---

## 5. Modelagem Analítica

O sistema opera principalmente sobre séries temporais estruturadas, permitindo:

* Agregações por minuto, hora, dia e semana
* Comparações interperíodo
* Análise de tendência e sazonalidade
* Segmentação por pontos de medição
* Correlação entre variáveis operacionais

---

## 6. Indicadores Derivados

A partir do processamento das séries temporais e das análises realizadas sobre os dados operacionais e energéticos, o sistema gera indicadores consolidados para suporte ao monitoramento e avaliação de desempenho da infraestrutura monitorada.

Entre os principais indicadores derivados implementados, destacam-se:

* Consumo energético agregado por período operacional
* Consumo segmentado por ponto de medição
* Perfil de carga ao longo do dia, semana e horários de pico
* Média, máximos e mínimos de consumo por intervalo temporal
* Comparação entre períodos distintos para identificação de anomalias e mudanças de comportamento
* Indicadores de tendência e sazonalidade das variáveis monitoradas

Os indicadores são processados na camada analítica em linguagem R, utilizando consultas ao banco de dados MySQL e rotinas de agregação temporal, sendo posteriormente disponibilizados no dashboard interativo desenvolvido em Shiny.

---
  
## 7. Tecnológias Empregadas

* **ScadaBR:** Sistema supervisório (interface)
* **MySQL:** banco de dados (armazenamento de dados)
* **R / RStudio:** Linguagem de programação (manipulação de dados e análise estatística)

---

## 8 Bibliotecas
  
- **shiny:** É o motor principal; permite criar aplicativos web interativos usando apenas a linguagem R.

- **shinythemes:** Fornece "temas" visuais prontos para mudar as cores e fontes do dashboard com um clique.

### 8.1 Conexão e Banco de Dados

- **DBI:** Funciona como uma interface padrão para comunicação entre o R e diversos sistemas de bancos de dados.

- **RMySQL:** É o driver específico que permite ao R "falar" com o banco de dados MySQL/MariaDB do seu projeto.

### 8.2 Manipulação e Limpeza de Dados

- **dplyr:** Ferramenta essencial para manipular dados (filtrar linhas, selecionar colunas, agrupar e realizar cálculos).

- **tidyr:** Serve para organizar dados "bagunçados", permitindo remodelar tabelas (ex: transformar colunas em linhas).

### 8.3 Gestão de Tempo e Datas

- **lubridate:** Facilita a leitura e operações matemáticas com datas (ex: somar dias ou extrair o mês de um timestamp).

- **hms:** Biblioteca especializada em tratar variáveis que contêm apenas Horas, Minutos e Segundos.

### 8.4 Gráficos e Visualização

- **ggplot2:** A ferramenta mais poderosa para criar gráficos estáticos e customizados (barras, linhas, dispersão).

- **plotly:** Transforma os gráficos do ggplot2 em versões interativas (com zoom e leitura de valores ao passar o mouse).

### 8.5 Tabelas Interativas

- **DT:** Permite exibir tabelas no dashboard com recursos de busca, paginação e ordenação automática.

---

## 9. Integração com o Repositório

Este repositório centraliza:

* Modelos de análise em R
* Documentação técnica do pipeline

---

## 10. Conclusão

O sistema apresentado integra de forma estruturada a análise de dados energéticos, desde a aquisição em campo via medidores e sistema SCADA até a disponibilização das informações em um ambiente analítico interativo.

A arquitetura proposta garante confiabilidade no fluxo de dados por meio de etapas de validação, tratamento e padronização, assegurando que apenas informações consistentes sejam utilizadas no processamento. Além disso, a separação entre camadas de coleta, armazenamento, processamento e visualização contribui para maior organização, escalabilidade e facilidade de manutenção do sistema.

A incorporação de análises estatísticas e indicadores energéticos permite a identificação de padrões de consumo e possíveis anomalias operacionais, apoiando a tomada de decisão orientada à eficiência energética.

Dessa forma, a solução não apenas centraliza e organiza os dados, mas também os transforma em informação útil para suporte à gestão e otimização de recursos energéticos no ambiente do CTI.

---

- **[Página Inicial](https://github.com/ScadaBR-CTI)**
