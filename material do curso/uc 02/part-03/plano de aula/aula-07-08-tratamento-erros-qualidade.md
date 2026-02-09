# Aula 07-08 - Tratamento de Erros, Depuração e Qualidade

**Carga Horária:** 8 horas  
**Modalidade:** Presencial  
**Competências:** Tratamento de erros, debugging e boas práticas

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Implementar tratamento de erros centralizado no Express
- ✅ Criar middleware de erro customizado
- ✅ Utilizar ferramentas de debugging do VS Code
- ✅ Implementar logging de erros
- ✅ Aplicar boas práticas de código
- ✅ Refatorar código para async/await
- ✅ Validar dados de entrada adequadamente

---

## 📚 Conteúdo Programático

### 1. Tratamento de Erros no Express
- Try-catch em rotas assíncronas
- Middleware de erro
- Tipos de erro (4xx vs 5xx)
- Mensagens de erro padronizadas

### 2. Depuração
- Breakpoints no VS Code
- Debug console
- Inspeção de variáveis
- Call stack

### 3. Logging
- Console.log vs logger profissional
- Níveis de log (error, warn, info, debug)
- Registro de erros

### 4. Qualidade de Código
- Nomenclatura clara
- Funções pequenas e focadas
- DRY (Don't Repeat Yourself)
- Comentários úteis

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- CRUD completo (CREATE, READ, UPDATE, DELETE)
- Validações e regras de negócio
- Integridade referencial

**Atividade de Aquecimento:**
```
Discussão:
- O que acontece quando o banco de dados está offline?
- Como saber onde está o erro no código?
- Por que alguns erros retornam 500 e outros 400?

Objetivo: Preparar para tratamento de erros
```

**Checkpoint:**
- Listar tipos de erro que já encontraram
- Discutir como trataram esses erros

---

### 2️⃣ Apresentação (90 min)

#### 📖 Parte 1: Tipos de Erro (20 min)

**Classificação de Erros:**

**Erros do Cliente (4xx):**
- 400 Bad Request: Dados inválidos
- 401 Unauthorized: Não autenticado
- 403 Forbidden: Sem permissão
- 404 Not Found: Recurso não existe
- 409 Conflict: Conflito de dados

**Erros do Servidor (5xx):**
- 500 Internal Server Error: Erro não tratado
- 503 Service Unavailable: Serviço indisponível

**Exemplo de Classificação:**
```javascript
// 400 - Cliente enviou dados errados
{ "username": "" }  // username vazio

// 404 - Recurso não existe
GET /usuarios/999  // usuário não existe

// 409 - Conflito
{ "email": "existente@email.com" }  // email já cadastrado

// 500 - Erro do servidor
Banco de dados offline
Erro de sintaxe no código
```

#### 📖 Parte 2: Middleware de Erro (25 min)

**Estrutura de Middleware de Erro:**

```javascript
// src/middleware/errorMiddleware.js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.isOperational = true;
    Error.captureStackTrace(this, this.constructor);
  }
}

const errorHandler = (err, req, res, next) => {
  let statusCode = err.statusCode || 500;
  let message = err.message || 'Erro interno do servidor';

  // Log do erro
  console.error(`[ERRO] ${statusCode} - ${message}`);
  console.error(err.stack);

  // Resposta ao cliente
  res.status(statusCode).json({
    erro: message,
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
  });
};

module.exports = { AppError, errorHandler };
```

**Uso no Controller:**
```javascript
const { AppError } = require('../middleware/errorMiddleware');

static async getById(req, res, next) {
  try {
    const { id } = req.params;
    
    UserService.findById(parseInt(id), (err, usuario) => {
      if (err) {
        if (err.message === 'Usuário não encontrado') {
          return next(new AppError(err.message, 404));
        }
        return next(new AppError('Erro ao buscar usuário', 500));
      }
      
      return res.status(200).json(usuario);
    });
  } catch (erro) {
    next(erro);
  }
}
```

**Registrar no app.js:**
```javascript
const { errorHandler } = require('./middleware/errorMiddleware');

// ... rotas ...

// Middleware de erro (sempre por último)
app.use(errorHandler);
```

#### 📖 Parte 3: Async/Await (25 min)

**Problema com Callbacks:**
```javascript
// Callback hell
UserRepository.findById(id, (err, usuario) => {
  if (err) return callback(err);
  
  UserRepository.countSalasAtivas(id, (err, total) => {
    if (err) return callback(err);
    
    if (total > 0) {
      return callback(new Error('Usuário tem salas ativas'));
    }
    
    UserRepository.delete(id, (err) => {
      if (err) return callback(err);
      callback(null);
    });
  });
});
```

**Solução com Promises:**
```javascript
// Converter callback para Promise
static findById(id) {
  return new Promise((resolve, reject) => {
    const sql = `SELECT * FROM usuarios WHERE id = ?`;
    db.get(sql, [id], (err, row) => {
      if (err) return reject(err);
      resolve(row);
    });
  });
}
```

**Usar com Async/Await:**
```javascript
static async delete(id) {
  const usuario = await UserRepository.findById(id);
  
  if (!usuario) {
    throw new Error('Usuário não encontrado');
  }
  
  const total = await UserRepository.countSalasAtivas(id);
  
  if (total > 0) {
    throw new Error('Usuário tem salas ativas');
  }
  
  await UserRepository.delete(id);
}
```

#### 📖 Parte 4: Debugging no VS Code (20 min)

**Configurar Debug:**

```json
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Backend",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}/src/server.js",
      "restart": true,
      "console": "integratedTerminal"
    }
  ]
}
```

**Usar Breakpoints:**
1. Clicar na margem esquerda do editor (bolinha vermelha)
2. Iniciar debug (F5)
3. Fazer requisição HTTP
4. Código para no breakpoint
5. Inspecionar variáveis
6. Avançar linha por linha (F10)

---

### 3️⃣ Prática Guiada (180 min)

#### 💻 Exercício 1: Criar Middleware de Erro (40 min)

**Arquivo:** `src/middleware/errorMiddleware.js`

```javascript
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.isOperational = true;
    Error.captureStackTrace(this, this.constructor);
  }
}

const errorHandler = (err, req, res, next) => {
  let statusCode = err.statusCode || 500;
  let message = err.message || 'Erro interno do servidor';

  // Log detalhado
  const timestamp = new Date().toISOString();
  console.error(`[${timestamp}] ${req.method} ${req.path} - ${statusCode}`);
  console.error(`Mensagem: ${message}`);
  if (err.stack) {
    console.error(`Stack: ${err.stack}`);
  }

  // Resposta ao cliente
  res.status(statusCode).json({
    erro: message,
    timestamp,
    path: req.path
  });
};

const asyncHandler = (fn) => {
  return (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
};

module.exports = { AppError, errorHandler, asyncHandler };
```

**Atualizar:** `src/app.js`

```javascript
const express = require('express');
const { errorHandler } = require('./middleware/errorMiddleware');

const userRoutes = require('./routes/userRoutes');
const categoriaRoutes = require('./routes/categoriaRoutes');

const app = express();

app.use(express.json());

// Rotas
app.use('/usuarios', userRoutes);
app.use('/categorias', categoriaRoutes);

// Rota não encontrada
app.use((req, res) => {
  res.status(404).json({ erro: 'Rota não encontrada' });
});

// Middleware de erro (sempre por último)
app.use(errorHandler);

module.exports = app;
```

#### 💻 Exercício 2: Refatorar Repository para Promises (50 min)

**Arquivo:** `src/repositories/UserRepository.js`

```javascript
const db = require('../config/database');

class UserRepository {
  static create(dados) {
    return new Promise((resolve, reject) => {
      const sql = `INSERT INTO usuarios (username, email, senha) VALUES (?, ?, ?)`;
      const params = [dados.username, dados.email, dados.senha];
      
      db.run(sql, params, function(err) {
        if (err) return reject(err);
        resolve({ id: this.lastID });
      });
    });
  }

  static findAll() {
    return new Promise((resolve, reject) => {
      const sql = `SELECT id, username, email, criado_em, ultimo_login, online FROM usuarios`;
      
      db.all(sql, [], (err, rows) => {
        if (err) return reject(err);
        resolve(rows);
      });
    });
  }

  static findById(id) {
    return new Promise((resolve, reject) => {
      const sql = `SELECT id, username, email, criado_em, ultimo_login, online FROM usuarios WHERE id = ?`;
      
      db.get(sql, [id], (err, row) => {
        if (err) return reject(err);
        resolve(row);
      });
    });
  }

  static findByEmail(email) {
    return new Promise((resolve, reject) => {
      const sql = `SELECT id, username, email, senha, criado_em, ultimo_login, online FROM usuarios WHERE email = ?`;
      
      db.get(sql, [email], (err, row) => {
        if (err) return reject(err);
        resolve(row);
      });
    });
  }

  static update(id, dados) {
    return new Promise((resolve, reject) => {
      const campos = [];
      const valores = [];
      
      if (dados.username !== undefined) {
        campos.push('username = ?');
        valores.push(dados.username);
      }
      if (dados.email !== undefined) {
        campos.push('email = ?');
        valores.push(dados.email);
      }
      if (dados.senha !== undefined) {
        campos.push('senha = ?');
        valores.push(dados.senha);
      }
      
      if (campos.length === 0) {
        return reject(new Error('Nenhum campo para atualizar'));
      }
      
      valores.push(id);
      const sql = `UPDATE usuarios SET ${campos.join(', ')} WHERE id = ?`;
      
      db.run(sql, valores, function(err) {
        if (err) return reject(err);
        if (this.changes === 0) {
          return reject(new Error('Usuário não encontrado'));
        }
        resolve({ changes: this.changes });
      });
    });
  }

  static delete(id) {
    return new Promise((resolve, reject) => {
      const sql = `DELETE FROM usuarios WHERE id = ?`;
      
      db.run(sql, [id], function(err) {
        if (err) return reject(err);
        if (this.changes === 0) {
          return reject(new Error('Usuário não encontrado'));
        }
        resolve({ changes: this.changes });
      });
    });
  }

  static countSalasAtivas(id) {
    return new Promise((resolve, reject) => {
      const sql = `
        SELECT COUNT(*) as total 
        FROM salas 
        WHERE (usuario1_id = ? OR usuario2_id = ?) 
        AND ativa = 1
      `;
      
      db.get(sql, [id, id], (err, row) => {
        if (err) return reject(err);
        resolve(row.total);
      });
    });
  }
}

module.exports = UserRepository;
```

#### 💻 Exercício 3: Refatorar Service para Async/Await (40 min)

**Arquivo:** `src/services/UserService.js`

```javascript
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

    // Criar usuário
    const resultado = await UserRepository.create(dados);
    
    // Buscar usuário criado
    const usuario = await UserRepository.findById(resultado.id);
    return usuario;
  }

  static async findAll() {
    const usuarios = await UserRepository.findAll();
    return usuarios;
  }

  static async findById(id) {
    const usuario = await UserRepository.findById(id);
    
    if (!usuario) {
      throw new Error('Usuário não encontrado');
    }
    
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

    // Verificar se usuário existe
    const usuario = await UserRepository.findById(id);
    if (!usuario) {
      throw new Error('Usuário não encontrado');
    }

    // Se está alterando email, verificar duplicação
    if (dados.email && dados.email !== usuario.email) {
      const usuarioExistente = await UserRepository.findByEmail(dados.email);
      if (usuarioExistente) {
        throw new Error('Email já cadastrado');
      }
    }

    // Atualizar
    await UserRepository.update(id, dados);
    
    // Buscar usuário atualizado
    const usuarioAtualizado = await UserRepository.findById(id);
    return usuarioAtualizado;
  }

  static async delete(id) {
    // Verificar se usuário existe
    const usuario = await UserRepository.findById(id);
    if (!usuario) {
      throw new Error('Usuário não encontrado');
    }

    // Verificar se tem salas ativas
    const total = await UserRepository.countSalasAtivas(id);
    if (total > 0) {
      throw new Error('Não é possível deletar usuário com salas ativas');
    }

    // Deletar
    await UserRepository.delete(id);
  }
}

module.exports = UserService;
```

#### 💻 Exercício 4: Refatorar Controller (50 min)

**Arquivo:** `src/controllers/UserController.js`

```javascript
const UserService = require('../services/UserService');
const { AppError, asyncHandler } = require('../middleware/errorMiddleware');

class UserController {
  static create = asyncHandler(async (req, res) => {
    const { username, email, senha } = req.body;

    if (!username || !email || !senha) {
      throw new AppError('Campos obrigatórios: username, email, senha', 400);
    }

    try {
      const usuario = await UserService.create({ username, email, senha });
      return res.status(201).json(usuario);
    } catch (erro) {
      if (erro.message.includes('já cadastrado')) {
        throw new AppError(erro.message, 409);
      }
      if (erro.message.includes('inválido') || erro.message.includes('mínimo')) {
        throw new AppError(erro.message, 400);
      }
      if (erro.message.includes('UNIQUE constraint')) {
        throw new AppError('Username já cadastrado', 409);
      }
      throw new AppError('Erro ao criar usuário', 500);
    }
  });

  static getAll = asyncHandler(async (req, res) => {
    const usuarios = await UserService.findAll();
    return res.status(200).json(usuarios);
  });

  static getById = asyncHandler(async (req, res) => {
    const { id } = req.params;

    try {
      const usuario = await UserService.findById(parseInt(id));
      return res.status(200).json(usuario);
    } catch (erro) {
      if (erro.message === 'Usuário não encontrado') {
        throw new AppError(erro.message, 404);
      }
      throw new AppError('Erro ao buscar usuário', 500);
    }
  });

  static update = asyncHandler(async (req, res) => {
    const { id } = req.params;
    const { username, email, senha } = req.body;

    const dados = {};
    if (username) dados.username = username;
    if (email) dados.email = email;
    if (senha) dados.senha = senha;

    if (Object.keys(dados).length === 0) {
      throw new AppError('Nenhum campo para atualizar', 400);
    }

    try {
      const usuario = await UserService.update(parseInt(id), dados);
      return res.status(200).json(usuario);
    } catch (erro) {
      if (erro.message === 'Usuário não encontrado') {
        throw new AppError(erro.message, 404);
      }
      if (erro.message.includes('já cadastrado')) {
        throw new AppError(erro.message, 409);
      }
      if (erro.message.includes('inválido') || erro.message.includes('mínimo')) {
        throw new AppError(erro.message, 400);
      }
      throw new AppError('Erro ao atualizar usuário', 500);
    }
  });

  static delete = asyncHandler(async (req, res) => {
    const { id } = req.params;

    try {
      await UserService.delete(parseInt(id));
      return res.status(204).send();
    } catch (erro) {
      if (erro.message === 'Usuário não encontrado') {
        throw new AppError(erro.message, 404);
      }
      if (erro.message.includes('salas ativas')) {
        throw new AppError(erro.message, 400);
      }
      throw new AppError('Erro ao deletar usuário', 500);
    }
  });
}

module.exports = UserController;
```

---

### 4️⃣ Prática Autônoma (120 min)

#### 🎯 Desafio 1: Refatorar CategoriaRepository, Service e Controller (60 min)

**Tarefa:** Aplicar mesmas refatorações para categorias

**Checklist:**
- [ ] CategoriaRepository com Promises
- [ ] CategoriaService com async/await
- [ ] CategoriaController com asyncHandler
- [ ] Tratamento de erros com AppError
- [ ] Testes realizados

#### 🎯 Desafio 2: Criar Middleware de Validação (30 min)

**Arquivo:** `src/middleware/validationMiddleware.js`

```javascript
const { AppError } = require('./errorMiddleware');

const validateUser = (req, res, next) => {
  const { username, email, senha } = req.body;

  if (!username || !email || !senha) {
    throw new AppError('Campos obrigatórios: username, email, senha', 400);
  }

  if (username.length < 3) {
    throw new AppError('Username deve ter no mínimo 3 caracteres', 400);
  }

  if (!email.includes('@')) {
    throw new AppError('Email inválido', 400);
  }

  if (senha.length < 6) {
    throw new AppError('Senha deve ter no mínimo 6 caracteres', 400);
  }

  next();
};

const validateCategoria = (req, res, next) => {
  const { nome } = req.body;

  if (!nome || nome.trim() === '') {
    throw new AppError('Campo obrigatório: nome', 400);
  }

  next();
};

module.exports = { validateUser, validateCategoria };
```

**Usar nas rotas:**
```javascript
const { validateUser } = require('../middleware/validationMiddleware');

router.post('/', validateUser, UserController.create);
```

#### 🎯 Desafio 3: Debugging com Breakpoints (30 min)

**Tarefa:** Usar VS Code debugger para encontrar bugs

**Cenários:**

1. **Bug: Email duplicado não está sendo detectado**
   - Colocar breakpoint em UserService.create
   - Verificar se findByEmail está retornando dados
   - Inspecionar variável usuarioExistente

2. **Bug: DELETE retorna 500 em vez de 404**
   - Colocar breakpoint em UserController.delete
   - Verificar fluxo de erro
   - Corrigir tratamento de erro

3. **Bug: UPDATE não valida email duplicado**
   - Colocar breakpoint em UserService.update
   - Verificar condição de email
   - Testar com dados duplicados

---

### 5️⃣ Síntese (60 min)

#### 📝 Revisão dos Conceitos

**Perguntas para a Turma:**

1. **Qual a vantagem de async/await sobre callbacks?**
   - Código mais limpo, evita callback hell, melhor tratamento de erros

2. **Por que usar middleware de erro centralizado?**
   - Padronização, menos código repetido, logging centralizado

3. **Quando usar 400 vs 500?**
   - 400: erro do cliente / 500: erro do servidor

4. **Como usar breakpoints?**
   - Clicar na margem, F5 para debug, F10 para próxima linha

#### 🎯 Fluxo de Erro

```
Controller
    ↓ throw new AppError('Mensagem', 404)
Express
    ↓ next(erro)
errorMiddleware
    ↓ log do erro
    ↓ res.status(404).json({ erro: 'Mensagem' })
Cliente
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Criar middleware de erro customizado
- [ ] Usar async/await
- [ ] Converter callbacks para Promises
- [ ] Usar asyncHandler
- [ ] Classificar erros (4xx vs 5xx)
- [ ] Usar debugger do VS Code
- [ ] Criar middleware de validação

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar logging em arquivo (não apenas console)
   - Criar middleware de validação para UPDATE
   - Implementar rate limiting

2. **Estudo:**
   - Pesquisar sobre Winston (logger)
   - Estudar try-catch best practices

---

## 📊 Avaliação

### Critérios de Avaliação (Peso: 15% da UC 02 Part 03)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Middleware de Erro** | 25% | Implementação correta |
| **Async/Await** | 30% | Refatoração completa |
| **Tratamento de Erros** | 25% | Classificação correta |
| **Debugging** | 20% | Uso de breakpoints |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar debugger do VS Code
- [ ] Preparar cenários de erro
- [ ] Revisar async/await
- [ ] Ter código bugado pronto

### Durante a Aula
- [ ] Demonstrar debugging ao vivo
- [ ] Mostrar callback hell vs async/await
- [ ] Simular erros de banco
- [ ] Circular durante debugging

### Pontos de Atenção
- ⚠️ Alunos esquecem try-catch em async
- ⚠️ Confusão entre throw e return
- ⚠️ Não entendem Promise.resolve
- ⚠️ Dificuldade com debugger

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
