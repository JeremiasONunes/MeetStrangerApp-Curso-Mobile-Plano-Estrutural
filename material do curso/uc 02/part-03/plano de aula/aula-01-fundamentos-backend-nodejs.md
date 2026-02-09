# Aula 01 - Fundamentos de Backend e Ambiente Node.js

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 03 - Backend  
**Carga Horária:** 4 horas  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Compreender** o papel do backend em aplicações mobile
2. **Diferenciar** arquitetura cliente-servidor
3. **Instalar** e configurar Node.js
4. **Criar** primeiro projeto backend
5. **Executar** scripts básicos em Node.js

---

## 📚 Conteúdos Programáticos

### 1. Arquitetura Cliente-Servidor (45 min)
- Conceito de cliente e servidor
- Comunicação HTTP/HTTPS
- Request e Response
- Papel do backend

### 2. Backend no Ecossistema Mobile (30 min)
- Por que apps precisam de backend
- Funcionalidades do backend
- Backend do MeetStranger

### 3. Node.js - Conceito e Funcionamento (45 min)
- O que é Node.js
- JavaScript no servidor
- Event Loop
- NPM (Node Package Manager)

### 4. Instalação e Configuração (60 min)
- Instalar Node.js
- Verificar instalação
- Configurar ambiente
- IDEs e ferramentas

### 5. Primeiro Projeto (60 min)
- Criar projeto
- package.json
- Scripts básicos
- Hello World

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Arquitetura Cliente-Servidor (45 min)

**Atividade 1:** Conceito (15 min)
```
CLIENTE (Frontend Mobile)
    ↓ Request (HTTP)
SERVIDOR (Backend)
    ↓ Response (JSON)
CLIENTE recebe dados

Exemplo MeetStranger:
1. App envia: POST /api/auth/login
2. Backend valida credenciais
3. Backend retorna: { token, user }
4. App armazena token
```

**Atividade 2:** Papel do Backend (20 min)
```
Backend é responsável por:
✅ Autenticação e autorização
✅ Lógica de negócio
✅ Acesso ao banco de dados
✅ Validação de dados
✅ Segurança
✅ APIs para comunicação

Frontend (App) é responsável por:
✅ Interface do usuário
✅ Experiência do usuário
✅ Consumir APIs
✅ Apresentar dados
```

**Atividade 3:** Discussão (10 min)

### Momento 2: Backend no Mobile (30 min)

**Atividade:** Por que Backend?
```
Sem Backend:
❌ Dados apenas no dispositivo
❌ Sem sincronização
❌ Sem compartilhamento
❌ Sem segurança centralizada

Com Backend:
✅ Dados centralizados
✅ Sincronização entre dispositivos
✅ Compartilhamento de dados
✅ Segurança robusta
✅ Escalabilidade

MeetStranger precisa de backend para:
- Autenticação de usuários
- Matching P2P
- Chat em tempo real (WebSocket)
- Gerenciar filas
- Armazenar dados
```

### Momento 3: Node.js (45 min + 10 min intervalo)

**Atividade 1:** O que é Node.js (15 min)
```
Node.js:
- JavaScript no servidor
- Baseado no V8 (Chrome)
- Assíncrono e event-driven
- Single-threaded com event loop
- NPM (maior repositório de pacotes)

Por que Node.js para backend mobile?
✅ JavaScript full-stack
✅ Performance alta
✅ Comunidade grande
✅ Pacotes prontos (Express, Socket.io)
✅ Fácil integração
```

**Atividade 2:** Event Loop (20 min)
```javascript
// Síncrono (bloqueia)
console.log('1');
console.log('2');
console.log('3');
// Saída: 1, 2, 3

// Assíncrono (não bloqueia)
console.log('1');
setTimeout(() => console.log('2'), 0);
console.log('3');
// Saída: 1, 3, 2

// Útil para I/O (banco, arquivos, rede)
```

**Atividade 3:** NPM (10 min)
```bash
# NPM: Node Package Manager
# Gerencia dependências do projeto

npm install express    # Instala pacote
npm install --save-dev nodemon  # Dev dependency
npm uninstall express  # Remove pacote
```

### Momento 4: Instalação e Configuração (60 min)

**Atividade 1:** Instalar Node.js (20 min)
```bash
# Windows
1. Baixar: https://nodejs.org/
2. Instalar versão LTS (Long Term Support)
3. Verificar instalação:

node --version
# v18.x.x ou superior

npm --version
# 9.x.x ou superior
```

**Atividade 2:** Configurar VS Code (20 min)
```
Extensões recomendadas:
✅ ESLint
✅ Prettier
✅ REST Client
✅ Thunder Client
✅ GitLens

Configurações:
- Auto Save: afterDelay
- Format On Save: true
- Tab Size: 2
```

**Atividade 3:** Ferramentas Adicionais (20 min)
```
Instalar globalmente:
npm install -g nodemon
# Reinicia servidor automaticamente

Ferramentas úteis:
- Postman (testar APIs)
- Insomnia (testar APIs)
- Thunder Client (extensão VS Code)
```

### Momento 5: Primeiro Projeto (60 min)

**Atividade 1:** Criar Projeto (20 min)
```bash
# Criar pasta
mkdir meu-primeiro-backend
cd meu-primeiro-backend

# Inicializar projeto
npm init -y

# Estrutura criada:
# meu-primeiro-backend/
# └── package.json
```

**package.json criado:**
```json
{
  "name": "meu-primeiro-backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

**Atividade 2:** Hello World (20 min)
```javascript
// index.js
console.log('Hello World!');
console.log('Meu primeiro backend em Node.js');

const nome = 'MeetStranger';
const versao = '1.0.0';

console.log(`Projeto: ${nome}`);
console.log(`Versão: ${versao}`);
```

```bash
# Executar
node index.js

# Saída:
# Hello World!
# Meu primeiro backend em Node.js
# Projeto: MeetStranger
# Versão: 1.0.0
```

**Atividade 3:** Scripts NPM (20 min)
```json
// package.json - adicionar scripts
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  }
}
```

```bash
# Executar com npm
npm start
# ou
npm run dev  # Com nodemon (reinicia automaticamente)
```

### Momento 6: Prática Guiada (45 min)

**Atividade:** Criar Projeto MeetStranger Backend

```bash
# 1. Criar estrutura
mkdir meetstranger-backend
cd meetstranger-backend
npm init -y

# 2. Instalar dependências
npm install express
npm install --save-dev nodemon

# 3. Criar estrutura de pastas
mkdir src
```

**src/index.js:**
```javascript
// Importar módulos
const express = require('express');

// Criar aplicação
const app = express();
const PORT = 3000;

// Rota básica
app.get('/', (req, res) => {
  res.json({
    message: 'MeetStranger API',
    version: '1.0.0',
    status: 'running'
  });
});

// Iniciar servidor
app.listen(PORT, () => {
  console.log(`🚀 Servidor rodando na porta ${PORT}`);
  console.log(`📡 Acesse: http://localhost:${PORT}`);
});
```

**package.json - atualizar:**
```json
{
  "name": "meetstranger-backend",
  "version": "1.0.0",
  "main": "src/index.js",
  "scripts": {
    "start": "node src/index.js",
    "dev": "nodemon src/index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "nodemon": "^3.0.2"
  }
}
```

```bash
# Executar
npm run dev

# Abrir navegador: http://localhost:3000
# Deve mostrar JSON com informações da API
```

### Momento 7: Fechamento (30 min)

**Atividade 1:** Síntese (15 min)
```
Aprendemos:
✅ Arquitetura cliente-servidor
✅ Papel do backend em apps mobile
✅ Node.js e JavaScript no servidor
✅ Instalação e configuração
✅ NPM e gerenciamento de pacotes
✅ Primeiro projeto backend
✅ Express básico

Próxima aula:
→ Express aprofundado
→ Rotas e middlewares
→ Estruturação de projetos
```

**Atividade 2:** Exercício para Casa (10 min)

**Atividade 3:** Preparação (5 min)

---

## 📝 Exercício para Casa

**Parte 1: Explorar Node.js**

Criar arquivo `explorando.js`:
```javascript
// 1. Variáveis e tipos
const nome = 'MeetStranger';
let usuarios = 0;

// 2. Função
function incrementarUsuarios() {
  usuarios++;
  console.log(`Total de usuários: ${usuarios}`);
}

// 3. Array
const categorias = ['Filmes', 'Jogos', 'Séries'];
console.log('Categorias:', categorias);

// 4. Objeto
const usuario = {
  id: 1,
  username: 'joao123',
  email: 'joao@email.com',
  online: true
};
console.log('Usuário:', usuario);

// 5. Executar
incrementarUsuarios();
incrementarUsuarios();
```

**Parte 2: Criar Projeto Pessoal**

Criar projeto "minha-api":
```bash
mkdir minha-api
cd minha-api
npm init -y
npm install express
```

Criar `index.js` com:
- Servidor Express
- 3 rotas diferentes
- Mensagens personalizadas

**Parte 3: Pesquisa**

Responder:
1. O que é Event Loop no Node.js?
2. Diferença entre dependência e devDependency?
3. Para que serve o nodemon?
4. O que é o package.json?

**Formato:** Arquivo .js + documento .txt com respostas

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Conhecimento prévio de JavaScript
- Experiência com linha de comando

### Avaliação Formativa

**Critérios:**
- ✅ Instala Node.js corretamente
- ✅ Cria projeto com npm init
- ✅ Executa scripts básicos
- ✅ Compreende arquitetura cliente-servidor
- ✅ Entende papel do backend

**Peso da Aula:** 10% da nota da Parte 3

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Explica arquitetura cliente-servidor  
✅ Instala e configura Node.js  
✅ Cria projeto com npm  
✅ Executa scripts Node.js  
✅ Usa Express básico  
✅ Compreende papel do backend  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Computadores com internet
- [ ] Instalador Node.js
- [ ] VS Code
- [ ] Projetor/TV
- [ ] Slides

### Links Úteis
- Node.js: https://nodejs.org/
- NPM: https://www.npmjs.com/
- Express: https://expressjs.com/
- Nodemon: https://nodemon.io/

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 45 min
- ⏰ Momento 2: 30 min
- ⏰ Momento 3: 55 min (com intervalo)
- ⏰ Momento 4: 60 min
- ⏰ Momento 5: 60 min
- ⏰ Momento 6: 45 min
- ⏰ Momento 7: 30 min

### Pontos de Atenção
1. **Instalação**: Verificar em todos os computadores
2. **Versão**: Usar LTS (Long Term Support)
3. **PATH**: Garantir que Node está no PATH
4. **NPM**: Explicar bem o package.json
5. **Erros**: Mostrar erros comuns e soluções

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
