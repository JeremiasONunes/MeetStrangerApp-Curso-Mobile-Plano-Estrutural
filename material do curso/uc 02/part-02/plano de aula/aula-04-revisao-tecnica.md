# Aula 04 - Revisão Técnica e Projeto Integrador (Aula Extra)

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas (não contabilizada na UC)  
**Data:** 21/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Consolidar** conhecimentos de CREATE e CRUD
2. **Corrigir** falhas de modelagem identificadas
3. **Refinar** estrutura do banco MeetStranger
4. **Executar** operações completas com segurança
5. **Resolver** dúvidas individuais e em grupo

---

## 📚 Conteúdos Programáticos

### 1. Revisão de CREATE (45 min)
- CREATE DATABASE
- CREATE TABLE
- Tipos de dados
- Chaves primárias e estrangeiras
- Restrições (CHECK, UNIQUE, NOT NULL)

### 2. Revisão de CRUD (60 min)
- INSERT (simples e múltiplo)
- UPDATE (com WHERE)
- DELETE (controlado)
- SELECT básico (preparação para próxima aula)

### 3. Ajustes Estruturais (60 min)
- Identificar problemas na modelagem
- Corrigir estruturas
- Adicionar campos faltantes
- Melhorar restrições

### 4. Prática Orientada (75 min)
- Atendimento individual
- Trabalho em grupos
- Resolução de exercícios
- Projeto integrador

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Diagnóstico e Planejamento (30 min)

**Atividade 1:** Avaliação Diagnóstica (15 min)
```
Questionário rápido (oral ou escrito):

1. Como criar um banco de dados?
2. Como criar uma tabela com chave primária?
3. Como inserir dados?
4. Como atualizar um registro específico?
5. Como deletar com segurança?
6. O que é chave estrangeira?
7. Para que serve WHERE?
8. O que é transação?

Objetivo: Identificar dificuldades comuns
```

**Atividade 2:** Planejamento da Aula (15 min)
- Listar dúvidas da turma
- Priorizar tópicos
- Organizar grupos de trabalho
- Definir metas individuais

### Momento 2: Revisão de CREATE (45 min)

**Atividade 1:** Recapitulação Teórica (15 min)
```sql
-- Estrutura básica
CREATE DATABASE nome_banco;

CREATE TABLE nome_tabela (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    campo1 TIPO NOT NULL,
    campo2 TIPO UNIQUE,
    campo3 TIPO DEFAULT valor,
    
    FOREIGN KEY (campo_fk) REFERENCES outra_tabela(id),
    CHECK (condição)
);
```

**Atividade 2:** Exercício Prático (20 min)
```
Criar banco "revisao_db" com tabela "produtos":
- id (PK, auto-incremento)
- nome (texto, obrigatório, único)
- preco (decimal, obrigatório, > 0)
- estoque (inteiro, padrão 0, >= 0)
- ativo (booleano, padrão verdadeiro)
```

**Atividade 3:** Correção Coletiva (10 min)
- Apresentar soluções
- Discutir alternativas
- Identificar erros comuns

### Momento 3: Revisão de CRUD (60 min)

**Atividade 1:** INSERT - Teoria e Prática (15 min)
```sql
-- Inserir um registro
INSERT INTO produtos (nome, preco, estoque)
VALUES ('Notebook', 2500.00, 10);

-- Inserir múltiplos
INSERT INTO produtos (nome, preco, estoque) VALUES
    ('Mouse', 50.00, 100),
    ('Teclado', 150.00, 50),
    ('Monitor', 800.00, 20);

-- Verificar
SELECT * FROM produtos;
```

**Atividade 2:** UPDATE - Teoria e Prática (15 min)
```sql
-- ⚠️ Sempre testar com SELECT primeiro
SELECT * FROM produtos WHERE id = 1;

-- Atualizar
UPDATE produtos
SET preco = 2400.00, estoque = 8
WHERE id = 1;

-- Confirmar
SELECT * FROM produtos WHERE id = 1;
```

**Atividade 3:** DELETE - Teoria e Prática (15 min)
```sql
-- ⚠️ Sempre testar com SELECT primeiro
SELECT * FROM produtos WHERE estoque = 0;

-- Deletar
DELETE FROM produtos WHERE estoque = 0;

-- Confirmar
SELECT * FROM produtos WHERE estoque = 0;  -- Vazio
```

**Atividade 4:** Exercício Completo (15 min)
```
CRUD completo em "produtos":
1. Inserir 3 produtos
2. Atualizar preço de um
3. Deletar produto inativo
4. Listar todos
```

### Momento 4: Ajustes no MeetStranger (60 min + 10 min intervalo)

**Atividade 1:** Análise da Estrutura Atual (20 min)
```sql
-- Verificar estrutura
USE meetstranger;
SHOW TABLES;

-- Analisar cada tabela
DESCRIBE usuarios;
DESCRIBE categorias;
DESCRIBE salas;
DESCRIBE fila_matching;
DESCRIBE estatisticas_usuario;

-- Verificar dados
SELECT COUNT(*) FROM usuarios;
SELECT * FROM categorias;
```

**Atividade 2:** Identificar Problemas (20 min)

**Checklist de Validação:**
```
Estrutura:
□ Todas as tabelas necessárias existem?
□ Campos suficientes em cada tabela?
□ Tipos de dados adequados?
□ Chaves primárias definidas?
□ Chaves estrangeiras corretas?

Restrições:
□ NOT NULL nos campos obrigatórios?
□ UNIQUE nos campos únicos?
□ CHECK para validações?
□ DEFAULT para valores padrão?

Dados:
□ Categorias cadastradas?
□ Dados de teste inseridos?
□ Integridade mantida?
```

**Atividade 3:** Implementar Correções (20 min)

**Problemas Comuns e Soluções:**

**Problema 1: Campo faltante**
```sql
-- Adicionar campo
ALTER TABLE usuarios
ADD COLUMN telefone TEXT;

-- Verificar
DESCRIBE usuarios;
```

**Problema 2: Restrição faltante**
```sql
-- Não é possível adicionar CHECK em SQLite após criação
-- Solução: Recriar tabela

-- 1. Criar tabela temporária com estrutura correta
CREATE TABLE usuarios_temp (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    email TEXT NOT NULL UNIQUE,
    senha TEXT NOT NULL,
    telefone TEXT,
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    ultimo_login DATETIME,
    online BOOLEAN DEFAULT FALSE,
    
    CHECK (LENGTH(username) >= 3),
    CHECK (LENGTH(senha) >= 6)
);

-- 2. Copiar dados
INSERT INTO usuarios_temp
SELECT * FROM usuarios;

-- 3. Remover tabela antiga
DROP TABLE usuarios;

-- 4. Renomear
ALTER TABLE usuarios_temp RENAME TO usuarios;
```

**Problema 3: Dados inconsistentes**
```sql
-- Limpar dados inválidos
DELETE FROM usuarios
WHERE LENGTH(username) < 3;

-- Corrigir dados
UPDATE usuarios
SET email = LOWER(email)
WHERE email != LOWER(email);
```

### Momento 5: Prática Orientada Individual (45 min)

**Atividade:** Atendimento Personalizado

**Estação 1: Dúvidas de CREATE**
- Ajudar com criação de tabelas
- Explicar tipos de dados
- Esclarecer chaves estrangeiras

**Estação 2: Dúvidas de CRUD**
- Praticar INSERT, UPDATE, DELETE
- Resolver erros de sintaxe
- Explicar WHERE

**Estação 3: Projeto MeetStranger**
- Ajudar com estrutura específica
- Corrigir modelagem
- Validar implementação

**Rotação:**
- Estudantes circulam conforme necessidade
- Docente atende individualmente
- Monitores auxiliam (se disponíveis)

### Momento 6: Trabalho em Grupos (45 min)

**Atividade:** Projeto Integrador

**Dividir turma em 4 grupos:**

**Grupo 1: Módulo de Usuários**
```
Tarefas:
1. Validar estrutura da tabela usuarios
2. Inserir 10 usuários de teste
3. Implementar login (UPDATE)
4. Implementar logout (UPDATE)
5. Deletar usuário inativo
```

**Grupo 2: Módulo de Matching**
```
Tarefas:
1. Validar tabelas fila_matching e salas
2. Adicionar usuários à fila
3. Criar salas (matches)
4. Remover da fila
5. Encerrar salas
```

**Grupo 3: Módulo de Estatísticas**
```
Tarefas:
1. Validar tabela estatisticas_usuario
2. Criar estatísticas para todos os usuários
3. Atualizar total_conversas
4. Atualizar tempo_total_minutos
5. Definir categoria_favorita
```

**Grupo 4: Módulo de Categorias**
```
Tarefas:
1. Validar tabela categorias
2. Verificar categorias padrão
3. Adicionar nova categoria (opcional)
4. Contar usuários por categoria
5. Identificar categoria mais popular
```

### Momento 7: Apresentação e Validação (30 min)

**Atividade 1:** Apresentação dos Grupos (20 min)
- Cada grupo apresenta (5 min)
- Demonstrar comandos executados
- Mostrar resultados
- Explicar dificuldades

**Atividade 2:** Validação Coletiva (10 min)
```sql
-- Verificar integridade geral
SELECT 'Total de usuários:' AS info, COUNT(*) AS total FROM usuarios;
SELECT 'Usuários online:' AS info, COUNT(*) AS total FROM usuarios WHERE online = TRUE;
SELECT 'Salas ativas:' AS info, COUNT(*) AS total FROM salas WHERE ativa = TRUE;
SELECT 'Fila de matching:' AS info, COUNT(*) AS total FROM fila_matching;

-- Verificar integridade referencial
SELECT 'Salas sem usuários válidos:' AS problema, COUNT(*) AS total
FROM salas s
WHERE NOT EXISTS (SELECT 1 FROM usuarios WHERE id = s.usuario1_id)
   OR NOT EXISTS (SELECT 1 FROM usuarios WHERE id = s.usuario2_id);
```

### Momento 8: Consolidação e Encerramento (30 min)

**Atividade 1:** Síntese dos Aprendizados (15 min)
```
O que consolidamos:
✅ CREATE DATABASE e CREATE TABLE
✅ Tipos de dados e restrições
✅ Chaves primárias e estrangeiras
✅ INSERT, UPDATE, DELETE
✅ Boas práticas (WHERE, transações)
✅ Estrutura completa do MeetStranger

Próximos passos:
→ Aula 05: SELECT avançado
→ Consultas complexas
→ Filtros e ordenação
```

**Atividade 2:** Feedback da Turma (10 min)
- O que ficou mais claro?
- Quais dúvidas persistem?
- Sugestões de melhoria

**Atividade 3:** Preparação para Próxima Aula (5 min)
- Revisar comandos SELECT básicos
- Estudar cláusulas WHERE e ORDER BY
- Preparar dúvidas

---

## 📝 Atividades Práticas

### Exercício de Revisão Completo

```sql
-- ============================================
-- EXERCÍCIO DE REVISÃO COMPLETA
-- ============================================

-- 1. CRIAR BANCO E ESTRUTURA
CREATE DATABASE loja_revisao;
USE loja_revisao;

CREATE TABLE clientes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    telefone TEXT,
    ativo BOOLEAN DEFAULT TRUE,
    cadastrado_em DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE pedidos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    cliente_id INTEGER NOT NULL,
    valor_total REAL NOT NULL,
    status TEXT DEFAULT 'pendente',
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (cliente_id) REFERENCES clientes(id),
    CHECK (valor_total > 0),
    CHECK (status IN ('pendente', 'pago', 'cancelado'))
);

-- 2. INSERIR DADOS
INSERT INTO clientes (nome, email, telefone) VALUES
    ('João Silva', 'joao@email.com', '11999999999'),
    ('Maria Santos', 'maria@email.com', '11988888888'),
    ('Pedro Oliveira', 'pedro@email.com', '11977777777');

INSERT INTO pedidos (cliente_id, valor_total, status) VALUES
    (1, 150.00, 'pago'),
    (1, 200.00, 'pendente'),
    (2, 350.00, 'pago'),
    (3, 100.00, 'pendente');

-- 3. ATUALIZAR DADOS
UPDATE pedidos
SET status = 'pago'
WHERE id = 2;

UPDATE clientes
SET telefone = '11966666666'
WHERE email = 'joao@email.com';

-- 4. DELETAR DADOS
DELETE FROM pedidos
WHERE status = 'cancelado';

-- 5. CONSULTAR DADOS
SELECT * FROM clientes;
SELECT * FROM pedidos;
SELECT * FROM pedidos WHERE status = 'pago';
```

### Checklist de Validação do MeetStranger

```sql
-- ============================================
-- CHECKLIST DE VALIDAÇÃO
-- ============================================

-- 1. ESTRUTURA
SHOW TABLES;
-- Esperado: usuarios, categorias, salas, fila_matching, estatisticas_usuario

-- 2. DADOS BÁSICOS
SELECT COUNT(*) AS total_usuarios FROM usuarios;
-- Esperado: >= 5

SELECT * FROM categorias;
-- Esperado: Filmes, Jogos, Séries

-- 3. INTEGRIDADE REFERENCIAL
SELECT 'Salas com usuários inválidos' AS problema, COUNT(*) AS total
FROM salas s
WHERE NOT EXISTS (SELECT 1 FROM usuarios WHERE id = s.usuario1_id)
   OR NOT EXISTS (SELECT 1 FROM usuarios WHERE id = s.usuario2_id);
-- Esperado: 0

SELECT 'Fila com usuários inválidos' AS problema, COUNT(*) AS total
FROM fila_matching f
WHERE NOT EXISTS (SELECT 1 FROM usuarios WHERE id = f.usuario_id);
-- Esperado: 0

-- 4. RESTRIÇÕES
-- Tentar inserir usuário inválido (deve falhar)
INSERT INTO usuarios (username, email, senha)
VALUES ('ab', 'teste@email.com', '123');  -- username < 3 caracteres
-- Esperado: Erro

-- 5. DADOS CONSISTENTES
SELECT 'Usuários sem estatísticas' AS problema, COUNT(*) AS total
FROM usuarios u
WHERE NOT EXISTS (SELECT 1 FROM estatisticas_usuario WHERE usuario_id = u.id);
-- Esperado: 0
```

### Exercício de Correção

**Cenário:** Banco com problemas identificados

```sql
-- PROBLEMA 1: Usuários com username inválido
SELECT * FROM usuarios WHERE LENGTH(username) < 3;
-- Solução: Deletar ou corrigir

-- PROBLEMA 2: Emails duplicados (case-insensitive)
SELECT email, COUNT(*) 
FROM usuarios 
GROUP BY LOWER(email) 
HAVING COUNT(*) > 1;
-- Solução: Manter apenas um

-- PROBLEMA 3: Salas sem usuários
SELECT s.* 
FROM salas s
LEFT JOIN usuarios u1 ON s.usuario1_id = u1.id
LEFT JOIN usuarios u2 ON s.usuario2_id = u2.id
WHERE u1.id IS NULL OR u2.id IS NULL;
-- Solução: Deletar salas órfãs

-- PROBLEMA 4: Fila antiga
SELECT * FROM fila_matching
WHERE entrou_em < DATETIME('now', '-1 hour');
-- Solução: Limpar fila
```

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Questionário inicial
- Identificação de dificuldades
- Mapeamento de conhecimentos

### Avaliação Formativa

**Critérios:**
- ✅ Participa ativamente
- ✅ Resolve exercícios propostos
- ✅ Corrige erros identificados
- ✅ Colabora com grupo
- ✅ Tira dúvidas
- ✅ Ajuda colegas

**Instrumentos:**
- Observação durante atividades
- Qualidade do trabalho em grupo
- Resolução de exercícios
- Participação nas discussões

### Avaliação Somativa
**Não há nota formal** (aula extra de reforço)
- Feedback qualitativo
- Identificação de progressos
- Orientações individuais

---

## 🎯 Indicadores de Desempenho

O estudante demonstra consolidação quando:

✅ Cria bancos e tabelas sem consultar material  
✅ Insere dados corretamente  
✅ Atualiza com WHERE sempre  
✅ Deleta de forma segura  
✅ Identifica e corrige erros  
✅ Valida integridade dos dados  
✅ Trabalha colaborativamente  
✅ Resolve problemas de forma autônoma  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Computadores com SQLite
- [ ] Banco MeetStranger (aulas anteriores)
- [ ] VS Code configurado
- [ ] Quadro branco
- [ ] Exercícios impressos
- [ ] Checklist de validação

### Materiais de Apoio
- Resumo de comandos SQL
- Guia de boas práticas
- Checklist de validação
- Scripts de correção

---

## 🔄 Conexão com Outras Aulas

### Revisão das Aulas 01-03
- CREATE DATABASE e TABLE
- INSERT, UPDATE, DELETE
- Chaves e restrições
- Estrutura do MeetStranger

### Preparação para Aula 05
- SELECT básico
- WHERE e ORDER BY
- Consultas no MeetStranger

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 45 min
- ⏰ Momento 3: 60 min
- ⏰ Momento 4: 70 min (com intervalo)
- ⏰ Momento 5: 45 min
- ⏰ Momento 6: 45 min
- ⏰ Momento 7: 30 min
- ⏰ Momento 8: 30 min

### Pontos de Atenção
1. **Aula de Reforço**: Foco em dificuldades
2. **Atendimento Individual**: Priorizar quem mais precisa
3. **Ambiente Seguro**: Permitir erros
4. **Colaboração**: Incentivar ajuda mútua
5. **Validação**: Garantir que todos avançam

### Estratégias
- Identificar dificuldades no início
- Adaptar conteúdo conforme necessidade
- Circular pela sala constantemente
- Dar feedback imediato
- Celebrar progressos

### Adaptações
- **Turma com muitas dúvidas**: Mais tempo em revisão
- **Turma avançada**: Desafios extras
- **Grupos mistos**: Peer teaching

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Preparar diagnóstico inicial
- [ ] Revisar dificuldades das aulas anteriores
- [ ] Preparar exercícios de reforço
- [ ] Organizar estações de atendimento
- [ ] Preparar material de apoio

### Durante a Aula
- [ ] Aplicar diagnóstico
- [ ] Revisar CREATE e CRUD
- [ ] Corrigir estrutura do MeetStranger
- [ ] Atender individualmente
- [ ] Facilitar trabalho em grupos
- [ ] Validar aprendizados

### Após a Aula
- [ ] Registrar frequência
- [ ] Anotar progressos individuais
- [ ] Identificar quem precisa de mais apoio
- [ ] Preparar próxima aula

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Diagnóstico inicial:
- Dificuldades principais:
  1. 
  2. 
  3. 

Progressos observados:
- 

Estudantes que precisam de mais apoio:
- 

Ajustes realizados:
- 

Feedback da turma:
- 

Preparação para próxima aula:
- 
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação  
**Observação:** Aula extra de caráter formativo (não contabilizada na carga horária)
