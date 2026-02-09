# Aula 06 - Integração com Banco de Dados e CRUD (Parte 2)

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Completar operações CRUD e aplicar regras de negócio

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Implementar operações UPDATE no banco de dados
- ✅ Implementar operações DELETE no banco de dados
- ✅ Aplicar regras de negócio complexas
- ✅ Validar integridade referencial
- ✅ Implementar soft delete vs hard delete
- ✅ Executar queries com JOIN
- ✅ Testar CRUD completo

---

## 📚 Conteúdo Programático

### 1. Operações UPDATE
- UPDATE com WHERE
- Atualização parcial vs completa
- Validação antes de atualizar

### 2. Operações DELETE
- DELETE com WHERE
- Soft delete (marcar como inativo)
- Hard delete (remover permanentemente)
- Integridade referencial

### 3. Regras de Negócio
- Validações complexas
- Verificação de dependências
- Transações

### 4. Queries com JOIN
- INNER JOIN
- LEFT JOIN
- Agregações

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Arquitetura em camadas (Controller/Service/Repository)
- Operações CREATE e READ
- Prepared statements

**Atividade de Aquecimento:**
```
Discussão:
- O que acontece se tentarmos deletar um usuário que tem salas ativas?
- Como atualizar apenas alguns campos sem sobrescrever outros?
- Qual a diferença entre desativar e deletar?

Objetivo: Preparar para regras de negócio complexas
```

**Checkpoint:**
- Revisar estrutura de tabelas e relacionamentos
- Relembrar comandos UPDATE e DELETE

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Operações UPDATE (20 min)

**UPDATE Básico:**
```javascript
// Atualizar todos os campos
const sql = `UPDATE usuarios SET username = ?, email = ?, senha = ? WHERE id = ?`;
db.run(sql, [username, email, senha, id], callback);

// Atualizar campos específicos
const sql = `UPDATE usuarios SET ultimo_login = CURRENT_TIMESTAMP, online = 1 WHERE id = ?`;
db.run(sql, [id], callback);
```

**UPDATE Parcial (apenas campos fornecidos):**
```javascript
static update(id, dados, callback) {
  const campos = [];
  const valores = [];
  
  if (dados.username) {
    campos.push('username = ?');
    valores.push(dados.username);
  }
  if (dados.email) {
    campos.push('email = ?');
    valores.push(dados.email);
  }
  
  if (campos.length === 0) {
    return callback(new Error('Nenhum campo para atualizar'), null);
  }
  
  valores.push(id);
  const sql = `UPDATE usuarios SET ${campos.join(', ')} WHERE id = ?`;
  
  db.run(sql, valores, function(err) {
    if (err) return callback(err, null);
    callback(null, { changes: this.changes });
  });
}
```

#### 📖 Parte 2: Operações DELETE (20 min)

**Hard Delete (remoção permanente):**
```javascript
static delete(id, callback) {
  const sql = `DELETE FROM usuarios WHERE id = ?`;
  
  db.run(sql, [id], function(err) {
    if (err) return callback(err, null);
    callback(null, { changes: this.changes });
  });
}
```

**Soft Delete (desativação):**
```javascript
// Adicionar coluna ativo na tabela
ALTER TABLE usuarios ADD COLUMN ativo BOOLEAN DEFAULT 1;

// Marcar como inativo
static softDelete(id, callback) {
  const sql = `UPDATE usuarios SET ativo = 0 WHERE id = ?`;
  
  db.run(sql, [id], function(err) {
    if (err) return callback(err, null);
    callback(null, { changes: this.changes });
  });
}

// Filtrar apenas ativos
static findAllAtivos(callback) {
  const sql = `SELECT * FROM usuarios WHERE ativo = 1`;
  db.all(sql, [], callback);
}
```

**Verificar Dependências:**
```javascript
static canDelete(id, callback) {
  const sql = `SELECT COUNT(*) as total FROM salas WHERE (usuario1_id = ? OR usuario2_id = ?) AND ativa = 1`;
  
  db.get(sql, [id, id], (err, row) => {
    if (err) return callback(err, null);
    callback(null, row.total === 0);
  });
}
```

#### 📖 Parte 3: Regras de Negócio (20 min)

**Exemplos de Regras:**

1. **Não permitir deletar usuário com salas ativas**
2. **Não permitir email duplicado ao atualizar**
3. **Atualizar estatísticas ao encerrar sala**
4. **Validar categoria ativa antes de criar sala**

**Implementação:**
```javascript
// Service com regra de negócio
static delete(id, callback) {
  // 1. Verificar se usuário existe
  UserRepository.findById(id, (err, usuario) => {
    if (err) return callback(err, null);
    if (!usuario) return callback(new Error('Usuário não encontrado'), null);
    
    // 2. Verificar se tem salas ativas
    UserRepository.canDelete(id, (err, podeDeletear) => {
      if (err) return callback(err, null);
      if (!podeDeletear) {
        return callback(new Error('Usuário possui salas ativas'), null);
      }
      
      // 3. Deletar
      UserRepository.delete(id, callback);
    });
  });
}
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Implementar UPDATE no UserRepository (25 min)

**Arquivo:** `src/repositories/UserRepository.js`

```javascript
// Adicionar métodos ao UserRepository existente

static update(id, dados, callback) {
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
    return callback(new Error('Nenhum campo para atualizar'), null);
  }
  
  valores.push(id);
  const sql = `UPDATE usuarios SET ${campos.join(', ')} WHERE id = ?`;
  
  db.run(sql, valores, function(err) {
    if (err) return callback(err, null);
    if (this.changes === 0) {
      return callback(new Error('Usuário não encontrado'), null);
    }
    callback(null, { changes: this.changes });
  });
}

static updateLogin(id, callback) {
  const sql = `UPDATE usuarios SET ultimo_login = CURRENT_TIMESTAMP, online = 1 WHERE id = ?`;
  
  db.run(sql, [id], function(err) {
    if (err) return callback(err, null);
    callback(null, { changes: this.changes });
  });
}

static updateOnlineStatus(id, online, callback) {
  const sql = `UPDATE usuarios SET online = ? WHERE id = ?`;
  
  db.run(sql, [online ? 1 : 0, id], function(err) {
    if (err) return callback(err, null);
    callback(null, { changes: this.changes });
  });
}
```

#### 💻 Exercício 2: Implementar DELETE no UserRepository (25 min)

**Arquivo:** `src/repositories/UserRepository.js`

```javascript
// Adicionar métodos ao UserRepository existente

static delete(id, callback) {
  const sql = `DELETE FROM usuarios WHERE id = ?`;
  
  db.run(sql, [id], function(err) {
    if (err) return callback(err, null);
    if (this.changes === 0) {
      return callback(new Error('Usuário não encontrado'), null);
    }
    callback(null, { changes: this.changes });
  });
}

static countSalasAtivas(id, callback) {
  const sql = `
    SELECT COUNT(*) as total 
    FROM salas 
    WHERE (usuario1_id = ? OR usuario2_id = ?) 
    AND ativa = 1
  `;
  
  db.get(sql, [id, id], (err, row) => {
    if (err) return callback(err, null);
    callback(null, row.total);
  });
}
```

#### 💻 Exercício 3: Atualizar UserService com Regras (20 min)

**Arquivo:** `src/services/UserService.js`

```javascript
// Adicionar métodos ao UserService existente

static update(id, dados, callback) {
  // Validações
  if (dados.username && dados.username.length < 3) {
    return callback(new Error('Username deve ter no mínimo 3 caracteres'), null);
  }

  if (dados.email && !dados.email.includes('@')) {
    return callback(new Error('Email inválido'), null);
  }

  if (dados.senha && dados.senha.length < 6) {
    return callback(new Error('Senha deve ter no mínimo 6 caracteres'), null);
  }

  // Verificar se usuário existe
  UserRepository.findById(id, (err, usuario) => {
    if (err) return callback(err, null);
    if (!usuario) return callback(new Error('Usuário não encontrado'), null);

    // Se está alterando email, verificar duplicação
    if (dados.email && dados.email !== usuario.email) {
      UserRepository.findByEmail(dados.email, (err, usuarioExistente) => {
        if (err) return callback(err, null);
        if (usuarioExistente) {
          return callback(new Error('Email já cadastrado'), null);
        }
        
        // Atualizar
        UserRepository.update(id, dados, (err) => {
          if (err) return callback(err, null);
          UserRepository.findById(id, callback);
        });
      });
    } else {
      // Atualizar sem verificar email
      UserRepository.update(id, dados, (err) => {
        if (err) {
          if (err.message.includes('UNIQUE constraint failed: usuarios.username')) {
            return callback(new Error('Username já cadastrado'), null);
          }
          return callback(err, null);
        }
        UserRepository.findById(id, callback);
      });
    }
  });
}

static delete(id, callback) {
  // Verificar se usuário existe
  UserRepository.findById(id, (err, usuario) => {
    if (err) return callback(err, null);
    if (!usuario) return callback(new Error('Usuário não encontrado'), null);

    // Verificar se tem salas ativas
    UserRepository.countSalasAtivas(id, (err, total) => {
      if (err) return callback(err, null);
      
      if (total > 0) {
        return callback(new Error('Não é possível deletar usuário com salas ativas'), null);
      }

      // Deletar
      UserRepository.delete(id, callback);
    });
  });
}
```

#### 💻 Exercício 4: Atualizar UserController (20 min)

**Arquivo:** `src/controllers/UserController.js`

```javascript
// Adicionar métodos ao UserController existente

static async update(req, res) {
  const { id } = req.params;
  const { username, email, senha } = req.body;

  const dados = {};
  if (username) dados.username = username;
  if (email) dados.email = email;
  if (senha) dados.senha = senha;

  if (Object.keys(dados).length === 0) {
    return res.status(400).json({ erro: 'Nenhum campo para atualizar' });
  }

  UserService.update(parseInt(id), dados, (err, usuario) => {
    if (err) {
      if (err.message === 'Usuário não encontrado') {
        return res.status(404).json({ erro: err.message });
      }
      if (err.message.includes('já cadastrado')) {
        return res.status(409).json({ erro: err.message });
      }
      if (err.message.includes('inválido') || err.message.includes('mínimo')) {
        return res.status(400).json({ erro: err.message });
      }
      return res.status(500).json({ erro: 'Erro ao atualizar usuário' });
    }

    return res.status(200).json(usuario);
  });
}

static async delete(req, res) {
  const { id } = req.params;

  UserService.delete(parseInt(id), (err) => {
    if (err) {
      if (err.message === 'Usuário não encontrado') {
        return res.status(404).json({ erro: err.message });
      }
      if (err.message.includes('salas ativas')) {
        return res.status(400).json({ erro: err.message });
      }
      return res.status(500).json({ erro: 'Erro ao deletar usuário' });
    }

    return res.status(204).send();
  });
}
```

**Atualizar rotas:** `src/routes/userRoutes.js`

```javascript
const express = require('express');
const UserController = require('../controllers/UserController');

const router = express.Router();

router.get('/', UserController.getAll);
router.get('/:id', UserController.getById);
router.post('/', UserController.create);
router.put('/:id', UserController.update);      // NOVO
router.delete('/:id', UserController.delete);   // NOVO

module.exports = router;
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Implementar UPDATE e DELETE para Categorias (30 min)

**Tarefa:** Completar CRUD de categorias

**CategoriaRepository.js - Adicionar:**

```javascript
static update(id, dados, callback) {
  const campos = [];
  const valores = [];
  
  if (dados.nome !== undefined) {
    campos.push('nome = ?');
    valores.push(dados.nome);
  }
  if (dados.descricao !== undefined) {
    campos.push('descricao = ?');
    valores.push(dados.descricao);
  }
  if (dados.icone !== undefined) {
    campos.push('icone = ?');
    valores.push(dados.icone);
  }
  if (dados.ativa !== undefined) {
    campos.push('ativa = ?');
    valores.push(dados.ativa ? 1 : 0);
  }
  
  if (campos.length === 0) {
    return callback(new Error('Nenhum campo para atualizar'), null);
  }
  
  valores.push(id);
  const sql = `UPDATE categorias SET ${campos.join(', ')} WHERE id = ?`;
  
  db.run(sql, valores, function(err) {
    if (err) return callback(err, null);
    if (this.changes === 0) {
      return callback(new Error('Categoria não encontrada'), null);
    }
    callback(null, { changes: this.changes });
  });
}

static delete(id, callback) {
  const sql = `DELETE FROM categorias WHERE id = ?`;
  
  db.run(sql, [id], function(err) {
    if (err) return callback(err, null);
    if (this.changes === 0) {
      return callback(new Error('Categoria não encontrada'), null);
    }
    callback(null, { changes: this.changes });
  });
}

static countSalasAtivas(id, callback) {
  const sql = `SELECT COUNT(*) as total FROM salas WHERE categoria_id = ? AND ativa = 1`;
  
  db.get(sql, [id], (err, row) => {
    if (err) return callback(err, null);
    callback(null, row.total);
  });
}
```

**CategoriaService.js - Adicionar:**

```javascript
static update(id, dados, callback) {
  if (dados.nome !== undefined && dados.nome.trim() === '') {
    return callback(new Error('Nome não pode ser vazio'), null);
  }

  CategoriaRepository.findById(id, (err, categoria) => {
    if (err) return callback(err, null);
    if (!categoria) return callback(new Error('Categoria não encontrada'), null);

    CategoriaRepository.update(id, dados, (err) => {
      if (err) return callback(err, null);
      CategoriaRepository.findById(id, callback);
    });
  });
}

static delete(id, callback) {
  CategoriaRepository.findById(id, (err, categoria) => {
    if (err) return callback(err, null);
    if (!categoria) return callback(new Error('Categoria não encontrada'), null);

    CategoriaRepository.countSalasAtivas(id, (err, total) => {
      if (err) return callback(err, null);
      
      if (total > 0) {
        return callback(new Error('Não é possível deletar categoria com salas ativas'), null);
      }

      CategoriaRepository.delete(id, callback);
    });
  });
}
```

**CategoriaController.js - Adicionar:**

```javascript
static async update(req, res) {
  const { id } = req.params;
  const { nome, descricao, icone, ativa } = req.body;

  const dados = {};
  if (nome !== undefined) dados.nome = nome;
  if (descricao !== undefined) dados.descricao = descricao;
  if (icone !== undefined) dados.icone = icone;
  if (ativa !== undefined) dados.ativa = ativa;

  if (Object.keys(dados).length === 0) {
    return res.status(400).json({ erro: 'Nenhum campo para atualizar' });
  }

  CategoriaService.update(parseInt(id), dados, (err, categoria) => {
    if (err) {
      if (err.message.includes('não encontrada')) {
        return res.status(404).json({ erro: err.message });
      }
      if (err.message.includes('vazio')) {
        return res.status(400).json({ erro: err.message });
      }
      return res.status(500).json({ erro: 'Erro ao atualizar categoria' });
    }

    return res.status(200).json(categoria);
  });
}

static async delete(req, res) {
  const { id } = req.params;

  CategoriaService.delete(parseInt(id), (err) => {
    if (err) {
      if (err.message.includes('não encontrada')) {
        return res.status(404).json({ erro: err.message });
      }
      if (err.message.includes('salas ativas')) {
        return res.status(400).json({ erro: err.message });
      }
      return res.status(500).json({ erro: 'Erro ao deletar categoria' });
    }

    return res.status(204).send();
  });
}
```

**Atualizar:** `src/routes/categoriaRoutes.js`

```javascript
router.put('/:id', CategoriaController.update);
router.delete('/:id', CategoriaController.delete);
```

#### 🎯 Desafio 2: Testes Completos de CRUD (30 min)

**Testes de UPDATE:**

```bash
# 1. Atualizar username
PUT http://localhost:3000/usuarios/1
Body: { "username": "maria_silva" }
Esperado: 200 + usuário atualizado

# 2. Atualizar email
PUT http://localhost:3000/usuarios/1
Body: { "email": "maria.silva@email.com" }
Esperado: 200 + usuário atualizado

# 3. Atualizar para email duplicado
PUT http://localhost:3000/usuarios/1
Body: { "email": "outro@email.com" }  # email de outro usuário
Esperado: 409 + "Email já cadastrado"

# 4. Atualizar múltiplos campos
PUT http://localhost:3000/usuarios/1
Body: { "username": "maria123", "email": "maria123@email.com" }
Esperado: 200 + usuário atualizado

# 5. Atualizar usuário inexistente
PUT http://localhost:3000/usuarios/999
Body: { "username": "teste" }
Esperado: 404 + "Usuário não encontrado"

# 6. Atualizar sem campos
PUT http://localhost:3000/usuarios/1
Body: {}
Esperado: 400 + "Nenhum campo para atualizar"

# 7. Atualizar categoria
PUT http://localhost:3000/categorias/1
Body: { "nome": "Cinema e Filmes", "descricao": "Converse sobre cinema" }
Esperado: 200 + categoria atualizada

# 8. Desativar categoria
PUT http://localhost:3000/categorias/1
Body: { "ativa": false }
Esperado: 200 + categoria desativada
```

**Testes de DELETE:**

```bash
# 9. Criar usuário para deletar
POST http://localhost:3000/usuarios
Body: { "username": "temp", "email": "temp@email.com", "senha": "123456" }
Esperado: 201 + usuário criado (anotar ID)

# 10. Deletar usuário sem salas
DELETE http://localhost:3000/usuarios/{ID_TEMP}
Esperado: 204

# 11. Verificar se foi deletado
GET http://localhost:3000/usuarios/{ID_TEMP}
Esperado: 404

# 12. Tentar deletar usuário inexistente
DELETE http://localhost:3000/usuarios/999
Esperado: 404 + "Usuário não encontrado"

# 13. Criar sala para usuário (simular)
# Inserir manualmente no banco:
# INSERT INTO salas (categoria_id, usuario1_id, usuario2_id, ativa) VALUES (1, 1, 2, 1);

# 14. Tentar deletar usuário com sala ativa
DELETE http://localhost:3000/usuarios/1
Esperado: 400 + "Não é possível deletar usuário com salas ativas"

# 15. Criar categoria para deletar
POST http://localhost:3000/categorias
Body: { "nome": "Teste", "descricao": "Categoria teste" }
Esperado: 201 + categoria criada (anotar ID)

# 16. Deletar categoria sem salas
DELETE http://localhost:3000/categorias/{ID_CATEGORIA}
Esperado: 204

# 17. Tentar deletar categoria com salas ativas
DELETE http://localhost:3000/categorias/1
Esperado: 400 + "Não é possível deletar categoria com salas ativas"
```

**Checklist:**
- [ ] Todos os 17 testes executados
- [ ] UPDATE funcionando com validações
- [ ] DELETE verificando dependências
- [ ] Códigos de status corretos
- [ ] Mensagens de erro claras

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas para a Turma:**

1. **Qual a diferença entre hard delete e soft delete?**
   - Hard: remove permanentemente / Soft: marca como inativo

2. **Por que verificar dependências antes de deletar?**
   - Manter integridade referencial, evitar dados órfãos

3. **Como fazer UPDATE parcial?**
   - Construir SQL dinamicamente apenas com campos fornecidos

4. **O que é this.changes no SQLite?**
   - Número de linhas afetadas pela operação

#### 🎯 CRUD Completo

```
CREATE  → POST   /usuarios     → 201
READ    → GET    /usuarios     → 200
READ    → GET    /usuarios/:id → 200
UPDATE  → PUT    /usuarios/:id → 200
DELETE  → DELETE /usuarios/:id → 204

Validações:
✅ Dados obrigatórios
✅ Formato correto
✅ Unicidade (email, username)
✅ Dependências (salas ativas)
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Implementar UPDATE com validações
- [ ] Implementar DELETE com verificação de dependências
- [ ] Construir UPDATE dinâmico
- [ ] Verificar integridade referencial
- [ ] Tratar erros de constraint
- [ ] Testar CRUD completo
- [ ] Aplicar regras de negócio

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar soft delete para usuários
   - Implementar endpoint PATCH para atualização parcial
   - Criar endpoint GET /usuarios/:id/salas (listar salas do usuário)

2. **Estudo:**
   - Pesquisar sobre transações SQL
   - Estudar CASCADE DELETE

3. **Reflexão:**
   - Quando usar soft delete vs hard delete?
   - Como garantir consistência em operações múltiplas?

---

## 📊 Avaliação

### Critérios de Avaliação (Peso: 20% da UC 02 Part 03)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Operações UPDATE** | 30% | UPDATE funcionando com validações |
| **Operações DELETE** | 30% | DELETE com verificação de dependências |
| **Regras de Negócio** | 25% | Validações e integridade implementadas |
| **Testes** | 15% | CRUD completo testado |

### Instrumentos de Avaliação

1. **Observação durante prática** (formativa)
2. **Desafio 1 - Categorias CRUD** (somativa - 60%)
3. **Desafio 2 - Testes completos** (somativa - 40%)

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Revisar operações UPDATE e DELETE
- [ ] Preparar exemplos de integridade referencial
- [ ] Ter banco com dados de teste
- [ ] Preparar cenários de erro

### Durante a Aula
- [ ] Demonstrar UPDATE dinâmico no quadro
- [ ] Mostrar erro de foreign key constraint
- [ ] Explicar this.changes
- [ ] Circular durante testes

### Pontos de Atenção
- ⚠️ Alunos esquecem WHERE no UPDATE/DELETE (perigo!)
- ⚠️ Confusão entre this.changes e this.lastID
- ⚠️ Não verificam dependências antes de deletar
- ⚠️ Esquecem de validar se registro existe

### Troubleshooting Comum

**Problema:** "UPDATE não retorna dados atualizados"
**Solução:** Fazer SELECT após UPDATE

**Problema:** "DELETE não funciona por foreign key"
**Solução:** Verificar dependências ou usar CASCADE

**Problema:** "this.changes sempre 0"
**Solução:** Verificar se WHERE está correto

---

## 📎 Recursos Adicionais

### Links Úteis
- [SQLite UPDATE](https://www.sqlitetutorial.net/sqlite-update/)
- [SQLite DELETE](https://www.sqlitetutorial.net/sqlite-delete/)
- [Foreign Key Constraints](https://www.sqlitetutorial.net/sqlite-foreign-key/)

### Ferramentas
- DB Browser for SQLite
- Thunder Client

### Próxima Aula
**Aula 07-08 - Tratamento de Erros, Depuração e Qualidade**
- Try-catch avançado
- Logging
- Debugging com VS Code
- Testes unitários
- Refatoração para async/await

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
