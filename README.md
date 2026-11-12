# Climate Mapping

Plataforma web interativa de visualização e análise de dados climáticos históricos com suporte de Inteligência Artificial para interpretação territorial.

## Visão Geral

O **Climate Mapping** centraliza dados meteorológicos históricos (janela de 30 anos: 1996 a 2025) e limites geográficos para permitir a exploração visual das mudanças climáticas em escala global e nacional. Por meio de um globo terrestre 3D interativo, o usuário seleciona países para visualizar séries históricas e, ao selecionar o Brasil, acessa uma camada detalhada das unidades federativas. A plataforma integra o modelo `gpt-4.1-nano` da OpenAI para interpretar métricas processadas, comparar territórios e responder a perguntas baseadas estritamente nos dados exibidos.

## Arquitetura do Sistema

O projeto adota uma arquitetura Single Page Application (SPA) dividida em três camadas principais, apoiada por uma camada de função serverless/backend para proteção de credenciais da IA:

1. **Camada de Apresentação:** Interface responsiva, globo 3D interativo, mapas vetoriais estaduais e gráficos estatísticos.
2. **Camada de Integração:** Consumo de APIs meteorológicas públicas, carregamento de malhas GeoJSON e agregação espacial.
3. **Camada de Análise e IA:** Processamento de médias territoriais, cálculo de anomalias térmicas e integração segura com a API da OpenAI.

## Fontes de Dados e Referências Técnicas

| Categoria | Fonte | Finalidade no Projeto | Documentação / Acesso |
| :--- | :--- | :--- | :--- |
| **Clima Global e Nacional** | Open-Meteo (ERA5) | Dados meteorológicos históricos (1996–2025): temperatura média, máxima e precipitação. | [Open-Meteo Historical API](https://open-meteo.com/en/docs/historical-weather-api) |
| **Clima (Validação)** | NASA POWER | Fonte complementar para validação cruzada de séries históricas e radiação/temperatura. | [NASA POWER Docs](https://power.larc.nasa.gov/docs/) |
| **Geografia Mundial** | Natural Earth | Polígonos e limites territoriais dos países em formato GeoJSON/TopoJSON. | [Natural Earth Data](https://www.naturalearthdata.com/) |
| **Geografia Brasil** | IBGE (Malhas Territoriais) | Limites oficiais das 27 unidades federativas brasileiras. | [API Localidades IBGE](https://servicodados.ibge.gov.br/api/v1/localidades/estados) / [Portal IBGE](https://www.ibge.gov.br/geociencias/organizacao-do-territorio/malhas-territoriais.html) |
| **Inteligência Artificial** | OpenAI API | Interpretação em linguagem natural dos indicadores processados (`gpt-4.1-nano`). | [OpenAI API Docs](https://platform.openai.com/docs) |

## Stack Tecnológica

* **Frontend:** React, Vite, CSS3 / Tailwind CSS
* **Visualização 3D:** Globe.gl (Three.js)
* **Mapas 2D (Brasil):** MapLibre GL JS
* **Gráficos Estatísticos:** Recharts
* **Processamento Geoespacial:** Turf.js (cálculo de centroides, grades e interseção de polígonos)
* **Backend Proxy (Segurança):** Node.js / Express ou Vercel Serverless Functions
* **IA:** OpenAI SDK (`gpt-4.1-nano`)

## Metodologia de Análise

* **Período Histórico:** 30 anos (01/01/1996 a 31/12/2025).
* **Agregação Espacial:** Geração de pontos de grade dentro dos polígonos territoriais (países e estados brasileiros) via Turf.js para cálculo de médias espaciais representativas, evitando o viés de coordenada única.
* **Indicadores:**
  * Temperatura Média Anual e Mensal (°C)
  * Temperatura Máxima Média (°C)
  * Precipitação Acumulada (mm)
  * Anomalia Térmica (desvio em relação à média climatológica de referência de 30 anos)

## Estrutura de Diretórios

```text
climate-mapping/
├── api/                          # Funções serverless (proxy seguro para OpenAI)
│   └── analyze.js
├── public/
│   └── geojson/                  # Arquivos estáticos otimizados (países e estados BR)
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── Globe/                # Globo 3D interativo (Globe.gl)
│   │   ├── Maps/                 # Mapa detalhado do Brasil (MapLibre)
│   │   ├── Charts/               # Séries temporais e anomalias (Recharts)
│   │   ├── Dashboard/            # Cards de KPIs e filtros
│   │   └── AI/                   # Painel de interpretação e chat climático
│   ├── hooks/
│   │   └── useClimateData.js
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── CountryDetails.jsx
│   │   └── BrazilDetails.jsx
│   ├── services/
│   │   ├── climateService.js     # Integração Open-Meteo
│   │   ├── geoService.js         # Integração IBGE e Natural Earth
│   │   └── aiService.js          # Comunicação com /api/analyze
│   ├── utils/
│   │   └── spatialMath.js        # Cálculo de médias e anomalias
│   ├── App.jsx
│   └── main.jsx
├── .env.example
├── package.json
└── README.md
