# Aula 02 - Express e Estruturação de Projetos Backend

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 03 - Backend  
**Carga Horária:** 4 horas  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Utilizar** Express para criar servidores web
2. **Estruturar** projetos backend profissionalmente
3. **Implementar** rotas básicas
4. **Organizar** código em camadas
5. **Testar** APIs com ferramentas adequadas

---

## 📚 Conteúdos Programáticos

### 1. Framework Express (45 min)
- O que é Express
- Vantagens do Express
- Middlewares
- Request e Response

### 2. Servidor HTTP (45 min)
- Criar servidor Express
- Configurações básicas
- Porta e host
- Inicialização

### 3. Organização de Projeto (60 min)
- Estrutura de pastas
- Separação de responsabilidades
- Padrão MVC adaptado
- Boas práticas

### 4. Rotas Básicas (60 min)
- GET, POST, PUT, DELETE
- Parâmetros de rota
- Query strings
- Body de requisição

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Framework Express (45 min)

**Atividade 1:** O que é Express (15 min)
```javascript
// Express: Framework minimalista para Node.js

// Sem Express (Node.js puro)
const http = require('http');
const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ message: 'Hello' }));
  }
});

// Com Express (muito mais simples)
const express = require('express');
const app = express();
app.get('/', (req, res) => {
  res.json({ message: 'Hello' });
});
```

**Atividade 2:** Vantagens (15 min)
```
Express oferece:
✅ Roteamento simplificado
✅ Middlewares poderosos
✅ Suporte a templates
✅ Gerenciamento de requisições
✅ Tratamento de erros
✅ Comunidade grande
✅ Muitos plugins

Ideal para:
- APIs REST
- Aplicações web
- Microserviços
- Backend mobile
```

**Atividade 3:** Conceito de Middleware (15 min)
```javascript
// Middleware: função que processa requisição

// Exemplo 1: Logger
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // Passa para próximo middleware
});

// Exemplo 2: JSON parser
app.use(express.json()); // Converte body para JSON

// Exemplo 3: CORS
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  next();
});

// Fluxo: Request → Middleware 1 → Middleware 2 → Rota → Response
```

### Momento 2: Servidor HTTP (45 min + 10 min intervalo)

**Atividade 1:** Criar Servidor Básico (20 min)
```javascript
// src/app.js
const express = require('express');
const app = express();

// Middlewares
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Rota de teste
app.get('/', (req, res) => {
  res.json({
    message: 'MeetStranger API',
    version: '1.0.0',
    status: 'online'
  });
});

module.exports = app;
```

```javascript
// src/server.js
const app = require('./app');
const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`🚀 Servidor rodando na porta ${PORT}`);
  console.log(`📡 http://localhost:${PORT}`);
});
```

**Atividade 2:** Configurações (15 min)
```javascript
// src/config/server.js
module.exports = {
  port: process.env.PORT || 3000,
  host: process.env.HOST || 'localhost',
  env: process.env.NODE_ENV || 'development'
};
```

**Atividade 3:** Executar e Testar (10 min)
```bash
npm run dev

# Testar no navegador: http://localhost:3000
# Ou com curl:
curl http://localhost:3000
```

### Momento 3: Estrutura de Projeto (60 min)

**Atividade 1:** Estrutura Profissional (20 min)
```
meetstranger-backend/
├── src/
│   ├── config/          # Configurações
│   │   └── database.js
│   ├── controllers/     # Lógica de controle
│   │   └── auth.controller.js
│   ├── routes/          # Definição de rotas
│   │   └── auth.routes.js
│   ├── services/        # Lógica de negócio
│   │   └── auth.service.js
│   ├── middleware/      # Middlewares customizados
│   │   └── auth.middleware.js
│   ├── models/          # Modelos de dados (futuro)
│   ├── utils/           # Funções auxiliares
│   ├── app.js           # Configuração Express
│   └── server.js        # Inicialização
├── tests/               # Testes
├── .env                 # Variáveis de ambiente
├── .gitignore
├── package.json
└── README.md
```

**Atividade 2:** Criar Estrutura (25 min)
```bash
# Criar pastas
mkdir -p src/config src/controllers src/routes src/services src/middleware src/utils

# Criar arquivos base
touch src/config/database.js
touch src/controllers/user.controller.js
touch src/routes/user.routes.js
touch src/services/user.service.js
touch .env .gitignore README.md
```

**.gitignore:**
```
node_modules/
.env
*.log
.DS_Store
```

**.env:**
```
PORT=3000
NODE_ENV=development
```

**Atividade 3:** Padrão MVC Adaptado (15 min)
```
Camadas:

ROUTES (Rotas)
  ↓ Define endpoints
CONTROLLERS (Controladores)
  ↓ Recebe requisição, valida, chama service
SERVICES (Serviços)
  ↓ Lógica de negócio
DATABASE (Banco de Dados)
  ↓ Persistência

Exemplo fluxo:
1. GET /api/users → routes
2. routes → userController.getAll()
3. controller → userService.findAll()
4. service → database.query()
5. database → retorna dados
6. service → processa
7. controller → formata resposta
8. response → JSON para cliente
```

### Momento 4: Rotas Básicas (60 min)

**Atividade 1:** Métodos HTTP (20 min)
```javascript
// src/routes/user.routes.js
const express = require('express');
const router = express.Router();

// GET - Listar todos
router.get('/', (req, res) => {
  res.json({ message: 'Listar usuários' });
});

// GET - Buscar por ID
router.get('/:id', (req, res) => {
  const { id } = req.params;
  res.json({ message: `Buscar usuário ${id}` });
});

// POST - Criar
router.post('/', (req, res) => {
  const { username, email } = req.body;
  res.json({ message: 'Criar usuário', data: { username, email } });
});

// PUT - Atualizar
router.put('/:id', (req, res) => {
  const { id } = req.params;
  res.json({ message: `Atualizar usuário ${id}` });
});

// DELETE - Deletar
router.delete('/:id', (req, res) => {
  const { id } = req.params;
  res.json({ message: `Deletar usuário ${id}` });
});

module.exports = router;
```

**Atividade 2:** Integrar Rotas (15 min)
```javascript
// src/app.js
const express = require('express');
const userRoutes = require('./routes/user.routes');

const app = express();

// Middlewares
app.use(express.json());

// Rotas
app.use('/api/users', userRoutes);

// Rota raiz
app.get('/', (req, res) => {
  res.json({
    message: 'MeetStranger API',
    endpoints: {
      users: '/api/users'
    }
  });
});

module.exports = app;
```

**Atividade 3:** Testar Rotas (25 min)
```bash
# GET - Listar
curl http://localhost:3000/api/users

# GET - Por ID
curl http://localhost:3000/api/users/1

# POST - Criar
curl -X POST http://localhost:3000/api/users \
  -H "Content-Type: application/json" \
  -d '{"username":"joao123","email":"joao@email.com"}'

# PUT - Atualizar
curl -X PUT http://localhost:3000/api/users/1 \
  -H "Content-Type: application/json" \
  -d '{"username":"joao_updated"}'

# DELETE - Deletar
curl -X DELETE http://localhost:3000/api/users/1
```

### Momento 5: Controllers e Services (60 min)

**Atividade 1:** Criar Controller (20 min)
```javascript
// src/controllers/user.controller.js
const userService = require('../services/user.service');

class UserController {
  async getAll(req, res) {
    try {
      const users = await userService.findAll();
      res.json({ success: true, data: users });
    } catch (error) {
      res.status(500).json({ success: false, error: error.message });
    }
  }

  async getById(req, res) {
    try {
      const { id } = req.params;
      const user = await userService.findById(id);
      
      if (!user) {
        return res.status(404).json({ success: false, error: 'Usuário não encontrado' });
      }
      
      res.json({ success: true, data: user });
    } catch (error) {
      res.status(500).json({ success: false, error: error.message });
    }
  }

  async create(req, res) {
    try {
      const { username, email, senha } = req.body;
      const user = await userService.create({ username, email, senha });
      res.status(201).json({ success: true, data: user });
    } catch (error) {
      res.status(400).json({ success: false, error: error.message });
    }
  }

  async update(req, res) {
    try {
      const { id } = req.params;
      const user = await userService.update(id, req.body);
      res.json({ success: true, data: user });
    } catch (error) {
      res.status(400).json({ success: false, error: error.message });
    }
  }

  async delete(req, res) {
    try {
      const { id } = req.params;
      await userService.delete(id);
      res.json({ success: true, message: 'Usuário deletado' });
    } catch (error) {
      res.status(400).json({ success: false, error: error.message });
    }
  }
}

module.exports = new UserController();
```

**Atividade 2:** Criar Service (20 min)
```javascript
// src/services/user.service.js
class UserService {
  constructor() {
    // Mock data (próxima aula: banco real)
    this.users = [
      { id: 1, username: 'alice', email: 'alice@email.com' },
      { id: 2, username: 'bob', email: 'bob@email.com' }
    ];
  }

  async findAll() {
    return this.users;
  }

  async findById(id) {
    return this.users.find(u => u.id === parseInt(id));
  }

  async create(userData) {
    const newUser = {
      id: this.users.length + 1,
      ...userData,
      createdAt: new Date()
    };
    this.users.push(newUser);
    return newUser;
  }

  async update(id, userData) {
    const index = this.users.findIndex(u => u.id === parseInt(id));
    if (index === -1) throw new Error('Usuário não encontrado');
    
    this.users[index] = { ...this.users[index], ...userData };
    return this.users[index];
  }

  async delete(id) {
    const index = this.users.findIndex(u => u.id === parseInt(id));
    if (index === -1) throw new Error('Usuário não encontrado');
    
    this.users.splice(index, 1);
    return true;
  }
}

module.exports = new UserService();
```

**Atividade 3:** Atualizar Rotas (20 min)
```javascript
// src/routes/user.routes.js
const express = require('express');
const router = express.Router();
const userController = require('../controllers/user.controller');

router.get('/', userController.getAll);
router.get('/:id', userController.getById);
router.post('/', userController.create);
router.put('/:id', userController.update);
router.delete('/:id', userController.delete);

module.exports = router;
```

### Momento 6: Testes e Validação (45 min)

**Atividade 1:** Testar CRUD Completo (30 min)
```bash
# 1. Listar usuários
curl http://localhost:3000/api/users

# 2. Criar usuário
curl -X POST http://localhost:3000/api/users \
  -H "Content-Type: application/json" \
  -d '{"username":"carlos","email":"carlos@email.com","senha":"senha123"}'

# 3. Buscar por ID
curl http://localhost:3000/api/users/3

# 4. Atualizar
curl -X PUT http://localhost:3000/api/users/3 \
  -H "Content-Type: application/json" \
  -d '{"username":"carlos_updated"}'

# 5. Deletar
curl -X DELETE http://localhost:3000/api/users/3

# 6. Verificar deleção
curl http://localhost:3000/api/users
```

**Atividade 2:** Thunder Client (15 min)
```
Usar extensão Thunder Client no VS Code:

1. Criar Collection "MeetStranger"
2. Adicionar requests:
   - GET /api/users
   - GET /api/users/:id
   - POST /api/users
   - PUT /api/users/:id
   - DELETE /api/users/:id
3. Testar todos os endpoints
4. Salvar collection
```

### Momento 7: Fechamento (30 min)

**Atividade 1:** Síntese (15 min)
```
Aprendemos:
✅ Framework Express
✅ Middlewares
✅ Estrutura profissional de projeto
✅ Rotas (GET, POST, PUT, DELETE)
✅ Controllers e Services
✅ Separação de responsabilidades
✅ Testes de API

Próxima aula:
→ APIs REST completas
→ Métodos HTTP aprofundados
→ Status codes
→ Padrões REST
```

**Atividade 2:** Exercício para Casa (10 min)

**Atividade 3:** Preparação (5 min)

---

## 📝 Exercício para Casa

**Parte 1: Criar Módulo de Categorias**

Implementar CRUD completo para categorias do MeetStranger:

```javascript
// src/routes/category.routes.js
// src/controllers/category.controller.js
// src/services/category.service.js

// Categorias: Filmes, Jogos, Séries
// Campos: id, nome, descricao, icone, ativa
```

**Parte 2: Adicionar Validações**

```javascript
// Validar no controller:
// - Nome obrigatório
// - Nome único
// - Descrição opcional
// - Ativa padrão true
```

**Parte 3: Documentar API**

Criar arquivo `API.md` documentando:
- Todos os endpoints
- Métodos HTTP
- Parâmetros
- Exemplos de request/response

**Formato:** Código + documentação

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Formativa

**Critérios:**
- ✅ Cria servidor Express
- ✅ Estrutura projeto adequadamente
- ✅ Implementa rotas corretamente
- ✅ Separa responsabilidades
- ✅ Testa endpoints

**Peso da Aula:** 15% da nota da Parte 3

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Configura Express corretamente  
✅ Organiza projeto em camadas  
✅ Implementa CRUD completo  
✅ Usa controllers e services  
✅ Testa APIs adequadamente  
✅ Documenta código  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Node.js instalado
- [ ] VS Code
- [ ] Thunder Client ou Postman
- [ ] Projeto da aula anterior

### Estrutura Final
```
meetstranger-backend/
├── src/
│   ├── controllers/
│   │   └── user.controller.js
│   ├── routes/
│   │   └── user.routes.js
│   ├── services/
│   │   └── user.service.js
│   ├── app.js
│   └── server.js
├── .env
├── .gitignore
└── package.json
```

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 45 min
- ⏰ Momento 2: 55 min (com intervalo)
- ⏰ Momento 3: 60 min
- ⏰ Momento 4: 60 min
- ⏰ Momento 5: 60 min
- ⏰ Momento 6: 45 min
- ⏰ Momento 7: 30 min

### Pontos de Atenção
1. **Estrutura**: Enfatizar organização
2. **Separação**: Controllers ≠ Services
3. **Async/Await**: Usar sempre
4. **Erros**: Try/catch em todos os métodos
5. **Testes**: Testar cada endpoint

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
