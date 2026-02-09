# Aula 05 - Projeto MeetStranger: INSERT e UPDATE com Regras de Negócio

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas  
**Data:** 23/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Aplicar** regras de negócio em operações de banco de dados
2. **Implementar** inserções condicionais
3. **Executar** atualizações baseadas em critérios
4. **Garantir** integridade e consistência dos dados
5. **Simular** cenários reais do MeetStranger

---

## 📚 Conteúdos Programáticos

### 1. Regras de Negócio do MeetStranger (45 min)
- Análise de requisitos
- Validações necessárias
- Fluxos de dados
- Restrições de integridade

### 2. Inserções Condicionais (60 min)
- Validar antes de inserir
- Verificar duplicatas
- Inserir com dados relacionados
- Tratamento de erros

### 3. Atualizações com Critérios (60 min)
- UPDATE baseado em regras
- Atualização em cascata
- Manter histórico
- Validar antes de atualizar

### 4. Integridade de Dados (45 min)
- Consistência referencial
- Validações de negócio
- Transações complexas
- Rollback em caso de erro

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Contextualização (30 min)

**Atividade:** Análise de Regras de Negócio

**Regras do MeetStranger:**
```
CADASTRO:
✅ Username: 3-20 caracteres, único
✅ Email: formato válido, único
✅ Senha: 6+ caracteres
✅ Idade: 13+ anos (se implementado)

LOGIN:
✅ Credenciais corretas
✅ Atualizar ultimo_login
✅ Marcar como online

MATCHING:
✅ Usuário autenticado
✅ Não estar em sala ativa
✅ Categoria válida
✅ Não estar na fila

CHAT:
✅ Estar em sala ativa
✅ Sala com 2 usuários
✅ Atualizar estatísticas

LOGOUT:
✅ Marcar como offline
✅ Remover da fila (se estiver)
✅ Encerrar sala (se estiver)
```

**Discussão:**
- Por que essas regras são importantes?
- O que acontece se não validar?
- Como implementar no banco?

### Momento 2: Cadastro com Validações (60 min)

**Atividade 1:** Cadastro Simples vs Validado (20 min)

**❌ Cadastro SEM validação:**
```sql
-- Problema: Pode inserir dados inválidos
INSERT INTO usuarios (username, email, senha)
VALUES ('ab', 'email_invalido', '123');
-- Aceita username curto, email sem @, senha fraca
```

**✅ Cadastro COM validação:**
```sql
-- 1. Verificar se username já existe
SELECT COUNT(*) FROM usuarios WHERE username = 'joao123';
-- Se retornar 0, pode prosseguir

-- 2. Verificar se email já existe
SELECT COUNT(*) FROM usuarios WHERE email = 'joao@email.com';
-- Se retornar 0, pode prosseguir

-- 3. Validar formato (feito pelas restrições CHECK)
-- 4. Inserir
INSERT INTO usuarios (username, email, senha)
VALUES ('joao123', 'joao@email.com', 'senha123');

-- 5. Criar estatísticas
INSERT INTO estatisticas_usuario (usuario_id)
VALUES (LAST_INSERT_ROWID());
```

**Atividade 2:** Função de Cadastro Completa (25 min)
```sql
-- Cadastro completo com validações
BEGIN TRANSACTION;

-- Verificar duplicatas
SELECT CASE
    WHEN EXISTS (SELECT 1 FROM usuarios WHERE username = 'maria456') THEN 'Username já existe'
    WHEN EXISTS (SELECT 1 FROM usuarios WHERE email = 'maria@email.com') THEN 'Email já existe'
    ELSE 'OK'
END AS validacao;

-- Se validação = 'OK', inserir
INSERT INTO usuarios (username, email, senha)
SELECT 'maria456', 'maria@email.com', 'senha456'
WHERE NOT EXISTS (
    SELECT 1 FROM usuarios 
    WHERE username = 'maria456' OR email = 'maria@email.com'
);

-- Criar estatísticas
INSERT INTO estatisticas_usuario (usuario_id)
SELECT id FROM usuarios WHERE username = 'maria456';

COMMIT;

-- Verificar
SELECT u.*, e.* 
FROM usuarios u
LEFT JOIN estatisticas_usuario e ON u.id = e.usuario_id
WHERE u.username = 'maria456';
```

**Atividade 3:** Exercício Prático (15 min)
```
Cadastrar 3 usuários com validações:
1. Verificar duplicatas
2. Inserir usuário
3. Criar estatísticas
4. Confirmar inserção
```

### Momento 3: Login com Regras (60 min + 10 min intervalo)

**Atividade 1:** Fluxo de Login (20 min)
```sql
-- FLUXO DE LOGIN COMPLETO

-- 1. Verificar se usuário existe
SELECT id, senha FROM usuarios 
WHERE email = 'joao@email.com';
-- Se não retornar nada: "Usuário não encontrado"

-- 2. Verificar senha (em produção: comparar hash)
SELECT id FROM usuarios 
WHERE email = 'joao@email.com' 
  AND senha = 'senha123';
-- Se não retornar nada: "Senha incorreta"

-- 3. Atualizar dados de login
UPDATE usuarios
SET 
    ultimo_login = CURRENT_TIMESTAMP,
    online = TRUE
WHERE email = 'joao@email.com';

-- 4. Verificar sucesso
SELECT id, username, online, ultimo_login
FROM usuarios
WHERE email = 'joao@email.com';
```

**Atividade 2:** Login com Transação (20 min)
```sql
-- Login seguro com transação
BEGIN TRANSACTION;

-- Variáveis simuladas (em produção: parâmetros)
-- email_input = 'maria@email.com'
-- senha_input = 'senha456'

-- Buscar usuário
SELECT id, username, senha 
FROM usuarios 
WHERE email = 'maria@email.com';

-- Se encontrado e senha correta:
UPDATE usuarios
SET 
    ultimo_login = CURRENT_TIMESTAMP,
    online = TRUE
WHERE email = 'maria@email.com' 
  AND senha = 'senha456';

-- Verificar se atualizou (CHANGES() retorna linhas afetadas)
SELECT CHANGES() AS linhas_atualizadas;
-- Se 0: login falhou
-- Se 1: login sucesso

COMMIT;
```

**Atividade 3:** Exercício - Múltiplos Logins (20 min)
```
Simular login de 5 usuários:
1. Verificar credenciais
2. Atualizar ultimo_login
3. Marcar como online
4. Listar usuários online
```

### Momento 4: Matching com Validações (60 min)

**Atividade 1:** Entrar na Fila (20 min)
```sql
-- ENTRAR NA FILA DE MATCHING

-- Regras:
-- 1. Usuário deve estar online
-- 2. Não pode estar em sala ativa
-- 3. Não pode estar em outra fila
-- 4. Categoria deve ser válida

BEGIN TRANSACTION;

-- Validações
SELECT CASE
    WHEN NOT EXISTS (SELECT 1 FROM usuarios WHERE id = 1 AND online = TRUE)
        THEN 'Usuário não está online'
    WHEN EXISTS (SELECT 1 FROM salas WHERE (usuario1_id = 1 OR usuario2_id = 1) AND ativa = TRUE)
        THEN 'Usuário já está em sala ativa'
    WHEN EXISTS (SELECT 1 FROM fila_matching WHERE usuario_id = 1)
        THEN 'Usuário já está na fila'
    WHEN NOT EXISTS (SELECT 1 FROM categorias WHERE id = 1 AND ativa = TRUE)
        THEN 'Categoria inválida'
    ELSE 'OK'
END AS validacao;

-- Se validação = 'OK', inserir na fila
INSERT INTO fila_matching (usuario_id, categoria_id)
SELECT 1, 1
WHERE NOT EXISTS (
    SELECT 1 FROM fila_matching WHERE usuario_id = 1
)
AND EXISTS (
    SELECT 1 FROM usuarios WHERE id = 1 AND online = TRUE
)
AND NOT EXISTS (
    SELECT 1 FROM salas 
    WHERE (usuario1_id = 1 OR usuario2_id = 1) AND ativa = TRUE
);

COMMIT;

-- Verificar posição na fila
SELECT 
    f.id,
    u.username,
    c.nome AS categoria,
    f.entrou_em,
    (SELECT COUNT(*) FROM fila_matching f2 
     WHERE f2.categoria_id = f.categoria_id 
     AND f2.entrou_em < f.entrou_em) + 1 AS posicao
FROM fila_matching f
JOIN usuarios u ON f.usuario_id = u.id
JOIN categorias c ON f.categoria_id = c.id
WHERE f.usuario_id = 1;
```

**Atividade 2:** Criar Match (25 min)
```sql
-- CRIAR MATCH (SALA)

-- Regras:
-- 1. Deve haver 2 usuários na mesma categoria
-- 2. Ambos devem estar online
-- 3. Nenhum pode estar em sala ativa

BEGIN TRANSACTION;

-- Buscar 2 usuários na fila da mesma categoria
SELECT 
    f1.usuario_id AS usuario1_id,
    f2.usuario_id AS usuario2_id,
    f1.categoria_id
FROM fila_matching f1
JOIN fila_matching f2 ON f1.categoria_id = f2.categoria_id
WHERE f1.usuario_id < f2.usuario_id  -- Evitar duplicatas
  AND f1.id < f2.id  -- Primeiro da fila
LIMIT 1;

-- Se encontrou match, criar sala
INSERT INTO salas (categoria_id, usuario1_id, usuario2_id)
SELECT 1, 1, 2  -- Valores do SELECT acima
WHERE EXISTS (
    SELECT 1 FROM usuarios WHERE id = 1 AND online = TRUE
)
AND EXISTS (
    SELECT 1 FROM usuarios WHERE id = 2 AND online = TRUE
);

-- Remover da fila
DELETE FROM fila_matching
WHERE usuario_id IN (1, 2);

-- Atualizar estatísticas
UPDATE estatisticas_usuario
SET total_conversas = total_conversas + 1
WHERE usuario_id IN (1, 2);

COMMIT;

-- Verificar sala criada
SELECT 
    s.id AS sala_id,
    c.nome AS categoria,
    u1.username AS usuario1,
    u2.username AS usuario2,
    s.criada_em
FROM salas s
JOIN categorias c ON s.categoria_id = c.id
JOIN usuarios u1 ON s.usuario1_id = u1.id
JOIN usuarios u2 ON s.usuario2_id = u2.id
WHERE s.id = LAST_INSERT_ROWID();
```

**Atividade 3:** Exercício - Matching Completo (15 min)
```
Simular matching:
1. 4 usuários entram na fila (2 em Filmes, 2 em Jogos)
2. Criar 2 matches
3. Remover da fila
4. Atualizar estatísticas
5. Verificar salas criadas
```

### Momento 5: Atualização de Estatísticas (45 min)

**Atividade 1:** Atualizar Durante Conversa (15 min)
```sql
-- Atualizar tempo de conversa
UPDATE estatisticas_usuario
SET 
    tempo_total_minutos = tempo_total_minutos + 15,
    ultima_atualizacao = CURRENT_TIMESTAMP
WHERE usuario_id IN (
    SELECT usuario1_id FROM salas WHERE id = 1
    UNION
    SELECT usuario2_id FROM salas WHERE id = 1
);

-- Verificar
SELECT 
    u.username,
    e.total_conversas,
    e.tempo_total_minutos,
    e.ultima_atualizacao
FROM estatisticas_usuario e
JOIN usuarios u ON e.usuario_id = u.id
WHERE e.usuario_id IN (1, 2);
```

**Atividade 2:** Definir Categoria Favorita (15 min)
```sql
-- Calcular categoria mais usada por usuário
UPDATE estatisticas_usuario
SET categoria_favorita_id = (
    SELECT s.categoria_id
    FROM salas s
    WHERE s.usuario1_id = estatisticas_usuario.usuario_id
       OR s.usuario2_id = estatisticas_usuario.usuario_id
    GROUP BY s.categoria_id
    ORDER BY COUNT(*) DESC
    LIMIT 1
)
WHERE usuario_id = 1;

-- Verificar
SELECT 
    u.username,
    c.nome AS categoria_favorita,
    e.total_conversas
FROM estatisticas_usuario e
JOIN usuarios u ON e.usuario_id = u.id
LEFT JOIN categorias c ON e.categoria_favorita_id = c.id
WHERE e.usuario_id = 1;
```

**Atividade 3:** Exercício - Estatísticas Completas (15 min)
```
Para cada usuário em sala ativa:
1. Incrementar total_conversas
2. Adicionar 20 minutos ao tempo_total
3. Atualizar categoria_favorita
4. Atualizar ultima_atualizacao
```

### Momento 6: Logout e Limpeza (45 min)

**Atividade 1:** Logout Completo (20 min)
```sql
-- LOGOUT COM LIMPEZA

BEGIN TRANSACTION;

-- 1. Encerrar sala se estiver em uma
UPDATE salas
SET 
    ativa = FALSE,
    encerrada_em = CURRENT_TIMESTAMP
WHERE (usuario1_id = 1 OR usuario2_id = 1)
  AND ativa = TRUE;

-- 2. Remover da fila se estiver
DELETE FROM fila_matching
WHERE usuario_id = 1;

-- 3. Marcar como offline
UPDATE usuarios
SET online = FALSE
WHERE id = 1;

COMMIT;

-- Verificar
SELECT 
    u.username,
    u.online,
    CASE 
        WHEN EXISTS (SELECT 1 FROM salas WHERE (usuario1_id = u.id OR usuario2_id = u.id) AND ativa = TRUE)
        THEN 'Em sala'
        WHEN EXISTS (SELECT 1 FROM fila_matching WHERE usuario_id = u.id)
        THEN 'Na fila'
        ELSE 'Desconectado'
    END AS status
FROM usuarios u
WHERE u.id = 1;
```

**Atividade 2:** Limpeza Automática (15 min)
```sql
-- Limpar dados antigos

-- 1. Remover fila antiga (30+ minutos)
DELETE FROM fila_matching
WHERE entrou_em < DATETIME('now', '-30 minutes');

-- 2. Marcar usuários inativos como offline
UPDATE usuarios
SET online = FALSE
WHERE ultimo_login < DATETIME('now', '-1 hour')
  AND online = TRUE;

-- 3. Arquivar salas antigas (opcional)
UPDATE salas
SET ativa = FALSE
WHERE criada_em < DATETIME('now', '-2 hours')
  AND ativa = TRUE
  AND encerrada_em IS NULL;

-- Verificar limpeza
SELECT 'Fila limpa' AS acao, COUNT(*) AS registros_removidos
FROM fila_matching
WHERE entrou_em < DATETIME('now', '-30 minutes');
```

**Atividade 3:** Exercício - Cenário Completo (10 min)
```
Simular logout de 3 usuários:
1. Encerrar salas ativas
2. Remover da fila
3. Marcar como offline
4. Executar limpeza automática
```

### Momento 7: Projeto Integrador (60 min)

**Atividade:** Simulação Completa do MeetStranger

**Cenário: Dia típico no MeetStranger**

```sql
-- ============================================
-- SIMULAÇÃO COMPLETA - DIA NO MEETSTRANGER
-- ============================================

BEGIN TRANSACTION;

-- MANHÃ: Cadastros
INSERT INTO usuarios (username, email, senha) VALUES
    ('user_manha1', 'manha1@email.com', 'senha123'),
    ('user_manha2', 'manha2@email.com', 'senha456');

INSERT INTO estatisticas_usuario (usuario_id)
SELECT id FROM usuarios WHERE username LIKE 'user_manha%';

-- TARDE: Logins e Matching
UPDATE usuarios
SET online = TRUE, ultimo_login = CURRENT_TIMESTAMP
WHERE username IN ('user_manha1', 'user_manha2', 'alice_cinema', 'bob_gamer');

-- Entrar na fila
INSERT INTO fila_matching (usuario_id, categoria_id)
SELECT u.id, 1 FROM usuarios u WHERE u.username = 'user_manha1'
UNION
SELECT u.id, 1 FROM usuarios u WHERE u.username = 'alice_cinema';

-- Criar match
INSERT INTO salas (categoria_id, usuario1_id, usuario2_id)
SELECT 1, 
    (SELECT id FROM usuarios WHERE username = 'user_manha1'),
    (SELECT id FROM usuarios WHERE username = 'alice_cinema');

DELETE FROM fila_matching WHERE usuario_id IN (
    SELECT id FROM usuarios WHERE username IN ('user_manha1', 'alice_cinema')
);

-- Atualizar estatísticas
UPDATE estatisticas_usuario
SET total_conversas = total_conversas + 1
WHERE usuario_id IN (
    SELECT id FROM usuarios WHERE username IN ('user_manha1', 'alice_cinema')
);

-- NOITE: Logouts
UPDATE salas
SET ativa = FALSE, encerrada_em = CURRENT_TIMESTAMP
WHERE ativa = TRUE;

UPDATE usuarios
SET online = FALSE
WHERE online = TRUE;

-- LIMPEZA
DELETE FROM fila_matching WHERE entrou_em < DATETIME('now', '-30 minutes');

COMMIT;

-- RELATÓRIO FINAL
SELECT 'Total de usuários' AS metrica, COUNT(*) AS valor FROM usuarios
UNION ALL
SELECT 'Usuários online', COUNT(*) FROM usuarios WHERE online = TRUE
UNION ALL
SELECT 'Salas criadas hoje', COUNT(*) FROM salas WHERE DATE(criada_em) = DATE('now')
UNION ALL
SELECT 'Conversas ativas', COUNT(*) FROM salas WHERE ativa = TRUE;
```

### Momento 8: Fechamento (30 min)

**Atividade 1:** Síntese (15 min)
```
Regras de negócio implementadas:
✅ Cadastro com validações
✅ Login com atualizações
✅ Matching com verificações
✅ Estatísticas automáticas
✅ Logout com limpeza

Boas práticas aplicadas:
✅ Validar antes de inserir
✅ Usar transações
✅ Manter integridade
✅ Atualizar dados relacionados
✅ Limpar dados antigos
```

**Atividade 2:** Exercício para Casa (10 min)

**Atividade 3:** Preparação Próxima Aula (5 min)
- SELECT avançado
- Consultas complexas
- Relatórios

---

## 📝 Exercício para Casa

**Parte 1: Implementar Funcionalidade "Trocar de Parceiro"**

```sql
-- Cenário: Usuário quer trocar de parceiro

-- Regras:
-- 1. Deve estar em sala ativa
-- 2. Encerrar sala atual
-- 3. Voltar para fila
-- 4. Atualizar estatísticas

-- Implementar:
BEGIN TRANSACTION;
-- Seu código aqui
COMMIT;
```

**Parte 2: Sistema de Bloqueio**

```sql
-- Criar tabela de bloqueios
CREATE TABLE bloqueios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario_id INTEGER NOT NULL,
    bloqueado_id INTEGER NOT NULL,
    motivo TEXT,
    bloqueado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id),
    FOREIGN KEY (bloqueado_id) REFERENCES usuarios(id),
    UNIQUE (usuario_id, bloqueado_id),
    CHECK (usuario_id != bloqueado_id)
);

-- Implementar:
-- 1. Bloquear usuário
-- 2. Verificar se está bloqueado antes de criar match
-- 3. Listar usuários bloqueados
```

**Parte 3: Relatório de Uso**

```sql
-- Criar consultas para:
-- 1. Top 5 usuários mais ativos
-- 2. Categoria mais popular
-- 3. Horário de pico
-- 4. Tempo médio de conversa
```

**Formato de Entrega:**
- Arquivo .sql com implementações
- Documento .txt explicando decisões

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Formativa

**Critérios:**
- ✅ Aplica regras de negócio corretamente
- ✅ Valida dados antes de inserir
- ✅ Usa transações apropriadamente
- ✅ Mantém integridade referencial
- ✅ Atualiza dados relacionados
- ✅ Implementa limpeza de dados

**Peso da Aula:** 20% da nota da Parte 2

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Implementa validações antes de INSERT  
✅ Verifica duplicatas  
✅ Usa transações em operações complexas  
✅ Atualiza dados relacionados em cascata  
✅ Mantém consistência dos dados  
✅ Aplica regras de negócio corretamente  
✅ Simula cenários reais completos  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Banco MeetStranger completo
- [ ] Scripts de validação
- [ ] Cenários de teste
- [ ] Documentação de regras

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 70 min (com intervalo)
- ⏰ Momento 4: 60 min
- ⏰ Momento 5: 45 min
- ⏰ Momento 6: 45 min
- ⏰ Momento 7: 60 min
- ⏰ Momento 8: 30 min

### Pontos de Atenção
1. **Regras de Negócio**: Conectar sempre com requisitos
2. **Validações**: Enfatizar importância
3. **Transações**: Usar em operações complexas
4. **Integridade**: Manter sempre
5. **Cenários Reais**: Simular situações práticas

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
