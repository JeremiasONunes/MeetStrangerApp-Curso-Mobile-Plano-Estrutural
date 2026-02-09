# Aula 09-10 - Segurança, Versionamento e Documentação

**Carga Horária:** 8 horas  
**Modalidade:** Presencial  
**Competências:** Segurança de APIs, controle de versão e documentação técnica

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Implementar autenticação básica com JWT
- ✅ Proteger rotas com middleware de autenticação
- ✅ Criptografar senhas com bcrypt
- ✅ Aplicar CORS adequadamente
- ✅ Utilizar Git para controle de versão
- ✅ Documentar API com Swagger/OpenAPI
- ✅ Criar README profissional

---

## 📚 Conteúdo Programático

### 1. Segurança da Informação
- Criptografia de senhas (bcrypt)
- Autenticação com JWT
- Proteção de rotas
- CORS (Cross-Origin Resource Sharing)
- Variáveis de ambiente

### 2. Controle de Versão
- Git básico (init, add, commit, push)
- Branches e merge
- .gitignore
- Commits semânticos

### 3. Documentação de APIs
- Swagger/OpenAPI
- README.md
- Comentários no código
- Exemplos de uso

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Tratamento de erros centralizado
- Async/await
- Debugging

**Atividade de Aquecimento:**
```
Discussão:
- Por que não podemos armazenar senhas em texto puro?
- Como o sistema sabe que você está logado?
- Por que documentar a API?

Objetivo: Preparar para segurança e documentação
```

---

### 2️⃣ Apresentação (90 min)

#### 📖 Parte 1: Criptografia de Senhas (20 min)

**Problema:**
```javascript
// ❌ NUNCA FAZER ISSO
{ senha: "123456" }  // Senha em texto puro no banco
```

**Solução com bcrypt:**
```javascript
const bcrypt = require('bcrypt');

// Criptografar
const senhaHash = await bcrypt.hash('123456', 10);
// $2b$10$xK8j9...

// Comparar
const valida = await bcrypt.compare('123456', senhaHash);
// true ou false
```

**Instalação:**
```bash
npm install bcrypt
```

#### 📖 Parte 2: Autenticação com JWT (30 min)

**O que é JWT?**
JSON Web Token - token criptografado que identifica o usuário

**Estrutura:**
```
header.payload.signature
eyJhbGc...  .  eyJ1c2Vy...  .  SflKxwRJ...
```

**Fluxo:**
```
1. Cliente faz login (POST /auth/login)
2. Servidor valida credenciais
3. Servidor gera JWT
4. Cliente armazena JWT
5. Cliente envia JWT em requisições (Header: Authorization)
6. Servidor valida JWT
7. Servidor processa requisição
```

**Instalação:**
```bash
npm install jsonwebtoken
```

**Gerar Token:**
```javascript
const jwt = require('jsonwebtoken');

const token = jwt.sign(
  { id: usuario.id, email: usuario.email },
  'SECRET_KEY',
  { expiresIn: '24h' }
);
```

**Validar Token:**
```javascript
const token = req.headers.authorization?.split(' ')[1];
const decoded = jwt.verify(token, 'SECRET_KEY');
// { id: 1, email: 'user@email.com' }
```

#### 📖 Parte 3: CORS (15 min)

**Problema:**
```
Access to fetch at 'http://localhost:3000/usuarios' from origin 
'http://localhost:19006' has been blocked by CORS policy
```

**Solução:**
```bash
npm install cors
```

```javascript
const cors = require('cors');

app.use(cors({
  origin: 'http://localhost:19006',
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

#### 📖 Parte 4: Variáveis de Ambiente (15 min)

**Problema:**
```javascript
// ❌ Expor credenciais no código
const SECRET = 'minha_chave_secreta';
```

**Solução:**
```bash
npm install dotenv
```

**Arquivo:** `.env`
```
PORT=3000
JWT_SECRET=sua_chave_super_secreta_aqui
DB_PATH=./database/meetstranger.db
NODE_ENV=development
```

**Uso:**
```javascript
require('dotenv').config();

const port = process.env.PORT || 3000;
const secret = process.env.JWT_SECRET;
```

#### 📖 Parte 5: Git e Versionamento (10 min)

**Comandos Básicos:**
```bash
git init                    # Inicializar repositório
git add .                   # Adicionar arquivos
git commit -m "mensagem"    # Commit
git branch feature/auth     # Criar branch
git checkout feature/auth   # Mudar de branch
git merge feature/auth      # Mesclar branch
```

**Commits Semânticos:**
```
feat: adicionar autenticação JWT
fix: corrigir validação de email
docs: atualizar README
refactor: refatorar UserService
```

---

### 3️⃣ Prática Guiada (180 min)

#### 💻 Exercício 1: Implementar Criptografia de Senhas (30 min)

**Instalar:**
```bash
npm install bcrypt
```

**Atualizar:** `src/services/UserService.js`

```javascript
const bcrypt = require('bcrypt');
const UserRepository = require('../repositories/UserRepository');

class UserService {
  static async create(dados) {
    // Validações
    if (!dados.username || dados.username.length < 3) {
      throw new Error('Username deve ter no mínimo 3 caracteres');
    }

    if (!dados.email || !dados.email.includes('@')) {
      throw new Error('Email inválido');
    }

    if (!dados.senha || dados.senha.length < 6) {
      throw new Error('Senha deve ter no mínimo 6 caracteres');
    }

    // Verificar email duplicado
    const usuarioExistente = await UserRepository.findByEmail(dados.email);
    if (usuarioExistente) {
      throw new Error('Email já cadastrado');
    }

    // Criptografar senha
    const senhaHash = await bcrypt.hash(dados.senha, 10);

    // Criar usuário
    const resultado = await UserRepository.create({
      ...dados,
      senha: senhaHash
    });
    
    const usuario = await UserRepository.findById(resultado.id);
    return usuario;
  }

  static async update(id, dados) {
    // Validações
    if (dados.username && dados.username.length < 3) {
      throw new Error('Username deve ter no mínimo 3 caracteres');
    }

    if (dados.email && !dados.email.includes('@')) {
      throw new Error('Email inválido');
    }

    if (dados.senha && dados.senha.length < 6) {
      throw new Error('Senha deve ter no mínimo 6 caracteres');
    }

    const usuario = await UserRepository.findById(id);
    if (!usuario) {
      throw new Error('Usuário não encontrado');
    }

    if (dados.email && dados.email !== usuario.email) {
      const usuarioExistente = await UserRepository.findByEmail(dados.email);
      if (usuarioExistente) {
        throw new Error('Email já cadastrado');
      }
    }

    // Criptografar senha se fornecida
    if (dados.senha) {
      dados.senha = await bcrypt.hash(dados.senha, 10);
    }

    await UserRepository.update(id, dados);
    
    const usuarioAtualizado = await UserRepository.findById(id);
    return usuarioAtualizado;
  }

  // ... outros métodos
}

module.exports = UserService;
```

#### 💻 Exercício 2: Implementar Autenticação JWT (50 min)

**Instalar:**
```bash
npm install jsonwebtoken dotenv
```

**Criar:** `.env`
```
PORT=3000
JWT_SECRET=meetstranger_secret_key_2024
DB_PATH=./database/meetstranger.db
NODE_ENV=development
```

**Criar:** `.env.example`
```
PORT=3000
JWT_SECRET=sua_chave_secreta_aqui
DB_PATH=./database/meetstranger.db
NODE_ENV=development
```

**Atualizar:** `src/config/database.js`

```javascript
require('dotenv').config();
const sqlite3 = require('sqlite3').verbose();
const path = require('path');

const dbPath = path.resolve(__dirname, '../../', process.env.DB_PATH || 'database/meetstranger.db');

const db = new sqlite3.Database(dbPath, (err) => {
  if (err) {
    console.error('Erro ao conectar ao banco:', err.message);
  } else {
    console.log('Conectado ao banco de dados SQLite');
  }
});

module.exports = db;
```

**Criar:** `src/services/AuthService.js`

```javascript
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');
const UserRepository = require('../repositories/UserRepository');

class AuthService {
  static async login(email, senha) {
    if (!email || !senha) {
      throw new Error('Email e senha são obrigatórios');
    }

    // Buscar usuário (incluindo senha)
    const usuario = await UserRepository.findByEmail(email);
    
    if (!usuario) {
      throw new Error('Credenciais inválidas');
    }

    // Verificar senha
    const senhaValida = await bcrypt.compare(senha, usuario.senha);
    
    if (!senhaValida) {
      throw new Error('Credenciais inválidas');
    }

    // Gerar token
    const token = jwt.sign(
      { id: usuario.id, email: usuario.email },
      process.env.JWT_SECRET,
      { expiresIn: '24h' }
    );

    // Atualizar último login
    await UserRepository.updateLogin(usuario.id);

    return {
      token,
      usuario: {
        id: usuario.id,
        username: usuario.username,
        email: usuario.email
      }
    };
  }

  static async verificarToken(token) {
    try {
      const decoded = jwt.verify(token, process.env.JWT_SECRET);
      return decoded;
    } catch (erro) {
      throw new Error('Token inválido ou expirado');
    }
  }
}

module.exports = AuthService;
```

**Criar:** `src/controllers/AuthController.js`

```javascript
const AuthService = require('../services/AuthService');
const { AppError, asyncHandler } = require('../middleware/errorMiddleware');

class AuthController {
  static login = asyncHandler(async (req, res) => {
    const { email, senha } = req.body;

    if (!email || !senha) {
      throw new AppError('Email e senha são obrigatórios', 400);
    }

    try {
      const resultado = await AuthService.login(email, senha);
      return res.status(200).json(resultado);
    } catch (erro) {
      if (erro.message === 'Credenciais inválidas') {
        throw new AppError(erro.message, 401);
      }
      throw new AppError('Erro ao fazer login', 500);
    }
  });
}

module.exports = AuthController;
```

**Criar:** `src/routes/authRoutes.js`

```javascript
const express = require('express');
const AuthController = require('../controllers/AuthController');

const router = express.Router();

router.post('/login', AuthController.login);

module.exports = router;
```

**Adicionar método no UserRepository:**

```javascript
static updateLogin(id) {
  return new Promise((resolve, reject) => {
    const sql = `UPDATE usuarios SET ultimo_login = CURRENT_TIMESTAMP, online = 1 WHERE id = ?`;
    
    db.run(sql, [id], function(err) {
      if (err) return reject(err);
      resolve({ changes: this.changes });
    });
  });
}
```

#### 💻 Exercício 3: Criar Middleware de Autenticação (30 min)

**Criar:** `src/middleware/authMiddleware.js`

```javascript
const jwt = require('jsonwebtoken');
const { AppError } = require('./errorMiddleware');

const authMiddleware = (req, res, next) => {
  try {
    const authHeader = req.headers.authorization;

    if (!authHeader) {
      throw new AppError('Token não fornecido', 401);
    }

    const parts = authHeader.split(' ');

    if (parts.length !== 2) {
      throw new AppError('Token mal formatado', 401);
    }

    const [scheme, token] = parts;

    if (!/^Bearer$/i.test(scheme)) {
      throw new AppError('Token mal formatado', 401);
    }

    jwt.verify(token, process.env.JWT_SECRET, (err, decoded) => {
      if (err) {
        throw new AppError('Token inválido ou expirado', 401);
      }

      req.userId = decoded.id;
      req.userEmail = decoded.email;
      return next();
    });
  } catch (erro) {
    next(erro);
  }
};

module.exports = authMiddleware;
```

**Proteger rotas:** `src/routes/userRoutes.js`

```javascript
const express = require('express');
const UserController = require('../controllers/UserController');
const authMiddleware = require('../middleware/authMiddleware');

const router = express.Router();

router.post('/', UserController.create);           // Público
router.get('/', authMiddleware, UserController.getAll);        // Protegido
router.get('/:id', authMiddleware, UserController.getById);    // Protegido
router.put('/:id', authMiddleware, UserController.update);     // Protegido
router.delete('/:id', authMiddleware, UserController.delete);  // Protegido

module.exports = router;
```

**Atualizar:** `src/app.js`

```javascript
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const { errorHandler } = require('./middleware/errorMiddleware');

const authRoutes = require('./routes/authRoutes');
const userRoutes = require('./routes/userRoutes');
const categoriaRoutes = require('./routes/categoriaRoutes');

const app = express();

app.use(cors());
app.use(express.json());

// Rotas
app.use('/auth', authRoutes);
app.use('/usuarios', userRoutes);
app.use('/categorias', categoriaRoutes);

// Rota não encontrada
app.use((req, res) => {
  res.status(404).json({ erro: 'Rota não encontrada' });
});

// Middleware de erro
app.use(errorHandler);

module.exports = app;
```

**Atualizar:** `src/server.js`

```javascript
require('dotenv').config();
const app = require('./app');

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Servidor rodando na porta ${PORT}`);
});
```

#### 💻 Exercício 4: Configurar Git (30 min)

**Criar:** `.gitignore`

```
# Dependencies
node_modules/

# Environment
.env

# Database
database/*.db
database/*.db-journal

# Logs
logs/
*.log

# OS
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
```

**Inicializar Git:**

```bash
git init
git add .
git commit -m "feat: configuração inicial do projeto"
```

**Criar branches:**

```bash
git branch develop
git checkout develop
git checkout -b feature/authentication
```

#### 💻 Exercício 5: Documentar API com Swagger (40 min)

**Instalar:**
```bash
npm install swagger-ui-express swagger-jsdoc
```

**Criar:** `src/config/swagger.js`

```javascript
const swaggerJsdoc = require('swagger-jsdoc');

const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'MeetStranger API',
      version: '1.0.0',
      description: 'API do aplicativo MeetStranger - Chat anônimo por categorias',
      contact: {
        name: 'Equipe MeetStranger',
        email: 'contato@meetstranger.com'
      }
    },
    servers: [
      {
        url: 'http://localhost:3000',
        description: 'Servidor de desenvolvimento'
      }
    ],
    components: {
      securitySchemes: {
        bearerAuth: {
          type: 'http',
          scheme: 'bearer',
          bearerFormat: 'JWT'
        }
      }
    }
  },
  apis: ['./src/routes/*.js']
};

const specs = swaggerJsdoc(options);

module.exports = specs;
```

**Atualizar:** `src/app.js`

```javascript
const swaggerUi = require('swagger-ui-express');
const swaggerSpecs = require('./config/swagger');

// ... outras configurações ...

// Documentação
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpecs));

// ... rotas ...
```

**Documentar rotas:** `src/routes/authRoutes.js`

```javascript
/**
 * @swagger
 * /auth/login:
 *   post:
 *     summary: Fazer login
 *     tags: [Autenticação]
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             required:
 *               - email
 *               - senha
 *             properties:
 *               email:
 *                 type: string
 *                 example: maria@email.com
 *               senha:
 *                 type: string
 *                 example: senha123
 *     responses:
 *       200:
 *         description: Login realizado com sucesso
 *         content:
 *           application/json:
 *             schema:
 *               type: object
 *               properties:
 *                 token:
 *                   type: string
 *                 usuario:
 *                   type: object
 *                   properties:
 *                     id:
 *                       type: integer
 *                     username:
 *                       type: string
 *                     email:
 *                       type: string
 *       401:
 *         description: Credenciais inválidas
 */
router.post('/login', AuthController.login);
```

**Documentar:** `src/routes/userRoutes.js`

```javascript
/**
 * @swagger
 * /usuarios:
 *   post:
 *     summary: Criar novo usuário
 *     tags: [Usuários]
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             required:
 *               - username
 *               - email
 *               - senha
 *             properties:
 *               username:
 *                 type: string
 *                 example: maria123
 *               email:
 *                 type: string
 *                 example: maria@email.com
 *               senha:
 *                 type: string
 *                 example: senha123
 *     responses:
 *       201:
 *         description: Usuário criado com sucesso
 *       409:
 *         description: Email ou username já cadastrado
 *   get:
 *     summary: Listar todos os usuários
 *     tags: [Usuários]
 *     security:
 *       - bearerAuth: []
 *     responses:
 *       200:
 *         description: Lista de usuários
 *       401:
 *         description: Token não fornecido ou inválido
 */
```

---

### 4️⃣ Prática Autônoma (120 min)

#### 🎯 Desafio 1: Testar Autenticação (30 min)

**Testes:**

```bash
# 1. Criar usuário
POST http://localhost:3000/usuarios
Body: { "username": "teste", "email": "teste@email.com", "senha": "123456" }
Esperado: 201

# 2. Fazer login
POST http://localhost:3000/auth/login
Body: { "email": "teste@email.com", "senha": "123456" }
Esperado: 200 + token

# 3. Login com senha errada
POST http://localhost:3000/auth/login
Body: { "email": "teste@email.com", "senha": "errada" }
Esperado: 401

# 4. Acessar rota protegida sem token
GET http://localhost:3000/usuarios
Esperado: 401

# 5. Acessar rota protegida com token
GET http://localhost:3000/usuarios
Headers: Authorization: Bearer {TOKEN}
Esperado: 200

# 6. Acessar com token inválido
GET http://localhost:3000/usuarios
Headers: Authorization: Bearer token_invalido
Esperado: 401
```

#### 🎯 Desafio 2: Criar README.md (40 min)

**Criar:** `README.md`

```markdown
# MeetStranger API

API REST para o aplicativo MeetStranger - plataforma de chat anônimo por categorias de interesse.

## 🚀 Tecnologias

- Node.js
- Express
- SQLite3
- JWT (autenticação)
- Bcrypt (criptografia)
- Swagger (documentação)

## 📋 Pré-requisitos

- Node.js 14+
- NPM ou Yarn

## 🔧 Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/meetstranger-api.git

# Entre na pasta
cd meetstranger-api

# Instale as dependências
npm install

# Configure as variáveis de ambiente
cp .env.example .env

# Crie o banco de dados
node database/init.js

# Inicie o servidor
npm start
```

## ⚙️ Variáveis de Ambiente

```
PORT=3000
JWT_SECRET=sua_chave_secreta
DB_PATH=./database/meetstranger.db
NODE_ENV=development
```

## 📚 Documentação

Acesse a documentação interativa em: `http://localhost:3000/api-docs`

## 🔐 Autenticação

A API usa JWT para autenticação. Para acessar rotas protegidas:

1. Faça login em `/auth/login`
2. Copie o token retornado
3. Envie o token no header: `Authorization: Bearer {token}`

## 📡 Endpoints

### Autenticação

- `POST /auth/login` - Fazer login

### Usuários

- `POST /usuarios` - Criar usuário (público)
- `GET /usuarios` - Listar usuários (protegido)
- `GET /usuarios/:id` - Buscar usuário (protegido)
- `PUT /usuarios/:id` - Atualizar usuário (protegido)
- `DELETE /usuarios/:id` - Deletar usuário (protegido)

### Categorias

- `GET /categorias` - Listar categorias (público)
- `GET /categorias/:id` - Buscar categoria (público)
- `POST /categorias` - Criar categoria (protegido)
- `PUT /categorias/:id` - Atualizar categoria (protegido)
- `DELETE /categorias/:id` - Deletar categoria (protegido)

## 🧪 Testes

```bash
# Executar testes
npm test
```

## 📦 Estrutura do Projeto

```
src/
├── config/          # Configurações (database, swagger)
├── controllers/     # Controladores
├── services/        # Lógica de negócio
├── repositories/    # Acesso ao banco
├── middleware/      # Middlewares (auth, error)
├── routes/          # Rotas
├── app.js           # Configuração do Express
└── server.js        # Inicialização do servidor
```

## 👥 Autores

- Equipe MeetStranger

## 📄 Licença

Este projeto está sob a licença MIT.
```

#### 🎯 Desafio 3: Documentar Todas as Rotas no Swagger (50 min)

**Tarefa:** Adicionar documentação Swagger para:
- GET /usuarios/:id
- PUT /usuarios/:id
- DELETE /usuarios/:id
- Todas as rotas de categorias

**Checklist:**
- [ ] Todas as rotas documentadas
- [ ] Exemplos de request/response
- [ ] Códigos de status corretos
- [ ] Autenticação indicada

---

### 5️⃣ Síntese (60 min)

#### 📝 Revisão dos Conceitos

**Perguntas para a Turma:**

1. **Por que criptografar senhas?**
   - Proteger dados em caso de vazamento

2. **Como funciona JWT?**
   - Token assinado que identifica o usuário

3. **O que é CORS?**
   - Política de segurança para requisições cross-origin

4. **Por que usar .env?**
   - Não expor credenciais no código

#### 🎯 Fluxo de Autenticação

```
1. POST /auth/login
   ↓
2. Validar credenciais
   ↓
3. Gerar JWT
   ↓
4. Retornar token
   ↓
5. Cliente armazena token
   ↓
6. GET /usuarios (Header: Authorization: Bearer token)
   ↓
7. authMiddleware valida token
   ↓
8. Processar requisição
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Criptografar senhas com bcrypt
- [ ] Gerar e validar JWT
- [ ] Criar middleware de autenticação
- [ ] Proteger rotas
- [ ] Configurar CORS
- [ ] Usar variáveis de ambiente
- [ ] Usar Git básico
- [ ] Documentar API com Swagger
- [ ] Criar README profissional

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar refresh token
   - Implementar logout
   - Adicionar rate limiting

2. **Estudo:**
   - Pesquisar sobre OAuth2
   - Estudar HTTPS

---

## 📊 Avaliação

### Critérios de Avaliação (Peso: 15% da UC 02 Part 03)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Segurança** | 40% | Bcrypt, JWT, proteção de rotas |
| **Versionamento** | 20% | Git configurado, commits |
| **Documentação** | 40% | Swagger completo, README |

### Instrumentos de Avaliação

1. **Testes de autenticação** (somativa - 40%)
2. **README.md** (somativa - 30%)
3. **Documentação Swagger** (somativa - 30%)

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar JWT e bcrypt
- [ ] Preparar exemplos de tokens
- [ ] Revisar Git básico
- [ ] Ter Swagger configurado

### Durante a Aula
- [ ] Demonstrar login ao vivo
- [ ] Mostrar token no Postman
- [ ] Explicar estrutura do JWT
- [ ] Circular durante documentação

### Pontos de Atenção
- ⚠️ Alunos esquecem Bearer no header
- ⚠️ Confusão entre hash e criptografia
- ⚠️ Não entendem expiração de token
- ⚠️ Dificuldade com sintaxe Swagger

---

## 📝 Anotações do Professor

```
Data: ____/____/____

Pontos positivos:


Dificuldades identificadas:
```

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
