# Aula 03 - APIs REST e Métodos HTTP

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Desenvolvimento de APIs RESTful seguindo padrões de mercado

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Compreender os princípios do padrão arquitetural REST
- ✅ Aplicar corretamente os métodos HTTP (GET, POST, PUT, DELETE)
- ✅ Estruturar requisições e respostas HTTP adequadamente
- ✅ Utilizar códigos de status HTTP de forma semântica
- ✅ Projetar endpoints RESTful seguindo boas práticas
- ✅ Implementar APIs REST para o projeto MeetStranger

---

## 📚 Conteúdo Programático

### 1. Conceito de API RESTful
- O que é REST (Representational State Transfer)
- Princípios REST: stateless, client-server, cacheable, uniform interface
- Recursos e URIs
- Diferença entre REST e RESTful

### 2. Métodos HTTP
- GET: Recuperar recursos
- POST: Criar novos recursos
- PUT: Atualizar recursos existentes
- DELETE: Remover recursos
- PATCH: Atualização parcial (conceito)

### 3. Estrutura de Requisição e Resposta
- Headers (cabeçalhos)
- Body (corpo da requisição/resposta)
- Query parameters
- Route parameters
- Content-Type e Accept

### 4. Códigos de Status HTTP
- 2xx: Sucesso (200, 201, 204)
- 4xx: Erro do cliente (400, 404, 409)
- 5xx: Erro do servidor (500)

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Estrutura de projeto backend (controllers, routes, services)
- CRUD básico com dados mockados
- Middlewares e fluxo de requisição

**Atividade de Aquecimento:**
```
Discussão em grupo:
- Quando vocês acessam o Instagram, que tipo de ações vocês fazem?
  (ver posts, curtir, comentar, deletar comentário)
- Como o app sabe qual ação executar?
- Por que algumas ações precisam de confirmação e outras não?

Objetivo: Conectar ações do usuário com métodos HTTP
```

**Checkpoint:**
- Perguntar: "Qual a diferença entre criar um usuário e buscar um usuário?"
- Resposta esperada: Criar modifica dados, buscar apenas lê

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: O que é REST? (20 min)

**Conceito:**
REST é um estilo arquitetural para sistemas distribuídos, especialmente para web services. Uma API RESTful usa HTTP de forma semântica para operações CRUD.

**Princípios REST:**

1. **Stateless (Sem Estado):**
   - Cada requisição contém todas as informações necessárias
   - Servidor não armazena contexto do cliente entre requisições

2. **Client-Server (Cliente-Servidor):**
   - Separação clara entre frontend e backend
   - Cada um evolui independentemente

3. **Uniform Interface (Interface Uniforme):**
   - Recursos identificados por URIs
   - Manipulação através de representações (JSON)
   - Mensagens auto-descritivas

**Recursos e URIs:**
```
Recurso: Entidade que queremos manipular (usuário, sala, categoria)
URI: Identificador único do recurso

Exemplos MeetStranger:
/usuarios          → Coleção de usuários
/usuarios/1        → Usuário específico (id=1)
/categorias        → Coleção de categorias
/salas/5/mensagens → Mensagens da sala 5
```

**❌ Não RESTful vs ✅ RESTful:**
```
❌ /getUsuarios
❌ /criarUsuario
❌ /deletarUsuario?id=1

✅ GET /usuarios
✅ POST /usuarios
✅ DELETE /usuarios/1
```

#### 📖 Parte 2: Métodos HTTP (25 min)

**Tabela de Métodos:**

| Método | Ação | Idempotente* | Corpo Requisição | Corpo Resposta |
|--------|------|--------------|------------------|----------------|
| GET | Ler/Buscar | ✅ Sim | ❌ Não | ✅ Sim |
| POST | Criar | ❌ Não | ✅ Sim | ✅ Sim |
| PUT | Atualizar completo | ✅ Sim | ✅ Sim | ✅ Sim |
| DELETE | Remover | ✅ Sim | ❌ Não | ⚠️ Opcional |

*Idempotente: Executar múltiplas vezes produz o mesmo resultado

**Exemplos MeetStranger:**

```javascript
// GET - Buscar todos os usuários
GET /usuarios
Resposta: Lista de usuários

// GET - Buscar usuário específico
GET /usuarios/1
Resposta: Dados do usuário id=1

// POST - Criar novo usuário
POST /usuarios
Body: { "username": "joao123", "email": "joao@email.com", "senha": "123456" }
Resposta: Usuário criado com id gerado

// PUT - Atualizar usuário completo
PUT /usuarios/1
Body: { "username": "joao_silva", "email": "joao.silva@email.com", "senha": "nova123" }
Resposta: Usuário atualizado

// DELETE - Remover usuário
DELETE /usuarios/1
Resposta: Confirmação de remoção
```

#### 📖 Parte 3: Códigos de Status HTTP (15 min)

**Códigos Principais:**

**2xx - Sucesso:**
- `200 OK`: Requisição bem-sucedida (GET, PUT)
- `201 Created`: Recurso criado com sucesso (POST)
- `204 No Content`: Sucesso sem conteúdo na resposta (DELETE)

**4xx - Erro do Cliente:**
- `400 Bad Request`: Dados inválidos enviados
- `404 Not Found`: Recurso não encontrado
- `409 Conflict`: Conflito (ex: email já cadastrado)

**5xx - Erro do Servidor:**
- `500 Internal Server Error`: Erro não tratado no servidor

**Quando usar cada código:**
```javascript
// 200 - Busca bem-sucedida
GET /usuarios/1 → 200 + dados do usuário

// 201 - Criação bem-sucedida
POST /usuarios → 201 + usuário criado

// 204 - Deleção bem-sucedida
DELETE /usuarios/1 → 204 (sem corpo)

// 400 - Dados inválidos
POST /usuarios (sem email) → 400 + { "erro": "Email obrigatório" }

// 404 - Não encontrado
GET /usuarios/999 → 404 + { "erro": "Usuário não encontrado" }

// 409 - Conflito
POST /usuarios (email duplicado) → 409 + { "erro": "Email já cadastrado" }
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Refatorar UserController com REST (30 min)

**Objetivo:** Aplicar padrões REST e códigos de status corretos

**Arquivo:** `src/controllers/UserController.js`

```javascript
const UserService = require('../services/UserService');

class UserController {
  // GET /usuarios - Listar todos
  static async getAll(req, res) {
    try {
      const usuarios = UserService.getAll();
      return res.status(200).json(usuarios);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao buscar usuários' });
    }
  }

  // GET /usuarios/:id - Buscar por ID
  static async getById(req, res) {
    try {
      const { id } = req.params;
      const usuario = UserService.getById(parseInt(id));
      
      if (!usuario) {
        return res.status(404).json({ erro: 'Usuário não encontrado' });
      }
      
      return res.status(200).json(usuario);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao buscar usuário' });
    }
  }

  // POST /usuarios - Criar novo
  static async create(req, res) {
    try {
      const { username, email, senha } = req.body;
      
      // Validação
      if (!username || !email || !senha) {
        return res.status(400).json({ 
          erro: 'Campos obrigatórios: username, email, senha' 
        });
      }
      
      // Verificar email duplicado
      const emailExiste = UserService.getAll().find(u => u.email === email);
      if (emailExiste) {
        return res.status(409).json({ erro: 'Email já cadastrado' });
      }
      
      const novoUsuario = UserService.create({ username, email, senha });
      return res.status(201).json(novoUsuario);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao criar usuário' });
    }
  }

  // PUT /usuarios/:id - Atualizar completo
  static async update(req, res) {
    try {
      const { id } = req.params;
      const { username, email, senha } = req.body;
      
      // Validação
      if (!username || !email || !senha) {
        return res.status(400).json({ 
          erro: 'Campos obrigatórios: username, email, senha' 
        });
      }
      
      const usuarioAtualizado = UserService.update(parseInt(id), { username, email, senha });
      
      if (!usuarioAtualizado) {
        return res.status(404).json({ erro: 'Usuário não encontrado' });
      }
      
      return res.status(200).json(usuarioAtualizado);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao atualizar usuário' });
    }
  }

  // DELETE /usuarios/:id - Remover
  static async delete(req, res) {
    try {
      const { id } = req.params;
      const removido = UserService.delete(parseInt(id));
      
      if (!removido) {
        return res.status(404).json({ erro: 'Usuário não encontrado' });
      }
      
      return res.status(204).send();
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao remover usuário' });
    }
  }
}

module.exports = UserController;
```

**Pontos de Atenção:**
- ✅ Status 200 para GET e PUT bem-sucedidos
- ✅ Status 201 para POST (criação)
- ✅ Status 204 para DELETE (sem corpo)
- ✅ Status 400 para validação
- ✅ Status 404 para recurso não encontrado
- ✅ Status 409 para conflito (email duplicado)
- ✅ Status 500 para erros não tratados

#### 💻 Exercício 2: Criar CategoriaController REST (30 min)

**Objetivo:** Aplicar conhecimento em novo recurso

**Arquivo:** `src/controllers/CategoriaController.js`

```javascript
const CategoriaService = require('../services/CategoriaService');

class CategoriaController {
  static async getAll(req, res) {
    try {
      const categorias = CategoriaService.getAll();
      return res.status(200).json(categorias);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao buscar categorias' });
    }
  }

  static async getById(req, res) {
    try {
      const { id } = req.params;
      const categoria = CategoriaService.getById(parseInt(id));
      
      if (!categoria) {
        return res.status(404).json({ erro: 'Categoria não encontrada' });
      }
      
      return res.status(200).json(categoria);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao buscar categoria' });
    }
  }

  static async create(req, res) {
    try {
      const { nome, descricao, icone } = req.body;
      
      if (!nome) {
        return res.status(400).json({ erro: 'Campo obrigatório: nome' });
      }
      
      const novaCategoria = CategoriaService.create({ nome, descricao, icone });
      return res.status(201).json(novaCategoria);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao criar categoria' });
    }
  }

  static async update(req, res) {
    try {
      const { id } = req.params;
      const { nome, descricao, icone, ativa } = req.body;
      
      const categoriaAtualizada = CategoriaService.update(parseInt(id), { 
        nome, descricao, icone, ativa 
      });
      
      if (!categoriaAtualizada) {
        return res.status(404).json({ erro: 'Categoria não encontrada' });
      }
      
      return res.status(200).json(categoriaAtualizada);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao atualizar categoria' });
    }
  }

  static async delete(req, res) {
    try {
      const { id } = req.params;
      const removido = CategoriaService.delete(parseInt(id));
      
      if (!removido) {
        return res.status(404).json({ erro: 'Categoria não encontrada' });
      }
      
      return res.status(204).send();
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao remover categoria' });
    }
  }
}

module.exports = CategoriaController;
```

**Arquivo:** `src/services/CategoriaService.js`

```javascript
let categorias = [
  { id: 1, nome: 'Filmes', descricao: 'Converse sobre cinema', icone: '🎬', ativa: true },
  { id: 2, nome: 'Jogos', descricao: 'Converse sobre games', icone: '🎮', ativa: true },
  { id: 3, nome: 'Séries', descricao: 'Converse sobre séries', icone: '📺', ativa: true }
];

let proximoId = 4;

class CategoriaService {
  static getAll() {
    return categorias;
  }

  static getById(id) {
    return categorias.find(c => c.id === id);
  }

  static create(dados) {
    const novaCategoria = {
      id: proximoId++,
      nome: dados.nome,
      descricao: dados.descricao || '',
      icone: dados.icone || '📁',
      ativa: true
    };
    categorias.push(novaCategoria);
    return novaCategoria;
  }

  static update(id, dados) {
    const index = categorias.findIndex(c => c.id === id);
    if (index === -1) return null;
    
    categorias[index] = { ...categorias[index], ...dados };
    return categorias[index];
  }

  static delete(id) {
    const index = categorias.findIndex(c => c.id === id);
    if (index === -1) return false;
    
    categorias.splice(index, 1);
    return true;
  }
}

module.exports = CategoriaService;
```

**Arquivo:** `src/routes/categoriaRoutes.js`

```javascript
const express = require('express');
const CategoriaController = require('../controllers/CategoriaController');

const router = express.Router();

router.get('/', CategoriaController.getAll);
router.get('/:id', CategoriaController.getById);
router.post('/', CategoriaController.create);
router.put('/:id', CategoriaController.update);
router.delete('/:id', CategoriaController.delete);

module.exports = router;
```

**Atualizar:** `src/app.js`

```javascript
const express = require('express');
const userRoutes = require('./routes/userRoutes');
const categoriaRoutes = require('./routes/categoriaRoutes');

const app = express();

app.use(express.json());

app.use('/usuarios', userRoutes);
app.use('/categorias', categoriaRoutes);

module.exports = app;
```

#### 💻 Exercício 3: Testar API REST (30 min)

**Testar com Thunder Client / Postman / curl:**

```bash
# GET - Listar categorias
GET http://localhost:3000/categorias
Esperado: 200 + array de categorias

# GET - Buscar categoria específica
GET http://localhost:3000/categorias/1
Esperado: 200 + categoria Filmes

# GET - Buscar categoria inexistente
GET http://localhost:3000/categorias/999
Esperado: 404 + { "erro": "Categoria não encontrada" }

# POST - Criar categoria
POST http://localhost:3000/categorias
Body: { "nome": "Música", "descricao": "Converse sobre música", "icone": "🎵" }
Esperado: 201 + categoria criada

# POST - Criar sem nome (validação)
POST http://localhost:3000/categorias
Body: { "descricao": "Teste" }
Esperado: 400 + { "erro": "Campo obrigatório: nome" }

# PUT - Atualizar categoria
PUT http://localhost:3000/categorias/1
Body: { "nome": "Cinema", "descricao": "Filmes e cinema", "icone": "🎬", "ativa": true }
Esperado: 200 + categoria atualizada

# DELETE - Remover categoria
DELETE http://localhost:3000/categorias/4
Esperado: 204 (sem corpo)

# DELETE - Remover inexistente
DELETE http://localhost:3000/categorias/999
Esperado: 404 + { "erro": "Categoria não encontrada" }
```

**Checklist de Testes:**
- [ ] GET retorna 200 com dados
- [ ] GET com ID inválido retorna 404
- [ ] POST com dados válidos retorna 201
- [ ] POST com dados inválidos retorna 400
- [ ] POST com conflito retorna 409 (usuários)
- [ ] PUT com dados válidos retorna 200
- [ ] PUT com ID inválido retorna 404
- [ ] DELETE com ID válido retorna 204
- [ ] DELETE com ID inválido retorna 404

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Criar SalaController REST (40 min)

**Requisitos:**

1. Criar `SalaService.js` com dados mockados:
```javascript
let salas = [
  { 
    id: 1, 
    categoriaId: 1, 
    usuario1Id: 1, 
    usuario2Id: 2, 
    criadaEm: '2024-01-15T10:30:00', 
    ativa: true 
  }
];
```

2. Criar `SalaController.js` com endpoints REST:
   - GET /salas - Listar todas
   - GET /salas/:id - Buscar por ID
   - POST /salas - Criar sala (validar categoriaId e usuario1Id)
   - PUT /salas/:id - Atualizar sala
   - DELETE /salas/:id - Remover sala

3. Criar `salaRoutes.js` e registrar em `app.js`

4. Implementar validações:
   - categoriaId obrigatório
   - usuario1Id obrigatório
   - Retornar 400 se faltar dados
   - Retornar 404 se sala não existir

5. Testar todos os endpoints

**Critérios de Avaliação:**
- [ ] Service criado com CRUD completo
- [ ] Controller com 5 métodos REST
- [ ] Códigos de status corretos
- [ ] Validações implementadas
- [ ] Rotas registradas
- [ ] Testes realizados

#### 🎯 Desafio 2: Endpoint de Busca com Query Parameters (20 min)

**Objetivo:** Implementar filtros em GET

**Requisito:**
```javascript
// GET /usuarios?online=true
// Retorna apenas usuários online

// GET /categorias?ativa=true
// Retorna apenas categorias ativas

// GET /salas?ativa=false
// Retorna apenas salas encerradas
```

**Implementação em UserController:**
```javascript
static async getAll(req, res) {
  try {
    const { online } = req.query;
    let usuarios = UserService.getAll();
    
    if (online !== undefined) {
      const filtroOnline = online === 'true';
      usuarios = usuarios.filter(u => u.online === filtroOnline);
    }
    
    return res.status(200).json(usuarios);
  } catch (erro) {
    return res.status(500).json({ erro: 'Erro ao buscar usuários' });
  }
}
```

**Tarefa:** Implementar filtros em CategoriaController e SalaController

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas para a Turma:**

1. **O que é REST?**
   - Resposta: Estilo arquitetural para APIs que usa HTTP de forma semântica

2. **Qual a diferença entre GET e POST?**
   - Resposta: GET busca dados (não modifica), POST cria novos recursos

3. **Quando usar status 404?**
   - Resposta: Quando o recurso solicitado não é encontrado

4. **Por que usar 201 em vez de 200 no POST?**
   - Resposta: 201 indica especificamente que um recurso foi criado

5. **O que significa API stateless?**
   - Resposta: Cada requisição contém todas as informações necessárias, servidor não guarda estado

#### 🎯 Mapa Mental REST

```
                    REST API
                       |
        ┌──────────────┼──────────────┐
        |              |              |
    Recursos        Métodos        Status
        |              |              |
    /usuarios      GET POST       200 201
    /categorias    PUT DELETE     400 404
    /salas                        409 500
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Explicar o que é REST
- [ ] Diferenciar os 4 métodos HTTP principais
- [ ] Usar códigos de status corretamente
- [ ] Estruturar URIs RESTful
- [ ] Validar dados de entrada
- [ ] Retornar respostas padronizadas
- [ ] Testar APIs com Thunder Client

#### 📚 Para Casa

1. **Leitura:**
   - Pesquisar sobre PATCH vs PUT
   - Estudar outros códigos de status (401, 403, 422)

2. **Prática:**
   - Implementar endpoint GET /usuarios/:id/estatisticas
   - Implementar endpoint POST /salas/:id/encerrar
   - Adicionar filtro por categoria em GET /salas

3. **Reflexão:**
   - Por que REST é tão usado na indústria?
   - Quais as vantagens de usar códigos de status corretos?

---

## 📊 Avaliação

### Critérios de Avaliação (Peso: 15% da UC 02 Part 03)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Conceitos REST** | 25% | Compreensão dos princípios REST |
| **Métodos HTTP** | 25% | Uso correto de GET, POST, PUT, DELETE |
| **Códigos de Status** | 25% | Aplicação semântica dos status codes |
| **Implementação** | 25% | SalaController funcional e testado |

### Instrumentos de Avaliação

1. **Observação durante prática guiada** (formativa)
2. **Desafio 1 - SalaController** (somativa - 60%)
3. **Desafio 2 - Query parameters** (somativa - 40%)

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Preparar exemplos de APIs REST conhecidas (Twitter, GitHub)
- [ ] Testar todos os códigos de exemplo
- [ ] Preparar Thunder Client com coleção de requisições
- [ ] Revisar diferença entre PUT e PATCH

### Durante a Aula
- [ ] Usar analogias do mundo real (biblioteca, restaurante)
- [ ] Demonstrar requisições ao vivo
- [ ] Mostrar Network tab do navegador
- [ ] Circular pela sala durante práticas

### Pontos de Atenção
- ⚠️ Alunos confundem PUT com POST
- ⚠️ Esquecem de retornar status corretos
- ⚠️ Dificuldade em entender stateless
- ⚠️ Confusão entre route params e query params

### Troubleshooting Comum

**Problema:** "Meu DELETE retorna 200 em vez de 204"
**Solução:** Usar `res.status(204).send()` em vez de `res.json()`

**Problema:** "Como testar DELETE que retorna 204?"
**Solução:** Verificar status code, não o corpo da resposta

**Problema:** "Quando usar 400 vs 404?"
**Solução:** 400 = dados inválidos, 404 = recurso não existe

---

## 📎 Recursos Adicionais

### Links Úteis
- [REST API Tutorial](https://restfulapi.net/)
- [HTTP Status Codes](https://httpstatuses.com/)
- [MDN - HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

### Ferramentas
- Thunder Client (VS Code)
- Postman
- Insomnia
- curl

### Próxima Aula
**Aula 04 - Análise de Requisitos e Modelagem do Backend**
- Levantamento de requisitos do MeetStranger
- Modelagem de endpoints
- Documentação de API
- Planejamento de implementação

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
