# Aula 05 - Integração com Banco de Dados e CRUD (Parte 1)

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Integração de backend com banco de dados relacional

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Conectar aplicação Node.js ao banco de dados SQLite
- ✅ Implementar arquitetura em camadas (Controller → Service → Repository)
- ✅ Executar operações CREATE no banco de dados
- ✅ Executar operações READ (SELECT) no banco de dados
- ✅ Tratar erros de banco de dados adequadamente
- ✅ Implementar cadastro e listagem de usuários com dados reais

---

## 📚 Conteúdo Programático

### 1. Conexão com Banco de Dados
- Instalação do driver SQLite3
- Configuração de conexão
- Pool de conexões

### 2. Arquitetura em Camadas
- Controller: Recebe requisição HTTP
- Service: Regras de negócio
- Repository: Acesso ao banco de dados
- Separação de responsabilidades

### 3. Operações CREATE
- INSERT INTO
- Retorno de ID gerado
- Validação de dados

### 4. Operações READ
- SELECT com filtros
- SELECT por ID
- SELECT com JOIN

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Modelagem de requisitos
- Definição de endpoints REST
- Estrutura de rotas por domínio

**Atividade de Aquecimento:**
```
Discussão:
- Qual a diferença entre dados mockados e dados reais?
- Por que separar lógica de negócio de acesso ao banco?
- O que acontece se o banco estiver offline?

Objetivo: Preparar para arquitetura em camadas
```

**Checkpoint:**
- Revisar estrutura do banco (tabela usuarios)
- Relembrar comandos SQL básicos (INSERT, SELECT)

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Conexão com Banco de Dados (20 min)

**Instalação do SQLite3:**
```bash
npm install sqlite3
```

**Estrutura de Conexão:**

```javascript
// config/database.js
const sqlite3 = require('sqlite3').verbose();
const path = require('path');

const dbPath = path.resolve(__dirname, '../../database/meetstranger.db');

const db = new sqlite3.Database(dbPath, (err) => {
  if (err) {
    console.error('Erro ao conectar ao banco:', err.message);
  } else {
    console.log('Conectado ao banco de dados SQLite');
  }
});

module.exports = db;
```

**Criar estrutura de banco:**
```sql
-- database/schema.sql
CREATE TABLE IF NOT EXISTS usuarios (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  username TEXT NOT NULL UNIQUE,
  email TEXT NOT NULL UNIQUE,
  senha TEXT NOT NULL,
  criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
  ultimo_login DATETIME,
  online BOOLEAN DEFAULT 0
);

CREATE TABLE IF NOT EXISTS categorias (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  nome TEXT NOT NULL,
  descricao TEXT,
  icone TEXT,
  ativa BOOLEAN DEFAULT 1
);

CREATE TABLE IF NOT EXISTS salas (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  categoria_id INTEGER NOT NULL,
  usuario1_id INTEGER NOT NULL,
  usuario2_id INTEGER NOT NULL,
  criada_em DATETIME DEFAULT CURRENT_TIMESTAMP,
  encerrada_em DATETIME,
  ativa BOOLEAN DEFAULT 1,
  FOREIGN KEY (categoria_id) REFERENCES categorias(id),
  FOREIGN KEY (usuario1_id) REFERENCES usuarios(id),
  FOREIGN KEY (usuario2_id) REFERENCES usuarios(id)
);
```

#### 📖 Parte 2: Arquitetura em Camadas (20 min)

**Fluxo de Dados:**

```
Cliente HTTP
    ↓
┌─────────────────┐
│   Controller    │  ← Recebe requisição, valida entrada
└─────────────────┘
    ↓
┌─────────────────┐
│    Service      │  ← Regras de negócio, orquestração
└─────────────────┘
    ↓
┌─────────────────┐
│   Repository    │  ← Acesso direto ao banco de dados
└─────────────────┘
    ↓
  Banco de Dados
```

**Responsabilidades:**

**Controller:**
- Receber req/res
- Validar entrada básica
- Chamar service
- Retornar resposta HTTP

**Service:**
- Validar regras de negócio
- Orquestrar múltiplos repositories
- Tratar erros de negócio
- Retornar dados processados

**Repository:**
- Executar queries SQL
- Mapear resultados
- Tratar erros de banco
- Retornar dados brutos

#### 📖 Parte 3: Operações CREATE e READ (20 min)

**CREATE - INSERT:**
```javascript
// Inserir usuário
const sql = `INSERT INTO usuarios (username, email, senha) VALUES (?, ?, ?)`;
db.run(sql, [username, email, senha], function(err) {
  if (err) return callback(err);
  callback(null, { id: this.lastID });
});
```

**READ - SELECT:**
```javascript
// Buscar todos
const sql = `SELECT * FROM usuarios`;
db.all(sql, [], (err, rows) => {
  if (err) return callback(err);
  callback(null, rows);
});

// Buscar por ID
const sql = `SELECT * FROM usuarios WHERE id = ?`;
db.get(sql, [id], (err, row) => {
  if (err) return callback(err);
  callback(null, row);
});
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Configurar Banco de Dados (20 min)

**Criar estrutura de pastas:**
```bash
mkdir database
mkdir src/repositories
```

**Arquivo:** `database/init.js`

```javascript
const db = require('../src/config/database');

const criarTabelas = () => {
  db.serialize(() => {
    // Tabela usuarios
    db.run(`
      CREATE TABLE IF NOT EXISTS usuarios (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        username TEXT NOT NULL UNIQUE,
        email TEXT NOT NULL UNIQUE,
        senha TEXT NOT NULL,
        criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
        ultimo_login DATETIME,
        online BOOLEAN DEFAULT 0
      )
    `);

    // Tabela categorias
    db.run(`
      CREATE TABLE IF NOT EXISTS categorias (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nome TEXT NOT NULL,
        descricao TEXT,
        icone TEXT,
        ativa BOOLEAN DEFAULT 1
      )
    `);

    // Inserir categorias padrão
    db.run(`
      INSERT OR IGNORE INTO categorias (id, nome, descricao, icone, ativa)
      VALUES 
        (1, 'Filmes', 'Converse sobre cinema', '🎬', 1),
        (2, 'Jogos', 'Converse sobre games', '🎮', 1),
        (3, 'Séries', 'Converse sobre séries', '📺', 1)
    `);

    console.log('Tabelas criadas com sucesso!');
  });
};

criarTabelas();
```

**Executar:**
```bash
node database/init.js
```

#### 💻 Exercício 2: Criar UserRepository (30 min)

**Arquivo:** `src/repositories/UserRepository.js`

```javascript
const db = require('../config/database');

class UserRepository {
  static create(dados, callback) {
    const sql = `INSERT INTO usuarios (username, email, senha) VALUES (?, ?, ?)`;
    const params = [dados.username, dados.email, dados.senha];
    
    db.run(sql, params, function(err) {
      if (err) {
        return callback(err, null);
      }
      callback(null, { id: this.lastID });
    });
  }

  static findAll(callback) {
    const sql = `SELECT id, username, email, criado_em, ultimo_login, online FROM usuarios`;
    
    db.all(sql, [], (err, rows) => {
      if (err) {
        return callback(err, null);
      }
      callback(null, rows);
    });
  }

  static findById(id, callback) {
    const sql = `SELECT id, username, email, criado_em, ultimo_login, online FROM usuarios WHERE id = ?`;
    
    db.get(sql, [id], (err, row) => {
      if (err) {
        return callback(err, null);
      }
      callback(null, row);
    });
  }

  static findByEmail(email, callback) {
    const sql = `SELECT id, username, email, senha, criado_em, ultimo_login, online FROM usuarios WHERE email = ?`;
    
    db.get(sql, [email], (err, row) => {
      if (err) {
        return callback(err, null);
      }
      callback(null, row);
    });
  }

  static findByUsername(username, callback) {
    const sql = `SELECT id, username, email, criado_em, ultimo_login, online FROM usuarios WHERE username = ?`;
    
    db.get(sql, [username], (err, row) => {
      if (err) {
        return callback(err, null);
      }
      callback(null, row);
    });
  }
}

module.exports = UserRepository;
```

**Pontos de Atenção:**
- ✅ Usar prepared statements (?) para prevenir SQL injection
- ✅ Não retornar senha em SELECT (exceto quando necessário)
- ✅ Usar callback pattern para operações assíncronas
- ✅ Tratar erros adequadamente

#### 💻 Exercício 3: Refatorar UserService (20 min)

**Arquivo:** `src/services/UserService.js`

```javascript
const UserRepository = require('../repositories/UserRepository');

class UserService {
  static create(dados, callback) {
    // Validações
    if (!dados.username || dados.username.length < 3) {
      return callback(new Error('Username deve ter no mínimo 3 caracteres'), null);
    }

    if (!dados.email || !dados.email.includes('@')) {
      return callback(new Error('Email inválido'), null);
    }

    if (!dados.senha || dados.senha.length < 6) {
      return callback(new Error('Senha deve ter no mínimo 6 caracteres'), null);
    }

    // Verificar email duplicado
    UserRepository.findByEmail(dados.email, (err, usuario) => {
      if (err) {
        return callback(err, null);
      }

      if (usuario) {
        return callback(new Error('Email já cadastrado'), null);
      }

      // Criar usuário
      UserRepository.create(dados, (err, resultado) => {
        if (err) {
          if (err.message.includes('UNIQUE constraint failed: usuarios.username')) {
            return callback(new Error('Username já cadastrado'), null);
          }
          return callback(err, null);
        }

        // Buscar usuário criado
        UserRepository.findById(resultado.id, callback);
      });
    });
  }

  static findAll(callback) {
    UserRepository.findAll(callback);
  }

  static findById(id, callback) {
    UserRepository.findById(id, (err, usuario) => {
      if (err) {
        return callback(err, null);
      }

      if (!usuario) {
        return callback(new Error('Usuário não encontrado'), null);
      }

      callback(null, usuario);
    });
  }
}

module.exports = UserService;
```

#### 💻 Exercício 4: Refatorar UserController (20 min)

**Arquivo:** `src/controllers/UserController.js`

```javascript
const UserService = require('../services/UserService');

class UserController {
  static async create(req, res) {
    const { username, email, senha } = req.body;

    if (!username || !email || !senha) {
      return res.status(400).json({ 
        erro: 'Campos obrigatórios: username, email, senha' 
      });
    }

    UserService.create({ username, email, senha }, (err, usuario) => {
      if (err) {
        if (err.message.includes('já cadastrado')) {
          return res.status(409).json({ erro: err.message });
        }
        if (err.message.includes('inválido') || err.message.includes('mínimo')) {
          return res.status(400).json({ erro: err.message });
        }
        return res.status(500).json({ erro: 'Erro ao criar usuário' });
      }

      return res.status(201).json(usuario);
    });
  }

  static async getAll(req, res) {
    UserService.findAll((err, usuarios) => {
      if (err) {
        return res.status(500).json({ erro: 'Erro ao buscar usuários' });
      }

      return res.status(200).json(usuarios);
    });
  }

  static async getById(req, res) {
    const { id } = req.params;

    UserService.findById(parseInt(id), (err, usuario) => {
      if (err) {
        if (err.message === 'Usuário não encontrado') {
          return res.status(404).json({ erro: err.message });
        }
        return res.status(500).json({ erro: 'Erro ao buscar usuário' });
      }

      return res.status(200).json(usuario);
    });
  }
}

module.exports = UserController;
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Implementar CategoriaRepository e Service (40 min)

**Tarefa:** Criar camada completa para categorias

**CategoriaRepository.js:**
```javascript
const db = require('../config/database');

class CategoriaRepository {
  static create(dados, callback) {
    const sql = `INSERT INTO categorias (nome, descricao, icone) VALUES (?, ?, ?)`;
    const params = [dados.nome, dados.descricao || '', dados.icone || '📁'];
    
    db.run(sql, params, function(err) {
      if (err) return callback(err, null);
      callback(null, { id: this.lastID });
    });
  }

  static findAll(callback) {
    const sql = `SELECT * FROM categorias`;
    db.all(sql, [], (err, rows) => {
      if (err) return callback(err, null);
      callback(null, rows);
    });
  }

  static findById(id, callback) {
    const sql = `SELECT * FROM categorias WHERE id = ?`;
    db.get(sql, [id], (err, row) => {
      if (err) return callback(err, null);
      callback(null, row);
    });
  }

  static findAtivas(callback) {
    const sql = `SELECT * FROM categorias WHERE ativa = 1`;
    db.all(sql, [], (err, rows) => {
      if (err) return callback(err, null);
      callback(null, rows);
    });
  }
}

module.exports = CategoriaRepository;
```

**CategoriaService.js:**
```javascript
const CategoriaRepository = require('../repositories/CategoriaRepository');

class CategoriaService {
  static create(dados, callback) {
    if (!dados.nome || dados.nome.trim() === '') {
      return callback(new Error('Nome é obrigatório'), null);
    }

    CategoriaRepository.create(dados, (err, resultado) => {
      if (err) return callback(err, null);
      
      CategoriaRepository.findById(resultado.id, callback);
    });
  }

  static findAll(filtros, callback) {
    if (filtros && filtros.ativa === true) {
      return CategoriaRepository.findAtivas(callback);
    }
    
    CategoriaRepository.findAll(callback);
  }

  static findById(id, callback) {
    CategoriaRepository.findById(id, (err, categoria) => {
      if (err) return callback(err, null);
      
      if (!categoria) {
        return callback(new Error('Categoria não encontrada'), null);
      }
      
      callback(null, categoria);
    });
  }
}

module.exports = CategoriaService;
```

**CategoriaController.js:**
```javascript
const CategoriaService = require('../services/CategoriaService');

class CategoriaController {
  static async create(req, res) {
    const { nome, descricao, icone } = req.body;

    if (!nome) {
      return res.status(400).json({ erro: 'Campo obrigatório: nome' });
    }

    CategoriaService.create({ nome, descricao, icone }, (err, categoria) => {
      if (err) {
        return res.status(500).json({ erro: 'Erro ao criar categoria' });
      }
      return res.status(201).json(categoria);
    });
  }

  static async getAll(req, res) {
    const { ativa } = req.query;
    const filtros = ativa ? { ativa: ativa === 'true' } : null;

    CategoriaService.findAll(filtros, (err, categorias) => {
      if (err) {
        return res.status(500).json({ erro: 'Erro ao buscar categorias' });
      }
      return res.status(200).json(categorias);
    });
  }

  static async getById(req, res) {
    const { id } = req.params;

    CategoriaService.findById(parseInt(id), (err, categoria) => {
      if (err) {
        if (err.message === 'Categoria não encontrada') {
          return res.status(404).json({ erro: err.message });
        }
        return res.status(500).json({ erro: 'Erro ao buscar categoria' });
      }
      return res.status(200).json(categoria);
    });
  }
}

module.exports = CategoriaController;
```

**Critérios:**
- [ ] Repository com create, findAll, findById, findAtivas
- [ ] Service com validações
- [ ] Controller com tratamento de erros
- [ ] Testes realizados

#### 🎯 Desafio 2: Testar API com Banco Real (20 min)

**Testes:**

```bash
# 1. Criar usuário
POST http://localhost:3000/usuarios
Body: {
  "username": "maria123",
  "email": "maria@email.com",
  "senha": "senha123"
}
Esperado: 201 + usuário criado

# 2. Criar usuário duplicado (email)
POST http://localhost:3000/usuarios
Body: {
  "username": "maria456",
  "email": "maria@email.com",
  "senha": "senha123"
}
Esperado: 409 + "Email já cadastrado"

# 3. Criar usuário duplicado (username)
POST http://localhost:3000/usuarios
Body: {
  "username": "maria123",
  "email": "maria2@email.com",
  "senha": "senha123"
}
Esperado: 409 + "Username já cadastrado"

# 4. Criar usuário com senha curta
POST http://localhost:3000/usuarios
Body: {
  "username": "joao",
  "email": "joao@email.com",
  "senha": "123"
}
Esperado: 400 + "Senha deve ter no mínimo 6 caracteres"

# 5. Listar todos os usuários
GET http://localhost:3000/usuarios
Esperado: 200 + array de usuários

# 6. Buscar usuário por ID
GET http://localhost:3000/usuarios/1
Esperado: 200 + dados do usuário

# 7. Buscar usuário inexistente
GET http://localhost:3000/usuarios/999
Esperado: 404 + "Usuário não encontrado"

# 8. Listar categorias
GET http://localhost:3000/categorias
Esperado: 200 + 3 categorias padrão

# 9. Listar categorias ativas
GET http://localhost:3000/categorias?ativa=true
Esperado: 200 + categorias ativas

# 10. Criar nova categoria
POST http://localhost:3000/categorias
Body: {
  "nome": "Música",
  "descricao": "Converse sobre música",
  "icone": "🎵"
}
Esperado: 201 + categoria criada
```

**Checklist:**
- [ ] Todos os testes passaram
- [ ] Dados persistem no banco
- [ ] Validações funcionando
- [ ] Erros tratados corretamente

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas para a Turma:**

1. **Por que usar arquitetura em camadas?**
   - Separação de responsabilidades, facilita manutenção e testes

2. **Qual a diferença entre Service e Repository?**
   - Service: regras de negócio / Repository: acesso ao banco

3. **Por que usar prepared statements (?)?**
   - Prevenir SQL injection, melhor performance

4. **O que é callback hell?**
   - Callbacks aninhados, dificulta leitura (próxima aula: Promises)

#### 🎯 Fluxo de Dados

```
POST /usuarios
    ↓
UserController.create
    ↓ validação básica
UserService.create
    ↓ regras de negócio
    ↓ verificar email duplicado
UserRepository.create
    ↓ INSERT INTO usuarios
Banco de Dados
    ↓ retorna ID
UserRepository.findById
    ↓ SELECT * FROM usuarios WHERE id = ?
    ↓ retorna usuário completo
UserController
    ↓ res.status(201).json(usuario)
Cliente
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Conectar Node.js ao SQLite
- [ ] Criar estrutura de tabelas
- [ ] Implementar Repository pattern
- [ ] Separar Service de Repository
- [ ] Executar INSERT e SELECT
- [ ] Tratar erros de banco
- [ ] Validar dados antes de inserir

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar método findByUsername no UserRepository
   - Implementar filtro por online em GET /usuarios

2. **Estudo:**
   - Pesquisar sobre Promises e async/await
   - Estudar SQL injection

3. **Reflexão:**
   - Quais as vantagens de usar ORM vs SQL puro?
   - Como melhorar performance de queries?

---

## 📊 Avaliação

### Critérios de Avaliação (Peso: 20% da UC 02 Part 03)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Conexão com Banco** | 20% | Configuração correta do SQLite |
| **Arquitetura em Camadas** | 30% | Separação Controller/Service/Repository |
| **Operações CREATE** | 25% | INSERT funcionando com validações |
| **Operações READ** | 25% | SELECT com filtros funcionando |

### Instrumentos de Avaliação

1. **Observação durante prática** (formativa)
2. **Desafio 1 - CategoriaRepository** (somativa - 60%)
3. **Desafio 2 - Testes completos** (somativa - 40%)

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar instalação do sqlite3
- [ ] Preparar banco de exemplo
- [ ] Revisar callback pattern
- [ ] Ter queries SQL prontas

### Durante a Aula
- [ ] Demonstrar SQL injection ao vivo
- [ ] Mostrar estrutura do banco com DB Browser
- [ ] Explicar diferença entre db.run, db.get, db.all
- [ ] Circular durante implementação

### Pontos de Atenção
- ⚠️ Alunos esquecem de criar tabelas antes de usar
- ⚠️ Confusão entre db.run (INSERT) e db.get (SELECT)
- ⚠️ Callback hell dificulta compreensão
- ⚠️ Esquecem de tratar erros de constraint UNIQUE

### Troubleshooting Comum

**Problema:** "Error: SQLITE_ERROR: no such table"
**Solução:** Executar database/init.js primeiro

**Problema:** "Callback não está sendo chamado"
**Solução:** Verificar se há return antes do callback

**Problema:** "UNIQUE constraint failed"
**Solução:** Tratar erro específico no Service

---

## 📎 Recursos Adicionais

### Links Úteis
- [SQLite3 Node.js Documentation](https://github.com/TryGhost/node-sqlite3)
- [Repository Pattern](https://martinfowler.com/eaaCatalog/repository.html)
- [SQL Injection Prevention](https://owasp.org/www-community/attacks/SQL_Injection)

### Ferramentas
- DB Browser for SQLite
- SQLite Viewer (VS Code extension)

### Próxima Aula
**Aula 06 - Integração com Banco de Dados e CRUD (Parte 2)**
- Operações UPDATE e DELETE
- Relacionamentos entre tabelas
- Queries com JOIN
- Refatoração para Promises/async-await

---

## 📝 Anotações do Professor

**Espaço para observações sobre a turma:**

```
Data: ____/____/____

Pontos positivos:


Dificuldades identificadas:


Ajustes necessários:


Alunos que precisam de atenção:
```

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0  
**Última atualização:** Janeiro 2024
