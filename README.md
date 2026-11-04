# Projeto Meteorológico Inteligente - Documentação e Guia Prático (React SPA)

Este documento serve como fonte da verdade para o desenvolvimento do sistema de consolidação e interpretação de dados meteorológicos. O projeto integra a One Call API 4.0 (OpenWeatherMap), a WeatherAPI e uma API de Inteligência Artificial para gerar previsões climáticas analisadas em linguagem natural, utilizando uma arquitetura de Single Page Application (SPA) com React.

O ciclo de vida de desenvolvimento (SDLC) e o Spec-Driven Development (SDD) seguem estritamente as quatro fases estabelecidas na diretriz institucional do projeto.

## FASE 1: Arquitetura do Sistema (Design e Planejamento)

Nesta fase inicial, definimos a base técnica obrigatória. Nenhuma codificação deve ocorrer sem a aprovação deste desenho técnico.

### Desenho de Arquitetura (High-Level Design)

O sistema adota uma arquitetura Client-Side Rendering (SPA) focada na orquestração de APIs externas diretamente no frontend:

1. **Camada de Apresentação (View):** Componentes React puros (Hooks, Context API) para renderização da interface (Dashboard de clima, cards de alertas e caixa de análise da IA).
2. **Camada de Serviços (API Clients):** Módulos JavaScript/TypeScript dedicados a realizar chamadas HTTP assíncronas (via `fetch` ou `axios`) para as APIs externas.
3. **Camada de Orquestração e IA:** Funções utilitárias no React que recebem os dados brutos das APIs meteorológicas, formatam o payload e enviam para a API de IA solicitando a interpretação em texto.

### Integrações Sistêmicas e Contratos

* **OpenWeatherMap (One Call API 4.0):**
  * Responsabilidade: Dados hiperlocais e linha do tempo.
  * Chamada via React: `GET https://api.openweathermap.org/data/3.0/onecall?lat={lat}&lon={lon}&appid={API_KEY}`

* **WeatherAPI:**
  * Responsabilidade: Qualidade do ar (AQI) e astronomia.
  * Chamada via React: `GET https://api.weatherapi.com/v1/forecast.json?key={API_KEY}&q={lat},{lon}`

* **API de IA (ex: OpenAI / Gemini via SDK ou REST):**
  * Responsabilidade: Raciocínio lógico sobre o JSON unificado e geração de resposta em linguagem natural.

### Riscos e Mitigações (Foco em SPA)

* **Risco:** Exposição de chaves de API no código cliente (Frontend).
  * **Mitigação:** Utilizar variáveis de ambiente injetadas no build (ex: `.env`) para desenvolvimento. Para o ambiente produtivo, planejar o uso de Serverless Functions (ex: Vercel Functions/Netlify Functions) como proxy seguro para ocultar as chaves, mantendo a filosofia SPA.
* **Risco:** Problemas de CORS (Cross-Origin Resource Sharing) ao chamar APIs de IA diretamente do navegador.
  * **Mitigação:** Garantir que o provedor de IA suporte chamadas via client-side ou implementar o proxy serverless mencionado acima.

## FASE 2: Discovery de Negócio (Requisitos)

O mapeamento do domínio conduzido pelo PO e Arquiteto focado na experiência do usuário na interface.

### AS IS vs TO BE

* **AS IS:** O usuário consulta múltiplos sites pesados para cruzar dados de previsão.
* **TO BE:** O usuário acessa uma única tela (SPA) rápida e responsiva que carrega assincronamente os dados, cruza as informações no navegador e exibe uma recomendação escrita por IA em segundos.

### Features Principais

1. **Feature A (Geolocalização):** Captura automática da localização do usuário via API do navegador (HTML5 Geolocation) com fallback para busca por nome da cidade.
2. **Feature B (Dashboard Consolidado):** Renderização de componentes React exibindo temperatura, umidade, UV e qualidade do ar.
3. **Feature C (Smart Insight):** Botão "Analisar com IA" que processa os dados carregados em tela e renderiza um componente de texto com o parecer meteorológico estruturado.

## FASE 3: Quebra das Histórias (Desenvolvimento e Testes)

Transformação das features em histórias consumíveis pelo time, conduzidas pelo Tech Community Lead (TCL).

### Regras de Qualidade (DoR e DoD)

**Definition of Ready (DoR):**
* História no formato: "Como \[persona\], quero \[ação\], para \[benefício\]".
* Critérios de aceite e protótipos de tela (Figma/Wireframes) anexados.

**Definition of Done (DoD) Específico para React:**
* Componentes criados seguindo princípios de responsividade (Mobile First).
* Código revisado via Pull Request.
* Testes unitários de componentes (ex: Jest + React Testing Library) cobrindo os cenários de sucesso, erro (API fora) e loading.
* Sem warnings de lint (ESLint) ou de dependências no console do navegador.

## FASE 4: Definição do MVP (Implantação)

* **MVP 1:** SPA em React de página única. O usuário digita a cidade ou permite a localização. A aplicação faz o fetch na WeatherAPI e OpenWeatherMap, exibe os dados básicos na tela e exibe a análise da IA logo abaixo. Sem gráficos complexos ou paginação.
* **MVP 2:** Adição de gráficos de previsão por hora (usando bibliotecas como Recharts ou Chart.js), persistência de histórico de buscas no `localStorage` do navegador e tratamento avançado de alertas severos.

---

## Guia de Implementação (React SPA)

### 1. Inicialização do Projeto
Recomenda-se o uso do Vite para scaffolding rápido e otimizado de um projeto React puro:
```bash
npm create vite@latest clima-inteligente-spa -- --template react
cd clima-inteligente-spa
npm install
```

### 2. Configuração de Variáveis de Ambiente
Crie um arquivo `.env` na raiz do projeto. O Vite exige o prefixo `VITE_` para expor variáveis ao frontend:
```env
VITE_OPENWEATHER_API_KEY=sua_chave_aqui
VITE_WEATHERAPI_KEY=sua_chave_aqui
VITE_AI_API_KEY=sua_chave_aqui
```

### 3. Estrutura de Pastas Sugerida
```text
src/
 ├── components/       (Cards, Botões, Loading Spinners)
 ├── hooks/            (Hooks customizados, ex: useWeatherData, useAI)
 ├── services/         (Funções utilitárias usando fetch/axios para as APIs)
 ├── utils/            (Formatadores de data, conversores de temperatura)
 ├── App.jsx           (Componente principal, gerenciador de estado global)
 └── index.css         (Estilos globais)
```

### 4. Execução Local
```bash
npm run dev
```

---

## Plano de Ação (Roadmap de Execução)

Para garantir a fluidez do projeto saindo da documentação para a prática, siga a ordem de execução abaixo:

| Etapa | Ação | Responsável | Objetivo |
| :--- | :--- | :--- | :--- |
| **Passo 1** | **Setup Base** | Engenharia | Criar o repositório, iniciar o projeto React (Vite) e configurar o ESLint. |
| **Passo 2** | **Serviços de API** | Engenharia | Criar os arquivos dentro de `src/services/` para buscar dados estruturados do OpenWeather e WeatherAPI. Testar no console. |
| **Passo 3** | **Integração IA** | Engenharia | Criar o serviço de IA, formatar o prompt unindo os JSONs das duas APIs e validar o retorno textual no console. |
| **Passo 4** | **Construção da UI** | Engenharia/UX | Desenvolver os componentes visuais básicos (Input de busca, Card de Clima, Box de Resposta da IA). |
| **Passo 5** | **Integração Front e APIs** | Engenharia | Conectar os componentes visuais aos serviços criados (gerenciamento de estados de Loading, Success e Error no React). |
| **Passo 6** | **Refinamento e Testes** | TL/Engenharia | Aplicar validações, escrever testes unitários nos componentes principais e garantir responsividade no mobile. |
| **Passo 7** | **Homologação MVP 1** | TL | Validar se o sistema atende aos critérios do MVP e realizar deploy em plataformas estáticas (ex: Vercel, Netlify, GitHub Pages). |
