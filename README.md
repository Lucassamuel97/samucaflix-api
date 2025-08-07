# 🎬 Samucalix API

Uma API REST Mock completa para streaming de vídeos, construída com JSON Server e hospedada na Vercel. Esta API simula um serviço de streaming como Netflix, fornecendo dados de filmes, séries e conteúdo em destaque.

## 🚀 Funcionalidades

- ✅ API REST completa com operações CRUD
- 🎯 Conteúdo em destaque (featured)
- 🎭 Filmes organizados por categorias
- 📺 Séries organizadas por categorias  
- 🔍 Busca e filtragem de conteúdo
- 🌐 Deploy automático na Vercel
- 📱 Suporte a CORS para integração frontend

## 📋 Endpoints Disponíveis

### Conteúdo em Destaque
```
GET /featured - Lista todos os conteúdos em destaque
GET /featured/{id} - Busca conteúdo em destaque por ID
```

### Filmes
```
GET /movies - Lista todos os filmes
GET /movies/{id} - Busca filme por ID
GET /movies?genres_like={genre} - Filtra filmes por gênero
```

### Séries
```
GET /series - Lista todas as séries
GET /series/{id} - Busca série por ID
GET /series?genres_like={genre} - Filtra séries por gênero
```

### Busca Geral
```
GET /featured?q={termo} - Busca no conteúdo em destaque
GET /movies?q={termo} - Busca nos filmes
GET /series?q={termo} - Busca nas séries
```

## 🛠️ Tecnologias Utilizadas

- **Node.js** - Runtime JavaScript
- **JSON Server** - Criação rápida de API REST
- **Vercel** - Hospedagem e deploy
- **JSON** - Banco de dados simulado

## 📦 Instalação Local

### Pré-requisitos
- Node.js (versão 14 ou superior)
- npm ou yarn

### Passos para instalação

1. **Clone o repositório**
```bash
git clone <url-do-repositorio>
cd samucalix_api-main
```

2. **Instale as dependências**
```bash
npm install
```

3. **Execute o servidor local**
```bash
npm start
```

4. **Acesse a API**
```
http://localhost:3000
```

## 🌐 Deploy na Vercel

Este projeto está configurado para deploy automático na Vercel:

1. **Conecte seu repositório à Vercel**
2. **Configure as variáveis de ambiente** (se necessário)
3. **Deploy automático** será feito a cada push na branch principal

### Configuração Vercel
O arquivo `vercel.json` já está configurado com:
- Função serverless para a API
- Inclusão do arquivo de dados `db.json`
- Rewrite de rotas para o servidor principal

## 📄 Estrutura de Dados

### Exemplo de Conteúdo
```json
{
  "id": 101,
  "title": "Squid Game",
  "description": "Centenas de jogadores sem dinheiro aceitam um convite...",
  "yearLaunched": "2021",
  "link": "/watch/101",
  "castMembers": ["Lee Jung-jae", "Park Hae-soo", "Wi Ha-jun"],
  "genres": ["Action", "Drama", "Mystery"],
  "thumbFileURL": "https://...",
  "bannerFileURL": "https://...",
  "videoFileURL": "https://...",
  "rating": "r"
}
```

### Campos Disponíveis
- **id**: Identificador único
- **title**: Título do conteúdo
- **description**: Descrição/sinopse
- **yearLaunched**: Ano de lançamento
- **link**: Link para visualização
- **castMembers**: Array com elenco principal
- **genres**: Array com gêneros
- **thumbFileURL**: URL da thumbnail
- **bannerFileURL**: URL do banner
- **videoFileURL**: URL do vídeo
- **rating**: Classificação etária

## 🔍 Exemplos de Uso

### Buscar conteúdo em destaque
```javascript
fetch('https://sua-api.vercel.app/featured')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Buscar filmes de ação
```javascript
fetch('https://sua-api.vercel.app/movies?genres_like=Action')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Buscar por título
```javascript
fetch('https://sua-api.vercel.app/featured?q=Stranger')
  .then(response => response.json())
  .then(data => console.log(data));
```

## ⚙️ Configurações Avançadas

### Habilitando Operações de Escrita
Para permitir POST, PUT, DELETE, descomente as linhas no arquivo `api/server.js`:

```javascript
// Descomente estas linhas:
const fs = require('fs')
const path = require('path')
const filePath = path.join('db.json')
const data = fs.readFileSync(filePath, "utf-8");
const db = JSON.parse(data);
const router = jsonServer.router(db)

// E comente esta linha:
// const router = jsonServer.router('db.json')
```

### Personalizando Rotas
Edite o objeto rewriter no `server.js` para criar rotas customizadas:

```javascript
server.use(jsonServer.rewriter({
    '/api/*': '/$1',
    '/v1/movies': '/movies',
    '/v1/series': '/series'
}))
```

⭐ Se este projeto foi útil para você, considere dar uma estrela no repositório!
