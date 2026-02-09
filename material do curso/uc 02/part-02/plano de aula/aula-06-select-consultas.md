# Aula 06 - Consultas SQL: SELECT em Tabelas

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas  
**Data:** 24/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Recuperar** dados usando SELECT
2. **Filtrar** resultados com WHERE
3. **Ordenar** dados com ORDER BY
4. **Aplicar** funções de agregação básicas
5. **Criar** consultas complexas para o MeetStranger

---

## 📚 Conteúdos Programáticos

### 1. Comando SELECT Básico (45 min)
- Sintaxe fundamental
- Selecionar todas as colunas (*)
- Selecionar colunas específicas
- DISTINCT

### 2. Cláusula WHERE (60 min)
- Filtros com operadores relacionais
- Operadores lógicos (AND, OR, NOT)
- LIKE, IN, BETWEEN
- IS NULL / IS NOT NULL

### 3. ORDER BY e LIMIT (45 min)
- Ordenação ASC/DESC
- Ordenar por múltiplas colunas
- LIMIT e OFFSET
- Paginação

### 4. Funções de Agregação (60 min)
- COUNT, SUM, AVG, MIN, MAX
- GROUP BY
- HAVING

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: SELECT Básico (45 min)

**Atividade 1:** Sintaxe Fundamental (15 min)
```sql
-- Selecionar tudo
SELECT * FROM usuarios;

-- Colunas específicas
SELECT username, email FROM usuarios;

-- Com alias
SELECT 
    username AS nome_usuario,
    email AS email_contato
FROM usuarios;

-- DISTINCT (valores únicos)
SELECT DISTINCT categoria_id FROM salas;
```

**Atividade 2:** Exercícios (20 min)
```sql
-- 1. Listar todos os usuários
SELECT * FROM usuarios;

-- 2. Listar apenas usernames e emails
SELECT username, email FROM usuarios;

-- 3. Listar categorias únicas das salas
SELECT DISTINCT categoria_id FROM salas;

-- 4. Contar total de usuários
SELECT COUNT(*) AS total FROM usuarios;
```

**Atividade 3:** Prática (10 min)

### Momento 2: WHERE - Filtros (60 min + 10 min intervalo)

**Atividade 1:** Operadores Relacionais (20 min)
```sql
-- Igual
SELECT * FROM usuarios WHERE online = TRUE;

-- Diferente
SELECT * FROM usuarios WHERE online != TRUE;

-- Maior/Menor
SELECT * FROM estatisticas_usuario WHERE total_conversas > 5;

-- Maior ou igual
SELECT * FROM salas WHERE criada_em >= DATE('now', '-7 days');
```

**Atividade 2:** Operadores Lógicos (20 min)
```sql
-- AND
SELECT * FROM usuarios 
WHERE online = TRUE AND ultimo_login > DATE('now', '-1 hour');

-- OR
SELECT * FROM salas 
WHERE categoria_id = 1 OR categoria_id = 2;

-- NOT
SELECT * FROM usuarios WHERE NOT online;

-- Combinação
SELECT * FROM usuarios 
WHERE (online = TRUE OR ultimo_login > DATE('now', '-1 day'))
  AND username LIKE 'a%';
```

**Atividade 3:** LIKE, IN, BETWEEN (20 min)
```sql
-- LIKE (padrões)
SELECT * FROM usuarios WHERE username LIKE 'a%';  -- Começa com 'a'
SELECT * FROM usuarios WHERE email LIKE '%@gmail.com';  -- Gmail
SELECT * FROM usuarios WHERE username LIKE '%123%';  -- Contém '123'

-- IN (lista de valores)
SELECT * FROM salas WHERE categoria_id IN (1, 2);
SELECT * FROM usuarios WHERE id IN (1, 3, 5, 7);

-- BETWEEN (intervalo)
SELECT * FROM estatisticas_usuario 
WHERE total_conversas BETWEEN 5 AND 10;

-- IS NULL / IS NOT NULL
SELECT * FROM usuarios WHERE ultimo_login IS NULL;
SELECT * FROM salas WHERE encerrada_em IS NOT NULL;
```

### Momento 3: ORDER BY e LIMIT (45 min)

**Atividade 1:** Ordenação (20 min)
```sql
-- ASC (crescente - padrão)
SELECT * FROM usuarios ORDER BY username ASC;

-- DESC (decrescente)
SELECT * FROM usuarios ORDER BY criado_em DESC;

-- Múltiplas colunas
SELECT * FROM salas 
ORDER BY categoria_id ASC, criada_em DESC;

-- Com WHERE
SELECT * FROM usuarios 
WHERE online = TRUE 
ORDER BY ultimo_login DESC;
```

**Atividade 2:** LIMIT e OFFSET (15 min)
```sql
-- Primeiros 5 registros
SELECT * FROM usuarios LIMIT 5;

-- Top 10 mais ativos
SELECT * FROM estatisticas_usuario 
ORDER BY total_conversas DESC 
LIMIT 10;

-- Paginação (página 2, 10 por página)
SELECT * FROM usuarios 
ORDER BY username 
LIMIT 10 OFFSET 10;

-- Registros 11-20
SELECT * FROM usuarios 
ORDER BY criado_em DESC 
LIMIT 10 OFFSET 10;
```

**Atividade 3:** Exercícios (10 min)

### Momento 4: Funções de Agregação (60 min)

**Atividade 1:** COUNT, SUM, AVG, MIN, MAX (25 min)
```sql
-- COUNT (contar)
SELECT COUNT(*) AS total_usuarios FROM usuarios;
SELECT COUNT(*) AS usuarios_online FROM usuarios WHERE online = TRUE;

-- SUM (somar)
SELECT SUM(total_conversas) AS conversas_totais FROM estatisticas_usuario;

-- AVG (média)
SELECT AVG(tempo_total_minutos) AS tempo_medio FROM estatisticas_usuario;

-- MIN e MAX
SELECT MIN(criado_em) AS primeiro_usuario FROM usuarios;
SELECT MAX(total_conversas) AS max_conversas FROM estatisticas_usuario;

-- Múltiplas funções
SELECT 
    COUNT(*) AS total,
    AVG(total_conversas) AS media_conversas,
    MAX(total_conversas) AS max_conversas,
    MIN(total_conversas) AS min_conversas
FROM estatisticas_usuario;
```

**Atividade 2:** GROUP BY (20 min)
```sql
-- Agrupar por categoria
SELECT 
    categoria_id,
    COUNT(*) AS total_salas
FROM salas
GROUP BY categoria_id;

-- Com JOIN (próxima aula)
SELECT 
    c.nome AS categoria,
    COUNT(s.id) AS total_salas
FROM categorias c
LEFT JOIN salas s ON c.id = s.categoria_id
GROUP BY c.id, c.nome;

-- Estatísticas por status
SELECT 
    online,
    COUNT(*) AS total
FROM usuarios
GROUP BY online;
```

**Atividade 3:** HAVING (15 min)
```sql
-- HAVING (filtro após GROUP BY)
SELECT 
    categoria_id,
    COUNT(*) AS total
FROM salas
GROUP BY categoria_id
HAVING COUNT(*) > 5;

-- Usuários com mais de 10 conversas
SELECT 
    usuario_id,
    total_conversas
FROM estatisticas_usuario
WHERE total_conversas > 10
ORDER BY total_conversas DESC;
```

### Momento 5: Consultas do MeetStranger (60 min)

**Atividade 1:** Relatórios Básicos (20 min)
```sql
-- 1. Usuários online agora
SELECT username, ultimo_login
FROM usuarios
WHERE online = TRUE
ORDER BY ultimo_login DESC;

-- 2. Top 10 usuários mais ativos
SELECT 
    u.username,
    e.total_conversas,
    e.tempo_total_minutos
FROM usuarios u
JOIN estatisticas_usuario e ON u.id = e.usuario_id
ORDER BY e.total_conversas DESC
LIMIT 10;

-- 3. Salas ativas por categoria
SELECT 
    c.nome AS categoria,
    COUNT(s.id) AS salas_ativas
FROM categorias c
LEFT JOIN salas s ON c.id = s.categoria_id AND s.ativa = TRUE
GROUP BY c.id, c.nome;

-- 4. Usuários na fila
SELECT 
    u.username,
    c.nome AS categoria,
    f.entrou_em
FROM fila_matching f
JOIN usuarios u ON f.usuario_id = u.id
JOIN categorias c ON f.categoria_id = c.id
ORDER BY f.entrou_em;
```

**Atividade 2:** Consultas Complexas (25 min)
```sql
-- 1. Usuários sem conversas
SELECT u.username, u.criado_em
FROM usuarios u
LEFT JOIN estatisticas_usuario e ON u.id = e.usuario_id
WHERE e.total_conversas = 0 OR e.total_conversas IS NULL
ORDER BY u.criado_em DESC;

-- 2. Categoria mais popular
SELECT 
    c.nome,
    COUNT(s.id) AS total_salas
FROM categorias c
LEFT JOIN salas s ON c.id = s.categoria_id
GROUP BY c.id, c.nome
ORDER BY total_salas DESC
LIMIT 1;

-- 3. Tempo médio por categoria
SELECT 
    c.nome AS categoria,
    AVG(JULIANDAY(s.encerrada_em) - JULIANDAY(s.criada_em)) * 24 * 60 AS tempo_medio_minutos
FROM salas s
JOIN categorias c ON s.categoria_id = c.id
WHERE s.encerrada_em IS NOT NULL
GROUP BY c.id, c.nome;

-- 4. Usuários inativos (30+ dias)
SELECT 
    username,
    ultimo_login,
    JULIANDAY('now') - JULIANDAY(ultimo_login) AS dias_inativo
FROM usuarios
WHERE ultimo_login < DATE('now', '-30 days')
ORDER BY ultimo_login;
```

**Atividade 3:** Dashboard (15 min)
```sql
-- Dashboard completo do MeetStranger
SELECT 'Total de Usuários' AS metrica, COUNT(*) AS valor FROM usuarios
UNION ALL
SELECT 'Usuários Online', COUNT(*) FROM usuarios WHERE online = TRUE
UNION ALL
SELECT 'Salas Ativas', COUNT(*) FROM salas WHERE ativa = TRUE
UNION ALL
SELECT 'Usuários na Fila', COUNT(*) FROM fila_matching
UNION ALL
SELECT 'Total de Conversas', SUM(total_conversas) FROM estatisticas_usuario
UNION ALL
SELECT 'Tempo Total (horas)', ROUND(SUM(tempo_total_minutos) / 60.0, 2) FROM estatisticas_usuario;
```

### Momento 6: Exercícios Práticos (45 min)

**Exercício 1:** Consultas Básicas (15 min)
```
1. Listar usuários cadastrados hoje
2. Contar salas criadas esta semana
3. Listar top 5 categorias mais usadas
4. Encontrar usuários com email Gmail
5. Listar salas encerradas nas últimas 24h
```

**Exercício 2:** Consultas com Filtros (15 min)
```
1. Usuários online há mais de 1 hora
2. Salas da categoria "Filmes" criadas hoje
3. Usuários com 5-10 conversas
4. Fila de matching ordenada por tempo de espera
5. Estatísticas de usuários ativos (conversas > 0)
```

**Exercício 3:** Relatórios (15 min)
```
1. Relatório de uso por categoria
2. Ranking de usuários mais ativos
3. Análise de horários de pico
4. Taxa de conversão (cadastro → primeira conversa)
5. Tempo médio de espera na fila
```

### Momento 7: Fechamento (30 min)

**Atividade 1:** Síntese (15 min)
```
Comandos aprendidos:
✅ SELECT - recuperar dados
✅ WHERE - filtrar
✅ ORDER BY - ordenar
✅ LIMIT - limitar resultados
✅ Funções agregação - COUNT, SUM, AVG, MIN, MAX
✅ GROUP BY - agrupar
✅ HAVING - filtrar grupos

Próxima aula:
→ SELECT avançado com JOIN
→ Subconsultas
→ Encerramento do módulo
```

**Atividade 2:** Exercício para Casa (10 min)

**Atividade 3:** Preparação (5 min)

---

## 📝 Exercício para Casa

**Parte 1: Consultas Essenciais**

Criar consultas SQL para:

1. **Análise de Usuários**
```sql
-- a) Usuários cadastrados por mês
-- b) Taxa de retenção (login nos últimos 7 dias)
-- c) Distribuição por domínio de email
-- d) Usuários mais antigos ainda ativos
```

2. **Análise de Salas**
```sql
-- a) Salas por categoria e status
-- b) Duração média das conversas
-- c) Horário de pico (mais salas criadas)
-- d) Taxa de conclusão (salas encerradas vs criadas)
```

3. **Análise de Fila**
```sql
-- a) Tempo médio de espera por categoria
-- b) Usuários que mais entraram na fila
-- c) Categoria com maior fila
-- d) Taxa de match (salas criadas / entradas na fila)
```

**Parte 2: Dashboard Gerencial**

Criar consulta única que retorne:
- Total de usuários (total, ativos, inativos)
- Salas (ativas, encerradas hoje, total)
- Conversas (total, média por usuário)
- Categoria mais popular
- Tempo médio de conversa

**Parte 3: Otimização**

Para cada consulta da Parte 1:
- Explicar o que ela faz
- Identificar possíveis melhorias
- Sugerir índices necessários

**Formato:** Arquivo .sql com consultas + documento .txt com análises

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Formativa

**Critérios:**
- ✅ Usa SELECT corretamente
- ✅ Aplica WHERE com operadores adequados
- ✅ Ordena resultados apropriadamente
- ✅ Usa funções de agregação
- ✅ Agrupa dados com GROUP BY
- ✅ Cria consultas complexas

**Peso da Aula:** 20% da nota da Parte 2

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Recupera dados com SELECT  
✅ Filtra com WHERE eficientemente  
✅ Ordena resultados adequadamente  
✅ Usa LIMIT para paginação  
✅ Aplica funções de agregação  
✅ Agrupa dados corretamente  
✅ Cria consultas para relatórios  

---

## 📚 Recursos Didáticos

### Tabela de Referência Rápida

```sql
-- SELECT básico
SELECT coluna1, coluna2 FROM tabela;

-- WHERE
SELECT * FROM tabela WHERE condição;

-- ORDER BY
SELECT * FROM tabela ORDER BY coluna ASC/DESC;

-- LIMIT
SELECT * FROM tabela LIMIT 10 OFFSET 5;

-- Agregação
SELECT COUNT(*), AVG(coluna) FROM tabela;

-- GROUP BY
SELECT coluna, COUNT(*) FROM tabela GROUP BY coluna;

-- HAVING
SELECT coluna, COUNT(*) FROM tabela 
GROUP BY coluna HAVING COUNT(*) > 5;
```

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 45 min
- ⏰ Momento 2: 70 min (com intervalo)
- ⏰ Momento 3: 45 min
- ⏰ Momento 4: 60 min
- ⏰ Momento 5: 60 min
- ⏰ Momento 6: 45 min
- ⏰ Momento 7: 30 min

### Pontos de Atenção
1. **SELECT ***: Explicar quando usar e quando evitar
2. **WHERE**: Enfatizar importância de filtros
3. **ORDER BY**: Performance em grandes volumes
4. **GROUP BY**: Conceito pode ser difícil
5. **Funções**: Mostrar aplicações práticas

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
