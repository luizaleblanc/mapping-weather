Climate Mapping 🌎

Plataforma de visualização e análise de dados climáticos com Inteligência Artificial

1. Visão Geral do Projeto

O Climate Mapping é uma plataforma web interativa que tem como objetivo apresentar, visualizar e interpretar dados climáticos de diferentes regiões do planeta, auxiliando na compreensão das mudanças climáticas e de seus possíveis efeitos ao longo do tempo.

A aplicação utilizará fontes de dados climáticos e geográficos para apresentar informações de países do mundo inteiro e oferecer uma análise mais detalhada dos estados brasileiros.

Por meio de um globo terrestre interativo, o usuário poderá selecionar um país e visualizar indicadores climáticos históricos. Ao selecionar o Brasil, será disponibilizada uma visualização específica de suas unidades federativas, permitindo a exploração e comparação dos dados entre os estados.

O projeto também contará com integração de Inteligência Artificial (IA), responsável por interpretar os dados apresentados, explicar tendências observadas e permitir comparações entre diferentes territórios e períodos.

O desenvolvimento será organizado em quatro fases: Arquitetura do Sistema, Discovery de Negócio, Desenvolvimento e Testes e Definição do MVP.

⸻

FASE 1: Arquitetura do Sistema (Design e Planejamento)

Nesta fase serão definidas as tecnologias, fontes de dados, estrutura da aplicação e estratégias de integração necessárias para o desenvolvimento.

1.1. Arquitetura Geral

O sistema será desenvolvido inicialmente como uma aplicação web utilizando React, com arquitetura Single Page Application (SPA).

A aplicação será organizada em três áreas principais:

1. Camada de Apresentação: responsável pela interface, navegação, mapas interativos, gráficos e componentes visuais.
2. Camada de Integração: responsável pelo consumo das APIs externas e organização dos dados recebidos.
3. Camada de Análise e Inteligência Artificial: responsável pela interpretação dos indicadores climáticos, comparação de dados e geração de explicações em linguagem natural.

A necessidade de um backend e a estratégia de processamento e armazenamento dos dados geográficos serão avaliadas durante o planejamento técnico, considerando a complexidade dos cálculos territoriais e as necessidades de integração com a IA.

1.2. Fontes de Dados e Integrações

O projeto utilizará fontes de dados climáticos e geográficos, cada uma com uma responsabilidade específica.

Dados climáticos

Open-Meteo (Historical Weather API - ERA5)

* Fonte principal candidata para obtenção de dados meteorológicos históricos em escala global.
* Consulta de variáveis como temperatura média, temperatura máxima e precipitação.
* Utilização de dados históricos para comparação e identificação de tendências climáticas.
* Possibilidade de consultas por coordenadas geográficas.

Documentação: https://open-meteo.com/en/docs/historical-weather-api

NASA POWER (alternativa ou fonte complementar)

* Fonte de dados meteorológicos e ambientais disponibilizados pela NASA.
* Possibilidade de obtenção de informações históricas de temperatura e precipitação.
* Será considerada para comparação e validação da disponibilidade dos dados.

Documentação: https://power.larc.nasa.gov/docs/

A escolha definitiva da fonte climática principal dependerá de testes de disponibilidade, cobertura territorial, resolução espacial e compatibilidade dos dados.

Dados geográficos

Natural Earth

* Fornecimento de dados geográficos e limites territoriais dos países.
* Utilização dos polígonos para identificação e seleção dos países no globo interativo.

Site: https://www.naturalearthdata.com/

IBGE - Malhas Territoriais

* Fornecimento dos limites geográficos dos estados brasileiros.
* Utilização dos polígonos das unidades federativas para a construção do mapa detalhado do Brasil.
* Apoio à identificação das áreas utilizadas na agregação territorial dos dados climáticos.

Site: https://www.ibge.gov.br/geociencias/organizacao-do-territorio/malhas-territoriais.html

O IBGE será utilizado como fonte geográfica, não como fonte principal de informações meteorológicas.

Inteligência Artificial

API de Inteligência Artificial (provedor a definir)

Responsável por interpretar os indicadores climáticos processados pela aplicação e produzir explicações em linguagem natural.

As possibilidades incluem:

* Interpretação dos indicadores de um país ou estado.
* Comparação entre diferentes territórios.
* Explicação das variações observadas ao longo do período histórico.
* Respostas a perguntas relacionadas aos dados apresentados.

A IA deverá utilizar os resultados efetivamente obtidos pela aplicação, evitando gerar informações ou conclusões sem respaldo nos dados.

1.3. Tecnologias e Bibliotecas

Tecnologias inicialmente previstas:

* React + Vite: desenvolvimento da aplicação frontend.
* Globe.gl: construção do globo terrestre 3D interativo.
* MapLibre ou solução equivalente: possibilidade de utilização na visualização detalhada dos estados brasileiros.
* Recharts ou Chart.js: construção dos gráficos e visualizações estatísticas.
* GeoJSON: representação dos limites geográficos dos países e estados.
* Open-Meteo: obtenção dos dados climáticos históricos.
* API de IA: interpretação dos dados e geração de respostas.

As tecnologias poderão ser ajustadas conforme os testes de viabilidade e as necessidades de implementação.

1.4. Metodologia de Análise dos Dados

O projeto terá como foco a análise territorial dos dados climáticos.

Em vez de utilizar apenas uma coordenada representativa de cada país ou estado, a proposta é calcular indicadores considerando a extensão geográfica de cada território.

Para isso, serão utilizados os limites territoriais e os dados climáticos disponíveis em grades geográficas.

O processamento deverá considerar os pontos ou células que representam cada território, buscando produzir médias espaciais representativas de sua área.

Essa metodologia será aplicada:

* Aos países do mundo inteiro.
* Aos estados brasileiros, incluindo o Distrito Federal.

A resolução espacial das fontes utilizadas e a disponibilidade de dados para territórios menores serão consideradas durante a implementação.

Período histórico

O período inicial de análise será de 30 anos, entre 1996 e 2025.

A escolha permite trabalhar com uma janela histórica uniforme e utilizar um período de referência climatológica reconhecido internacionalmente.

A aplicação deverá permitir a visualização da evolução dos indicadores durante esse intervalo.

Indicadores climáticos iniciais

O sistema trabalhará inicialmente com três indicadores:

1. Temperatura média: acompanhamento da evolução das temperaturas médias ao longo dos anos.
2. Temperatura máxima: observação das temperaturas máximas médias e de suas variações.
3. Precipitação: análise do volume de chuvas e das alterações nos padrões de precipitação.

A periodicidade das visualizações (anual, mensal ou ambas) será definida durante o planejamento dos gráficos.

Anomalias de temperatura

Será considerada a possibilidade de apresentar anomalias térmicas, identificando diferenças entre as temperaturas observadas e uma média de referência.

A metodologia de cálculo e o período de referência específico serão definidos durante a implementação.

⸻

FASE 2: Discovery de Negócio (Requisitos)

Nesta fase serão definidos os requisitos funcionais e a experiência que a aplicação deverá oferecer aos usuários.

2.1. AS IS vs TO BE

AS IS:

A consulta e comparação de informações climáticas exige a utilização de diferentes fontes de dados, dificultando a visualização conjunta de tendências históricas e diferenças entre regiões.

TO BE:

O usuário acessa uma plataforma centralizada que reúne dados climáticos históricos, apresenta informações por meio de mapas e gráficos interativos e utiliza Inteligência Artificial para facilitar a interpretação dos indicadores.

2.2. Funcionalidades Principais

Feature A - Globo Interativo

* Apresentação de um globo terrestre 3D na página inicial.
* Possibilidade de girar, aproximar e afastar a visualização.
* Seleção de países diretamente no globo.
* Identificação do território selecionado.
* Navegação para a área de análise correspondente.

Feature B - Análise Mundial por Países

Ao selecionar um país, o usuário terá acesso a um painel com:

* Identificação do país selecionado.
* Temperatura média histórica.
* Temperatura máxima.
* Precipitação.
* Gráficos de evolução dos indicadores.
* Comparação entre períodos históricos.
* Interpretação dos dados pela Inteligência Artificial.

A análise mundial será apresentada em nível nacional, utilizando a média territorial dos dados disponíveis.

Feature C - Análise Detalhada do Brasil

Ao selecionar o Brasil no globo, a aplicação disponibilizará uma visualização específica das unidades federativas.

Funcionalidades previstas:

* Mapa interativo dos estados brasileiros.
* Seleção individual de cada estado.
* Visualização dos indicadores climáticos estaduais.
* Gráficos históricos.
* Comparação entre diferentes estados.
* Comparação com indicadores nacionais.
* Interpretação dos dados pela Inteligência Artificial.

Feature D - Dashboard Climático

Apresentação organizada dos indicadores por meio de:

* Cards informativos.
* Gráficos históricos.
* Mapas com representação visual dos indicadores.
* Filtros de território e período.
* Comparações entre diferentes regiões.

Feature E - Climate AI

Integração com Inteligência Artificial para interpretação dos dados climáticos.

Funcionalidades previstas:

1. Análise individual: interpretação dos indicadores de um país ou estado selecionado.
2. Comparação territorial: comparação dos indicadores entre dois ou mais territórios.
3. Análise histórica: explicação das tendências identificadas durante o período analisado.
4. Chatbot climático: possibilidade de realizar perguntas sobre os dados apresentados.

A IA deverá contextualizar os resultados e explicar suas limitações, sem atribuir automaticamente eventos climáticos específicos ao aquecimento global.

⸻

FASE 3: Desenvolvimento e Testes

Nesta fase as funcionalidades serão divididas em tarefas menores, permitindo o desenvolvimento organizado e a validação contínua do sistema.

3.1. Requisitos de Qualidade

Definition of Ready (DoR)

Uma tarefa estará pronta para desenvolvimento quando:

* Possuir descrição clara da funcionalidade.
* Apresentar critérios de aceitação.
* Ter suas dependências identificadas.
* Possuir protótipo ou referência visual, quando necessário.
* Ter sua implementação compreendida pela equipe.

Definition of Done (DoD)

Uma funcionalidade será considerada concluída quando:

* Estiver implementada e integrada à aplicação.
* Apresentar comportamento responsivo.
* Possuir tratamento de carregamento, erros e ausência de dados.
* Não apresentar erros relevantes no console.
* Passar pelos testes definidos para a funcionalidade.
* Ter seu código revisado pela equipe.

3.2. Testes

Serão realizados testes para verificar:

* Funcionamento da navegação entre países e estados.
* Seleção correta dos territórios no mapa.
* Consumo e tratamento das APIs.
* Consistência dos indicadores calculados.
* Renderização correta dos gráficos.
* Funcionamento da integração com a IA.
* Tratamento de falhas nas fontes de dados.
* Responsividade da interface em diferentes dispositivos.

⸻

FASE 4: Definição do MVP (Produto Mínimo Viável)

O desenvolvimento será dividido em duas entregas principais, permitindo construir e validar a aplicação progressivamente.

MVP 1 - Análise Climática Mundial

Desenvolvimento da estrutura principal da aplicação.

Funcionalidades:

* Interface inicial responsiva.
* Globo terrestre 3D interativo.
* Seleção de países.
* Consulta e apresentação dos indicadores climáticos históricos.
* Visualização de temperatura média, temperatura máxima e precipitação.
* Gráficos históricos.
* Primeira integração com Inteligência Artificial para interpretação dos dados.

O objetivo é validar a experiência de navegação e a apresentação das informações climáticas mundiais.

MVP 2 - Análise Brasileira e Recursos Avançados

Expansão das funcionalidades da aplicação.

Funcionalidades:

* Mapa interativo dos estados brasileiros.
* Seleção individual das unidades federativas.
* Apresentação dos indicadores estaduais.
* Comparação entre estados e regiões.
* Aprimoramento dos gráficos e filtros temporais.
* Comparações entre territórios.
* Expansão da integração com IA.
* Implementação do chatbot climático.

O objetivo é aprofundar a análise territorial brasileira e ampliar as possibilidades de interação com os dados.

⸻

Guia Inicial de Implementação

1. Inicialização do Projeto

Será utilizado o Vite para criação e configuração inicial da aplicação React.

npm create vite@latest climate-mapping -- --template react
cd climate-mapping
npm install
npm run dev

2. Estrutura de Pastas Sugerida

A estrutura inicial poderá seguir a organização abaixo:

src/
├── assets/
│   ├── images/
│   └── maps/
│
├── components/
│   ├── Globe/
│   ├── Maps/
│   ├── Charts/
│   ├── Dashboard/
│   └── AI/
│
├── pages/
│   ├── Home/
│   ├── CountryDetails/
│   └── BrazilDetails/
│
├── services/
│   ├── climateService.js
│   └── aiService.js
│
├── hooks/
├── utils/
├── data/
├── App.jsx
└── index.css

A estrutura poderá ser adaptada conforme o crescimento da aplicação e as decisões de arquitetura.

3. Configuração e Segurança

As integrações deverão seguir as recomendações de segurança de cada serviço.

Chaves privadas de serviços de Inteligência Artificial não deverão ser disponibilizadas diretamente no código frontend.

A estratégia de gerenciamento das credenciais e a eventual utilização de funções serverless ou backend serão definidas durante o planejamento técnico.

⸻

Plano de Ação (Roadmap de Execução)

Etapa	Ação	Objetivo
1	Planejamento técnico	Validar as fontes de dados e as tecnologias.
2	Configuração inicial	Criar o projeto React com Vite e organizar a estrutura.
3	Integração geográfica	Preparar os limites dos países e estados brasileiros.
4	Integração climática	Testar o consumo e a disponibilidade dos dados históricos.
5	Processamento territorial	Implementar a metodologia de média territorial.
6	Construção do globo	Desenvolver a visualização 3D e a seleção de países.
7	Dashboard mundial	Apresentar os indicadores e gráficos por país.
8	Integração com IA	Implementar a interpretação dos dados climáticos.
9	Análise brasileira	Desenvolver o mapa estadual e suas funcionalidades.
10	Testes e refinamento	Validar os resultados, a responsividade e as integrações.
11	Entrega	Finalizar e disponibilizar a aplicação.

⸻

Decisões Técnicas Pendentes

Os seguintes pontos deverão ser discutidos e definidos pela equipe antes ou durante a implementação:

* Validação definitiva da API climática principal (Open-Meteo ERA5 e possibilidade de utilização da NASA POWER).
* Definição da periodicidade dos gráficos (anual, mensal ou ambas).
* Metodologia de cálculo das anomalias térmicas.
* Estratégia de processamento e armazenamento dos dados territoriais.
* Tratamento de países pequenos e territórios com baixa disponibilidade de dados.
* Definição do provedor de Inteligência Artificial.
* Estratégia de integração segura com a IA.
* Avaliação da necessidade de backend ou funções serverless.
* Definição da biblioteca para o mapa detalhado do Brasil.

Observação: as tecnologias e fontes de dados apresentadas neste documento representam a proposta inicial do projeto e poderão ser ajustadas após os testes de viabilidade.

⸻

Climate Mapping — Explorando os dados para compreender as mudanças climáticas.