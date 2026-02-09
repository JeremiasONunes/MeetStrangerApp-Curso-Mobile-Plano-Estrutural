# Aula 04 - Análise de Requisitos e Modelagem do Backend

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Análise de requisitos e modelagem de sistemas backend

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Analisar requisitos funcionais sob a perspectiva do backend
- ✅ Identificar entidades e relacionamentos do sistema
- ✅ Modelar casos de uso para APIs REST
- ✅ Organizar rotas por domínio/recurso
- ✅ Definir a estrutura completa da API do MeetStranger
- ✅ Documentar endpoints e suas responsabilidades

---

## 📚 Conteúdo Programático

### 1. Análise de Requisitos para Backend
- Requisitos funcionais vs não-funcionais
- Identificação de entidades e operações
- Regras de negócio

### 2. Diagrama de Caso de Uso
- Atores do sistema
- Casos de uso principais
- Fluxos de interação

### 3. Diagrama de Classes
- Entidades principais
- Atributos e tipos
- Relacionamentos

### 4. Organização de Rotas por Domínio
- Agrupamento por recurso
- Hierarquia de endpoints
- Versionamento de API

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Padrão REST e métodos HTTP
- Códigos de status HTTP
- Estrutura de requisição/resposta

**Atividade de Aquecimento:**
```
Discussão em grupo:
- O que o MeetStranger precisa fazer?
  (cadastrar usuários, criar salas, fazer matching, etc.)
- Quais dados precisamos armazenar?
- Quais operações o backend precisa oferecer?

Objetivo: Levantar requisitos de forma colaborativa
```

**Checkpoint:**
- Listar no quadro as funcionalidades mencionadas
- Agrupar por similaridade (usuários, salas, matching, etc.)

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Análise de Requisitos (20 min)

**Requisitos Funcionais do MeetStranger:**

**RF01 - Gestão de Usuários**
- Cadastrar novo usuário (username, email, senha)
- Fazer login
- Atualizar perfil
- Visualizar estatísticas pessoais

**RF02 - Gestão de Categorias**
- Listar categorias disponíveis
- Filtrar categorias ativas

**RF03 - Sistema de Matching**
- Entrar na fila de matching por categoria
- Sair da fila
- Criar sala quando houver match
- Visualizar posição na fila

**RF04 - Gestão de Salas**
- Criar sala de chat
- Encerrar sala
- Listar salas ativas do usuário
- Visualizar histórico de salas

**RF05 - Estatísticas**
- Registrar tempo de conversa
- Contar total de conversas
- Identificar categoria favorita
- Gerar relatório de uso

**Requisitos Não-Funcionais:**
- Segurança: Senhas criptografadas
- Performance: Matching em menos de 2 segundos
- Disponibilidade: API sempre disponível
- Escalabilidade: Suportar múltiplos usuários simultâneos

#### 📖 Parte 2: Diagrama de Caso de Uso (20 min)

**Atores:**
- Usuário (principal)
- Sistema de Matching (secundário)

**Casos de Uso:**

```
┌─────────────────────────────────────────────────┐
│                  MeetStranger                   │
│                                                 │
│  ┌──────────────────────────────────────────┐  │
│  │ Usuário                                  │  │
│  │                                          │  │
│  │  • Cadastrar-se                          │  │
│  │  • Fazer Login                           │  │
│  │  • Atualizar Perfil                      │  │
│  │  • Entrar na Fila                        │  │
│  │  • Sair da Fila                          │  │
│  │  • Visualizar Salas Ativas               │  │
│  │  • Encerrar Sala                         │  │
│  │  • Visualizar Estatísticas               │  │
│  └──────────────────────────────────────────┘  │
│                                                 │
│  ┌──────────────────────────────────────────┐  │
│  │ Sistema de Matching                      │  │
│  │                                          │  │
│  │  • Processar Fila                        │  │
│  │  • Criar Sala Automaticamente            │  │
│  │  • Atualizar Estatísticas                │  │
│  └──────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

**Fluxo Principal - Entrar na Fila:**
1. Usuário seleciona categoria
2. Sistema adiciona usuário na fila
3. Sistema verifica se há outro usuário na mesma categoria
4. Se houver: Sistema cria sala e notifica ambos
5. Se não houver: Usuário aguarda na fila

#### 📖 Parte 3: Diagrama de Classes (20 min)

**Entidades Principais:**

```
┌─────────────────────────┐
│       Usuario           │
├─────────────────────────┤
│ - id: INTEGER           │
│ - username: TEXT        │
│ - email: TEXT           │
│ - senha: TEXT           │
│ - criado_em: DATETIME   │
│ - ultimo_login: DATETIME│
│ - online: BOOLEAN       │
└─────────────────────────┘
           │
           │ 1:1
           ▼
┌─────────────────────────┐
│  EstatisticasUsuario    │
├─────────────────────────┤
│ - id: INTEGER           │
│ - usuario_id: INTEGER   │
│ - total_conversas: INT  │
│ - tempo_total_min: INT  │
│ - categoria_fav_id: INT │
└─────────────────────────┘

┌─────────────────────────┐
│      Categoria          │
├─────────────────────────┤
│ - id: INTEGER           │
│ - nome: TEXT            │
│ - descricao: TEXT       │
│ - icone: TEXT           │
│ - ativa: BOOLEAN        │
└─────────────────────────┘
           │
           │ 1:N
           ▼
┌─────────────────────────┐
│     FilaMatching        │
├─────────────────────────┤
│ - id: INTEGER           │
│ - usuario_id: INTEGER   │
│ - categoria_id: INTEGER │
│ - entrou_em: DATETIME   │
│ - posicao: INTEGER      │
└─────────────────────────┘

┌─────────────────────────┐
│         Sala            │
├─────────────────────────┤
│ - id: INTEGER           │
│ - categoria_id: INTEGER │
│ - usuario1_id: INTEGER  │
│ - usuario2_id: INTEGER  │
│ - criada_em: DATETIME   │
│ - encerrada_em: DATETIME│
│ - ativa: BOOLEAN        │
└─────────────────────────┘
```

**Relacionamentos:**
- Usuario 1:1 EstatisticasUsuario
- Categoria 1:N FilaMatching
- Usuario 1:N FilaMatching
- Categoria 1:N Sala
- Usuario 1:N Sala (como usuario1 ou usuario2)

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Definir Rotas da API (40 min)

**Organização por Domínio:**

**1. Domínio: Autenticação**
```
POST   /auth/registro          # Cadastrar novo usuário
POST   /auth/login             # Fazer login
POST   /auth/logout            # Fazer logout
```

**2. Domínio: Usuários**
```
GET    /usuarios               # Listar todos (admin)
GET    /usuarios/:id           # Buscar por ID
PUT    /usuarios/:id           # Atualizar perfil
DELETE /usuarios/:id           # Remover conta
GET    /usuarios/:id/estatisticas  # Ver estatísticas
```

**3. Domínio: Categorias**
```
GET    /categorias             # Listar todas
GET    /categorias/:id         # Buscar por ID
POST   /categorias             # Criar (admin)
PUT    /categorias/:id         # Atualizar (admin)
DELETE /categorias/:id         # Remover (admin)
```

**4. Domínio: Matching**
```
POST   /matching/entrar        # Entrar na fila
DELETE /matching/sair           # Sair da fila
GET    /matching/fila          # Ver fila atual
GET    /matching/posicao       # Ver minha posição
```

**5. Domínio: Salas**
```
GET    /salas                  # Listar minhas salas
GET    /salas/:id              # Buscar sala específica
POST   /salas/:id/encerrar     # Encerrar sala
GET    /salas/ativas           # Listar salas ativas
GET    /salas/historico        # Histórico de salas
```

**Tabela Resumo:**

| Endpoint | Método | Descrição | Auth |
|----------|--------|-----------|------|
| /auth/registro | POST | Cadastrar usuário | ❌ |
| /auth/login | POST | Fazer login | ❌ |
| /auth/logout | POST | Fazer logout | ✅ |
| /usuarios/:id | GET | Buscar usuário | ✅ |
| /usuarios/:id | PUT | Atualizar perfil | ✅ |
| /usuarios/:id/estatisticas | GET | Ver estatísticas | ✅ |
| /categorias | GET | Listar categorias | ❌ |
| /categorias/:id | GET | Buscar categoria | ❌ |
| /matching/entrar | POST | Entrar na fila | ✅ |
| /matching/sair | DELETE | Sair da fila | ✅ |
| /matching/posicao | GET | Ver posição | ✅ |
| /salas | GET | Minhas salas | ✅ |
| /salas/:id | GET | Buscar sala | ✅ |
| /salas/:id/encerrar | POST | Encerrar sala | ✅ |

#### 💻 Exercício 2: Documentar Endpoints (30 min)

**Template de Documentação:**

**Endpoint:** POST /auth/registro

**Descrição:** Cadastra novo usuário no sistema

**Request Body:**
```json
{
  "username": "joao123",
  "email": "joao@email.com",
  "senha": "senha123"
}
```

**Response Success (201):**
```json
{
  "id": 1,
  "username": "joao123",
  "email": "joao@email.com",
  "criado_em": "2024-01-15T10:30:00",
  "online": false
}
```

**Response Error (400):**
```json
{
  "erro": "Email já cadastrado"
}
```

**Regras de Negócio:**
- Username deve ter entre 3 e 20 caracteres
- Email deve ser válido
- Senha deve ter no mínimo 6 caracteres
- Email deve ser único no sistema

---

**Endpoint:** POST /matching/entrar

**Descrição:** Adiciona usuário na fila de matching

**Request Body:**
```json
{
  "usuario_id": 1,
  "categoria_id": 2
}
```

**Response Success (201):**
```json
{
  "id": 5,
  "usuario_id": 1,
  "categoria_id": 2,
  "entrou_em": "2024-01-15T14:20:00",
  "posicao": 3
}
```

**Response Success com Match (201):**
```json
{
  "match": true,
  "sala": {
    "id": 10,
    "categoria_id": 2,
    "usuario1_id": 1,
    "usuario2_id": 4,
    "criada_em": "2024-01-15T14:20:00",
    "ativa": true
  }
}
```

**Regras de Negócio:**
- Usuário não pode estar em múltiplas filas
- Categoria deve estar ativa
- Se houver outro usuário na fila da mesma categoria: criar sala
- Se não houver: adicionar na fila

#### 💻 Exercício 3: Criar Estrutura de Arquivos (20 min)

**Organizar projeto por domínio:**

```
src/
├── controllers/
│   ├── AuthController.js
│   ├── UserController.js
│   ├── CategoriaController.js
│   ├── MatchingController.js
│   └── SalaController.js
├── services/
│   ├── AuthService.js
│   ├── UserService.js
│   ├── CategoriaService.js
│   ├── MatchingService.js
│   └── SalaService.js
├── routes/
│   ├── authRoutes.js
│   ├── userRoutes.js
│   ├── categoriaRoutes.js
│   ├── matchingRoutes.js
│   └── salaRoutes.js
├── middleware/
│   ├── authMiddleware.js
│   └── validationMiddleware.js
├── config/
│   └── database.js
└── app.js
```

**Criar arquivos base:**

**authRoutes.js:**
```javascript
const express = require('express');
const AuthController = require('../controllers/AuthController');

const router = express.Router();

router.post('/registro', AuthController.registro);
router.post('/login', AuthController.login);
router.post('/logout', AuthController.logout);

module.exports = router;
```

**matchingRoutes.js:**
```javascript
const express = require('express');
const MatchingController = require('../controllers/MatchingController');

const router = express.Router();

router.post('/entrar', MatchingController.entrar);
router.delete('/sair', MatchingController.sair);
router.get('/fila', MatchingController.verFila);
router.get('/posicao', MatchingController.verPosicao);

module.exports = router;
```

**salaRoutes.js:**
```javascript
const express = require('express');
const SalaController = require('../controllers/SalaController');

const router = express.Router();

router.get('/', SalaController.listarMinhas);
router.get('/ativas', SalaController.listarAtivas);
router.get('/historico', SalaController.historico);
router.get('/:id', SalaController.buscarPorId);
router.post('/:id/encerrar', SalaController.encerrar);

module.exports = router;
```

**app.js atualizado:**
```javascript
const express = require('express');
const authRoutes = require('./routes/authRoutes');
const userRoutes = require('./routes/userRoutes');
const categoriaRoutes = require('./routes/categoriaRoutes');
const matchingRoutes = require('./routes/matchingRoutes');
const salaRoutes = require('./routes/salaRoutes');

const app = express();

app.use(express.json());

app.use('/auth', authRoutes);
app.use('/usuarios', userRoutes);
app.use('/categorias', categoriaRoutes);
app.use('/matching', matchingRoutes);
app.use('/salas', salaRoutes);

module.exports = app;
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Documentar Todos os Endpoints (40 min)

**Tarefa:** Criar arquivo `API_DOCUMENTATION.md` com documentação completa

**Estrutura:**
```markdown
# API MeetStranger - Documentação

## Autenticação

### POST /auth/registro
[Descrição, Request, Response, Regras]

### POST /auth/login
[Descrição, Request, Response, Regras]

## Usuários

### GET /usuarios/:id
[Descrição, Request, Response, Regras]

[... continuar para todos os endpoints]
```

**Critérios:**
- [ ] Todos os 15+ endpoints documentados
- [ ] Request body com exemplo
- [ ] Response success com exemplo
- [ ] Response error com exemplo
- [ ] Regras de negócio listadas
- [ ] Códigos de status corretos

#### 🎯 Desafio 2: Implementar MatchingController (20 min)

**Tarefa:** Criar lógica básica de matching

**MatchingService.js:**
```javascript
let fila = [];
let proximoId = 1;

class MatchingService {
  static entrar(usuarioId, categoriaId) {
    // Verificar se já está na fila
    const jaEstaFila = fila.find(f => f.usuario_id === usuarioId);
    if (jaEstaFila) {
      throw new Error('Usuário já está na fila');
    }

    // Buscar outro usuário na mesma categoria
    const outroUsuario = fila.find(f => f.categoria_id === categoriaId);
    
    if (outroUsuario) {
      // Match encontrado - remover da fila e criar sala
      fila = fila.filter(f => f.id !== outroUsuario.id);
      return {
        match: true,
        sala: {
          id: Math.floor(Math.random() * 1000),
          categoria_id: categoriaId,
          usuario1_id: outroUsuario.usuario_id,
          usuario2_id: usuarioId,
          criada_em: new Date().toISOString(),
          ativa: true
        }
      };
    } else {
      // Adicionar na fila
      const novaEntrada = {
        id: proximoId++,
        usuario_id: usuarioId,
        categoria_id: categoriaId,
        entrou_em: new Date().toISOString(),
        posicao: fila.filter(f => f.categoria_id === categoriaId).length + 1
      };
      fila.push(novaEntrada);
      return { match: false, fila: novaEntrada };
    }
  }

  static sair(usuarioId) {
    const index = fila.findIndex(f => f.usuario_id === usuarioId);
    if (index === -1) return false;
    
    fila.splice(index, 1);
    return true;
  }

  static verFila() {
    return fila;
  }

  static verPosicao(usuarioId) {
    const entrada = fila.find(f => f.usuario_id === usuarioId);
    return entrada || null;
  }
}

module.exports = MatchingService;
```

**MatchingController.js:**
```javascript
const MatchingService = require('../services/MatchingService');

class MatchingController {
  static async entrar(req, res) {
    try {
      const { usuario_id, categoria_id } = req.body;
      
      if (!usuario_id || !categoria_id) {
        return res.status(400).json({ erro: 'usuario_id e categoria_id obrigatórios' });
      }
      
      const resultado = MatchingService.entrar(usuario_id, categoria_id);
      return res.status(201).json(resultado);
    } catch (erro) {
      return res.status(400).json({ erro: erro.message });
    }
  }

  static async sair(req, res) {
    try {
      const { usuario_id } = req.body;
      
      if (!usuario_id) {
        return res.status(400).json({ erro: 'usuario_id obrigatório' });
      }
      
      const removido = MatchingService.sair(usuario_id);
      
      if (!removido) {
        return res.status(404).json({ erro: 'Usuário não está na fila' });
      }
      
      return res.status(204).send();
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao sair da fila' });
    }
  }

  static async verFila(req, res) {
    try {
      const fila = MatchingService.verFila();
      return res.status(200).json(fila);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao buscar fila' });
    }
  }

  static async verPosicao(req, res) {
    try {
      const { usuario_id } = req.query;
      
      if (!usuario_id) {
        return res.status(400).json({ erro: 'usuario_id obrigatório' });
      }
      
      const posicao = MatchingService.verPosicao(parseInt(usuario_id));
      
      if (!posicao) {
        return res.status(404).json({ erro: 'Usuário não está na fila' });
      }
      
      return res.status(200).json(posicao);
    } catch (erro) {
      return res.status(500).json({ erro: 'Erro ao buscar posição' });
    }
  }
}

module.exports = MatchingController;
```

**Testar:**
```bash
# Usuário 1 entra na fila
POST http://localhost:3000/matching/entrar
Body: { "usuario_id": 1, "categoria_id": 2 }
Esperado: 201 + { "match": false, "fila": {...} }

# Usuário 2 entra na mesma categoria (match!)
POST http://localhost:3000/matching/entrar
Body: { "usuario_id": 2, "categoria_id": 2 }
Esperado: 201 + { "match": true, "sala": {...} }

# Ver fila
GET http://localhost:3000/matching/fila
Esperado: 200 + array

# Sair da fila
DELETE http://localhost:3000/matching/sair
Body: { "usuario_id": 1 }
Esperado: 204
```

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas para a Turma:**

1. **Qual a diferença entre requisito funcional e não-funcional?**
   - RF: O que o sistema faz / RNF: Como o sistema faz

2. **Por que organizar rotas por domínio?**
   - Facilita manutenção, escalabilidade e compreensão

3. **O que é um caso de uso?**
   - Interação entre ator e sistema para atingir objetivo

4. **Como decidir quais endpoints criar?**
   - Baseado nos requisitos funcionais e operações CRUD

#### 🎯 Mapa Mental da API

```
        MeetStranger API
              |
    ┌─────────┼─────────┐
    |         |         |
  /auth   /usuarios  /categorias
    |         |         |
 registro  perfil   listar
  login    stats    buscar
  logout
              |
    ┌─────────┼─────────┐
    |                   |
 /matching           /salas
    |                   |
  entrar            minhas
   sair             ativas
   fila           encerrar
  posicao         historico
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Identificar requisitos funcionais
- [ ] Modelar casos de uso
- [ ] Definir entidades e relacionamentos
- [ ] Organizar rotas por domínio
- [ ] Documentar endpoints
- [ ] Implementar lógica de matching básica

#### 📚 Para Casa

1. **Documentação:**
   - Completar API_DOCUMENTATION.md
   - Adicionar exemplos de erro para cada endpoint

2. **Modelagem:**
   - Desenhar fluxo completo de matching
   - Identificar possíveis problemas (race condition)

3. **Implementação:**
   - Criar AuthController básico
   - Implementar validação de email

---

## 📊 Avaliação

### Critérios de Avaliação (Peso: 15% da UC 02 Part 03)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Análise de Requisitos** | 25% | Identificação correta de funcionalidades |
| **Modelagem** | 25% | Casos de uso e entidades bem definidos |
| **Organização de Rotas** | 25% | Estrutura lógica e RESTful |
| **Documentação** | 25% | API_DOCUMENTATION.md completo |

### Instrumentos de Avaliação

1. **Participação em discussões** (formativa)
2. **Desafio 1 - Documentação** (somativa - 50%)
3. **Desafio 2 - MatchingController** (somativa - 50%)

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Revisar requisitos do MeetStranger
- [ ] Preparar exemplos de APIs conhecidas
- [ ] Ter diagramas prontos para projetar
- [ ] Preparar template de documentação

### Durante a Aula
- [ ] Usar quadro para desenhar diagramas colaborativamente
- [ ] Incentivar discussão sobre requisitos
- [ ] Mostrar exemplos reais (GitHub API, Twitter API)
- [ ] Circular durante modelagem

### Pontos de Atenção
- ⚠️ Alunos confundem requisito com solução técnica
- ⚠️ Dificuldade em identificar relacionamentos
- ⚠️ Tendência a criar endpoints não-RESTful
- ⚠️ Esquecem de documentar regras de negócio

### Troubleshooting Comum

**Problema:** "Não sei quais endpoints criar"
**Solução:** Listar operações CRUD para cada entidade primeiro

**Problema:** "Como organizar rotas aninhadas?"
**Solução:** Usar relacionamento: /usuarios/:id/estatisticas

**Problema:** "Matching está muito complexo"
**Solução:** Começar com versão simples (FIFO), melhorar depois

---

## 📎 Recursos Adicionais

### Links Úteis
- [REST API Design Best Practices](https://restfulapi.net/resource-naming/)
- [API Documentation Guide](https://swagger.io/resources/articles/documenting-apis/)
- [Use Case Diagrams](https://www.lucidchart.com/pages/uml-use-case-diagram)

### Ferramentas
- Draw.io (diagramas)
- Swagger/OpenAPI (documentação)
- Postman (testes)

### Próxima Aula
**Aula 05-06 - Integração com Banco de Dados e CRUD**
- Conectar SQLite ao projeto
- Implementar camada de dados
- CRUD completo com banco real
- Migrations e seeds

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
