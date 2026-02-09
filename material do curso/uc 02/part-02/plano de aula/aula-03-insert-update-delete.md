# Aula 03 - Manipulação de Dados: INSERT, UPDATE e DELETE

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas  
**Data:** 20/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Inserir** dados no banco usando INSERT
2. **Atualizar** registros existentes com UPDATE
3. **Excluir** dados de forma segura com DELETE
4. **Aplicar** boas práticas de manipulação de dados
5. **Identificar** riscos de operações incorretas

---

## 📚 Conteúdos Programáticos

### 1. Comando INSERT (60 min)
- Sintaxe básica
- Inserção de um registro
- Inserção múltipla
- Valores padrão e NULL

### 2. Comando UPDATE (60 min)
- Sintaxe e cláusula WHERE
- Atualização de um campo
- Atualização múltipla
- Riscos de UPDATE sem WHERE

### 3. Comando DELETE (45 min)
- Sintaxe e cláusula WHERE
- Exclusão controlada
- Riscos de DELETE sem WHERE
- Diferença entre DELETE e DROP

### 4. Boas Práticas e Segurança (45 min)
- Transações básicas
- Backup antes de operações críticas
- Validação de dados
- Testes em ambiente seguro

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Retomada e Contextualização (30 min)

**Revisão Rápida (15 min):**
```sql
-- Verificar estrutura criada
USE meetstranger;
SHOW TABLES;
DESCRIBE usuarios;

-- Verificar dados existentes
SELECT * FROM categorias;
```

**Problema Motivador (15 min):**
```
Situação: Banco criado, mas vazio

Perguntas:
- Como adicionar usuários?
- Como atualizar perfil?
- Como remover conta?
- O que acontece se errar?

Hoje: Operações de manipulação (CRUD)
```

### Momento 2: Comando INSERT (60 min)

**Atividade 1:** Sintaxe Básica (20 min)
```sql
-- Sintaxe completa
INSERT INTO tabela (coluna1, coluna2, coluna3)
VALUES (valor1, valor2, valor3);

-- Exemplo: Inserir usuário
INSERT INTO usuarios (username, email, senha)
VALUES ('joao123', 'joao@email.com', 'senha123');

-- Verificar inserção
SELECT * FROM usuarios;
```

**Atividade 2:** Inserção com Todos os Campos (15 min)
```sql
-- Especificando todas as colunas
INSERT INTO usuarios (
    username,
    email,
    senha,
    criado_em,
    ultimo_login,
    online
) VALUES (
    'maria456',
    'maria@email.com',
    'senha456',
    CURRENT_TIMESTAMP,
    NULL,
    FALSE
);

-- Ou deixar campos com valores padrão
INSERT INTO usuarios (username, email, senha)
VALUES ('pedro789', 'pedro@email.com', 'senha789');
-- criado_em, online usam valores DEFAULT
```

**Atividade 3:** Inserção Múltipla (15 min)
```sql
-- Inserir vários registros de uma vez
INSERT INTO usuarios (username, email, senha) VALUES
    ('ana111', 'ana@email.com', 'senha111'),
    ('carlos222', 'carlos@email.com', 'senha222'),
    ('julia333', 'julia@email.com', 'senha333'),
    ('bruno444', 'bruno@email.com', 'senha444');

-- Verificar
SELECT COUNT(*) FROM usuarios;
SELECT * FROM usuarios;
```

**Atividade 4:** Exercício Prático (10 min)
```
Inserir 3 usuários com dados fictícios:
- Escolher usernames únicos
- Emails válidos
- Senhas com 6+ caracteres
```

### Momento 3: Comando UPDATE (60 min + 10 min intervalo)

**Atividade 1:** Sintaxe e WHERE (20 min)
```sql
-- Sintaxe básica
UPDATE tabela
SET coluna1 = valor1, coluna2 = valor2
WHERE condição;

-- ⚠️ PERIGO: UPDATE sem WHERE atualiza TODOS os registros
UPDATE usuarios
SET senha = 'nova_senha';  -- TODOS os usuários!

-- ✅ CORRETO: UPDATE com WHERE
UPDATE usuarios
SET senha = 'nova_senha123'
WHERE id = 1;  -- Apenas usuário com id 1

-- Verificar
SELECT id, username, senha FROM usuarios WHERE id = 1;
```

**Atividade 2:** Atualizar Múltiplos Campos (15 min)
```sql
-- Atualizar vários campos de uma vez
UPDATE usuarios
SET 
    ultimo_login = CURRENT_TIMESTAMP,
    online = TRUE
WHERE username = 'joao123';

-- Atualizar baseado em condição
UPDATE usuarios
SET online = FALSE
WHERE ultimo_login < DATE('now', '-1 day');
```

**Atividade 3:** UPDATE com Cálculos (15 min)
```sql
-- Incrementar valor
UPDATE estatisticas_usuario
SET total_conversas = total_conversas + 1
WHERE usuario_id = 1;

-- Atualizar com base em outra coluna
UPDATE usuarios
SET email = LOWER(email)
WHERE email != LOWER(email);
```

**Atividade 4:** Exercício Prático (10 min)
```
1. Atualizar status online de um usuário
2. Atualizar ultimo_login para agora
3. Mudar email de um usuário específico
```

### Momento 4: Comando DELETE (45 min)

**Atividade 1:** Sintaxe e Riscos (20 min)
```sql
-- Sintaxe básica
DELETE FROM tabela
WHERE condição;

-- ⚠️ PERIGO EXTREMO: DELETE sem WHERE
DELETE FROM usuarios;  -- APAGA TODOS OS REGISTROS!

-- ✅ CORRETO: DELETE com WHERE
DELETE FROM usuarios
WHERE id = 10;

-- Verificar antes de deletar
SELECT * FROM usuarios WHERE id = 10;
-- Depois deletar
DELETE FROM usuarios WHERE id = 10;
-- Confirmar
SELECT * FROM usuarios WHERE id = 10;  -- Vazio
```

**Atividade 2:** DELETE com Condições (15 min)
```sql
-- Deletar registros antigos
DELETE FROM fila_matching
WHERE entrou_em < DATE('now', '-1 hour');

-- Deletar baseado em múltiplas condições
DELETE FROM salas
WHERE ativa = FALSE 
  AND encerrada_em < DATE('now', '-7 days');

-- Deletar com subconsulta (avançado)
DELETE FROM usuarios
WHERE id IN (
    SELECT usuario_id 
    FROM estatisticas_usuario 
    WHERE total_conversas = 0
);
```

**Atividade 3:** DELETE vs DROP vs TRUNCATE (10 min)
```sql
-- DELETE: Remove registros (pode usar WHERE)
DELETE FROM usuarios WHERE id = 1;

-- TRUNCATE: Remove TODOS os registros (mais rápido)
TRUNCATE TABLE usuarios;  -- Esvazia tabela

-- DROP: Remove a TABELA inteira
DROP TABLE usuarios;  -- Tabela deixa de existir

-- ⚠️ Cuidado: TRUNCATE e DROP são irreversíveis!
```

### Momento 5: Boas Práticas (45 min)

**Atividade 1:** Sempre Usar WHERE (10 min)
```sql
-- ❌ NUNCA faça isso em produção
UPDATE usuarios SET senha = '123456';
DELETE FROM usuarios;

-- ✅ SEMPRE use WHERE
UPDATE usuarios SET senha = '123456' WHERE id = 1;
DELETE FROM usuarios WHERE id = 1;

-- ✅ Verificar antes
SELECT * FROM usuarios WHERE id = 1;
-- Depois executar UPDATE ou DELETE
```

**Atividade 2:** Testar com SELECT (10 min)
```sql
-- Antes de UPDATE, testar com SELECT
SELECT * FROM usuarios WHERE username = 'joao123';
-- Se retornar o registro correto, fazer UPDATE
UPDATE usuarios SET online = TRUE WHERE username = 'joao123';

-- Antes de DELETE, testar com SELECT
SELECT * FROM salas WHERE ativa = FALSE;
-- Se retornar os registros corretos, fazer DELETE
DELETE FROM salas WHERE ativa = FALSE;
```

**Atividade 3:** Transações Básicas (15 min)
```sql
-- Iniciar transação
BEGIN TRANSACTION;

-- Executar operações
UPDATE usuarios SET online = FALSE WHERE id = 1;
DELETE FROM fila_matching WHERE usuario_id = 1;

-- Se tudo OK, confirmar
COMMIT;

-- Se algo errado, reverter
ROLLBACK;

-- Exemplo prático
BEGIN TRANSACTION;
DELETE FROM usuarios WHERE id = 999;
-- Ops, id errado!
ROLLBACK;  -- Desfaz a operação
```

**Atividade 4:** Backup e Segurança (10 min)
```sql
-- Criar backup de tabela
CREATE TABLE usuarios_backup AS
SELECT * FROM usuarios;

-- Restaurar se necessário
INSERT INTO usuarios
SELECT * FROM usuarios_backup;

-- Contar registros antes de operação crítica
SELECT COUNT(*) FROM usuarios;  -- Ex: 50
DELETE FROM usuarios WHERE online = FALSE;
SELECT COUNT(*) FROM usuarios;  -- Ex: 30 (deletou 20)
```

### Momento 6: Prática com MeetStranger (60 min)

**Atividade 1:** Cadastrar Usuários (15 min)
```sql
-- Inserir usuários de teste
INSERT INTO usuarios (username, email, senha) VALUES
    ('alice_films', 'alice@email.com', 'senha123'),
    ('bob_games', 'bob@email.com', 'senha456'),
    ('carol_series', 'carol@email.com', 'senha789'),
    ('david_films', 'david@email.com', 'senha012'),
    ('eve_games', 'eve@email.com', 'senha345');

-- Criar estatísticas para cada usuário
INSERT INTO estatisticas_usuario (usuario_id)
SELECT id FROM usuarios;
```

**Atividade 2:** Simular Login (15 min)
```sql
-- Usuário faz login
UPDATE usuarios
SET 
    ultimo_login = CURRENT_TIMESTAMP,
    online = TRUE
WHERE username = 'alice_films';

-- Verificar usuários online
SELECT username, ultimo_login, online
FROM usuarios
WHERE online = TRUE;
```

**Atividade 3:** Simular Matching (15 min)
```sql
-- Usuários entram na fila
INSERT INTO fila_matching (usuario_id, categoria_id) VALUES
    (1, 1),  -- alice em Filmes
    (2, 2),  -- bob em Jogos
    (3, 3);  -- carol em Séries

-- Criar sala quando há match
INSERT INTO salas (categoria_id, usuario1_id, usuario2_id)
VALUES (1, 1, 4);  -- alice e david em Filmes

-- Remover da fila
DELETE FROM fila_matching
WHERE usuario_id IN (1, 4);

-- Atualizar estatísticas
UPDATE estatisticas_usuario
SET total_conversas = total_conversas + 1
WHERE usuario_id IN (1, 4);
```

**Atividade 4:** Simular Logout (15 min)
```sql
-- Usuário sai do chat
UPDATE salas
SET 
    ativa = FALSE,
    encerrada_em = CURRENT_TIMESTAMP
WHERE id = 1;

-- Usuário faz logout
UPDATE usuarios
SET online = FALSE
WHERE id = 1;

-- Limpar fila antiga
DELETE FROM fila_matching
WHERE entrou_em < DATETIME('now', '-30 minutes');
```

### Momento 7: Exercícios Práticos (45 min)

**Exercício 1:** CRUD Completo de Usuário (15 min)
```sql
-- CREATE (Insert)
INSERT INTO usuarios (username, email, senha)
VALUES ('teste_user', 'teste@email.com', 'senha999');

-- READ (Select - próxima aula)
SELECT * FROM usuarios WHERE username = 'teste_user';

-- UPDATE
UPDATE usuarios
SET email = 'novo_email@email.com'
WHERE username = 'teste_user';

-- DELETE
DELETE FROM usuarios WHERE username = 'teste_user';
```

**Exercício 2:** Gerenciar Fila (15 min)
```
1. Adicionar 3 usuários na fila de "Jogos"
2. Verificar quantos estão na fila
3. Remover o primeiro da fila
4. Limpar toda a fila de "Jogos"
```

**Exercício 3:** Atualizar Estatísticas (15 min)
```
1. Incrementar total_conversas de um usuário
2. Atualizar tempo_total_minutos
3. Definir categoria_favorita_id
4. Atualizar ultima_atualizacao
```

### Momento 8: Fechamento (30 min)

**Atividade 1:** Síntese (15 min)
```
Comandos aprendidos:
✅ INSERT - Adicionar dados
✅ UPDATE - Modificar dados
✅ DELETE - Remover dados

Boas práticas:
✅ Sempre usar WHERE
✅ Testar com SELECT antes
✅ Usar transações
✅ Fazer backup
```

**Atividade 2:** Discussão de Riscos (10 min)
- O que acontece se deletar usuário com salas ativas?
- Como garantir integridade dos dados?
- Quando usar CASCADE?

**Atividade 3:** Exercício para Casa (5 min)

---

## 📝 Atividades Práticas

### Script Completo: Populando MeetStranger

```sql
-- ============================================
-- POPULAR BANCO MEETSTRANGER
-- ============================================

USE meetstranger;

-- 1. INSERIR USUÁRIOS
INSERT INTO usuarios (username, email, senha) VALUES
    ('alice_cinema', 'alice@email.com', 'senha123'),
    ('bob_gamer', 'bob@email.com', 'senha456'),
    ('carol_series', 'carol@email.com', 'senha789'),
    ('david_movies', 'david@email.com', 'senha012'),
    ('eve_player', 'eve@email.com', 'senha345'),
    ('frank_tv', 'frank@email.com', 'senha678'),
    ('grace_films', 'grace@email.com', 'senha901'),
    ('henry_games', 'henry@email.com', 'senha234');

-- 2. CRIAR ESTATÍSTICAS PARA TODOS
INSERT INTO estatisticas_usuario (usuario_id)
SELECT id FROM usuarios;

-- 3. SIMULAR LOGINS
UPDATE usuarios
SET 
    ultimo_login = CURRENT_TIMESTAMP,
    online = TRUE
WHERE id IN (1, 2, 3, 4);

-- 4. ADICIONAR À FILA
INSERT INTO fila_matching (usuario_id, categoria_id) VALUES
    (1, 1),  -- alice em Filmes
    (4, 1),  -- david em Filmes
    (2, 2),  -- bob em Jogos
    (5, 2);  -- eve em Jogos

-- 5. CRIAR SALAS (MATCHES)
INSERT INTO salas (categoria_id, usuario1_id, usuario2_id) VALUES
    (1, 1, 4),  -- alice e david em Filmes
    (2, 2, 5);  -- bob e eve em Jogos

-- 6. REMOVER DA FILA (JÁ ESTÃO EM SALA)
DELETE FROM fila_matching
WHERE usuario_id IN (1, 4, 2, 5);

-- 7. ATUALIZAR ESTATÍSTICAS
UPDATE estatisticas_usuario
SET 
    total_conversas = total_conversas + 1,
    tempo_total_minutos = tempo_total_minutos + 15
WHERE usuario_id IN (1, 4, 2, 5);

-- 8. VERIFICAR DADOS
SELECT 'Usuários online:' AS info;
SELECT username, online FROM usuarios WHERE online = TRUE;

SELECT 'Salas ativas:' AS info;
SELECT s.id, c.nome AS categoria, 
       u1.username AS usuario1, 
       u2.username AS usuario2
FROM salas s
JOIN categorias c ON s.categoria_id = c.id
JOIN usuarios u1 ON s.usuario1_id = u1.id
JOIN usuarios u2 ON s.usuario2_id = u2.id
WHERE s.ativa = TRUE;

SELECT 'Fila de matching:' AS info;
SELECT u.username, c.nome AS categoria
FROM fila_matching f
JOIN usuarios u ON f.usuario_id = u.id
JOIN categorias c ON f.categoria_id = c.id;
```

### Exercício para Casa

**Parte 1: Cenários de Uso**

Implementar os seguintes cenários:

**Cenário 1: Novo Usuário**
```sql
-- 1. Cadastrar usuário
-- 2. Criar estatísticas
-- 3. Fazer primeiro login
-- 4. Entrar na fila de "Séries"
```

**Cenário 2: Usuário Ativo**
```sql
-- 1. Fazer login
-- 2. Entrar na fila
-- 3. Criar sala (match)
-- 4. Atualizar estatísticas
-- 5. Encerrar sala
-- 6. Fazer logout
```

**Cenário 3: Limpeza de Dados**
```sql
-- 1. Remover usuários inativos (sem login há 30+ dias)
-- 2. Limpar fila antiga (30+ minutos)
-- 3. Arquivar salas encerradas (7+ dias)
```

**Parte 2: Operações Críticas**

Para cada operação, escrever:
1. SELECT para verificar antes
2. Comando de manipulação (INSERT/UPDATE/DELETE)
3. SELECT para confirmar depois

**Operações:**
- Deletar usuário (considerar integridade referencial)
- Atualizar email (verificar se já existe)
- Limpar todas as salas inativas

**Parte 3: Análise de Riscos**

Responder:
1. O que acontece se deletar usuário que está em sala ativa?
2. Como evitar UPDATE/DELETE acidental de todos os registros?
3. Quando usar CASCADE nas chaves estrangeiras?

**Formato de Entrega:**
- Arquivo .sql com todos os comandos
- Documento .txt com análise de riscos

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Compreensão da estrutura do banco
- Conhecimento de SQL básico

### Avaliação Formativa

**Critérios:**
- ✅ Insere dados corretamente
- ✅ Atualiza com WHERE apropriado
- ✅ Deleta de forma segura
- ✅ Testa antes de executar
- ✅ Usa transações quando necessário
- ✅ Identifica riscos de operações

**Instrumentos:**
- Exercícios práticos
- Observação durante atividades
- Qualidade dos comandos SQL

### Avaliação Somativa
- Exercícios em aula: 40%
- Exercício para casa: 60%

**Peso da Aula:** 20% da nota da Parte 2

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Insere dados com sintaxe correta  
✅ Usa UPDATE com WHERE sempre  
✅ Deleta dados de forma controlada  
✅ Testa operações com SELECT antes  
✅ Identifica riscos de operações sem WHERE  
✅ Aplica transações em operações críticas  
✅ Mantém integridade referencial  
✅ Documenta operações realizadas  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Computadores com SQLite
- [ ] Banco MeetStranger criado (aula anterior)
- [ ] VS Code configurado
- [ ] Projetor/TV
- [ ] Quadro branco
- [ ] Scripts de exemplo

### Comandos de Referência Rápida

```sql
-- INSERT
INSERT INTO tabela (col1, col2) VALUES (val1, val2);

-- UPDATE
UPDATE tabela SET col1 = val1 WHERE condição;

-- DELETE
DELETE FROM tabela WHERE condição;

-- TRANSACTION
BEGIN TRANSACTION;
-- comandos
COMMIT;  -- ou ROLLBACK;
```

### Referências
- SQLite INSERT: https://www.sqlite.org/lang_insert.html
- SQLite UPDATE: https://www.sqlite.org/lang_update.html
- SQLite DELETE: https://www.sqlite.org/lang_delete.html

---

## 🔄 Conexão com Outras Aulas

### Revisão da Aula 02
- Estrutura do banco MeetStranger
- Tabelas criadas
- Chaves primárias e estrangeiras

### Preparação para Aula 04
- Revisão técnica ou projeto integrador
- Consolidação de CREATE e CRUD
- Ajustes e melhorias

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 70 min (com intervalo)
- ⏰ Momento 4: 45 min
- ⏰ Momento 5: 45 min
- ⏰ Momento 6: 60 min
- ⏰ Momento 7: 45 min
- ⏰ Momento 8: 30 min

### Pontos de Atenção
1. **WHERE é OBRIGATÓRIO**: Enfatizar sempre
2. **Testar antes**: SELECT antes de UPDATE/DELETE
3. **Transações**: Mostrar utilidade prática
4. **Integridade**: Explicar CASCADE
5. **Backup**: Sempre antes de operações críticas

### Estratégias
- Demonstrar erros comuns ao vivo
- Mostrar como recuperar de erros
- Usar dados reais do MeetStranger
- Simular cenários completos
- Deixar estudantes errarem em ambiente seguro

### Adaptações
- **Turma iniciante**: Mais tempo em INSERT
- **Turma avançada**: Subconsultas em UPDATE/DELETE
- **EAD**: Gravar demonstrações de erros comuns

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Verificar banco MeetStranger criado
- [ ] Preparar scripts de exemplo
- [ ] Criar backup do banco
- [ ] Testar todos os comandos
- [ ] Preparar cenários de erro

### Durante a Aula
- [ ] Revisar aula anterior
- [ ] Demonstrar INSERT
- [ ] Ensinar UPDATE com cuidado
- [ ] Alertar sobre riscos de DELETE
- [ ] Praticar com dados reais
- [ ] Simular cenários completos
- [ ] Entregar exercício para casa

### Após a Aula
- [ ] Registrar frequência
- [ ] Salvar estado do banco
- [ ] Anotar dificuldades
- [ ] Preparar próxima aula

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Compreensão:
- INSERT: ___/10
- UPDATE: ___/10
- DELETE: ___/10
- Boas práticas: ___/10

Erros comuns observados:
- 

Dificuldades:
- 

Banco populado com sucesso: Sim ( ) Não ( )

Ajustes necessários:
- 

Tempo real: _____ min
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
