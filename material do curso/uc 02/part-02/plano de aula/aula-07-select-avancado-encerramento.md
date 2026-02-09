# Aula 07 - SELECT no Projeto MeetStranger e Encerramento do Módulo

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas  
**Data:** 25/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Consolidar** conhecimentos de SQL no MeetStranger
2. **Criar** consultas complexas com JOIN
3. **Gerar** relatórios completos do sistema
4. **Integrar** conceitos de banco de dados com backend
5. **Avaliar** aprendizado do módulo

---

## 📚 Conteúdos Programáticos

### 1. JOIN - Relacionamentos (60 min)
- INNER JOIN
- LEFT JOIN
- Consultas com múltiplas tabelas

### 2. Subconsultas (45 min)
- Subconsultas no WHERE
- Subconsultas no SELECT
- EXISTS e NOT EXISTS

### 3. Consultas Avançadas MeetStranger (60 min)
- Relatórios gerenciais
- Análises de uso
- Métricas de negócio

### 4. Avaliação e Encerramento (75 min)
- Avaliação prática
- Feedback coletivo
- Integração com próximas partes

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: JOIN - Relacionamentos (60 min)

**Atividade 1:** INNER JOIN (20 min)
```sql
-- Salas com informações completas
SELECT 
    s.id AS sala_id,
    c.nome AS categoria,
    u1.username AS usuario1,
    u2.username AS usuario2,
    s.criada_em,
    s.ativa
FROM salas s
INNER JOIN categorias c ON s.categoria_id = c.id
INNER JOIN usuarios u1 ON s.usuario1_id = u1.id
INNER JOIN usuarios u2 ON s.usuario2_id = u2.id
WHERE s.ativa = TRUE;

-- Fila com detalhes
SELECT 
    f.id,
    u.username,
    c.nome AS categoria,
    f.entrou_em,
    ROUND((JULIANDAY('now') - JULIANDAY(f.entrou_em)) * 24 * 60) AS minutos_esperando
FROM fila_matching f
INNER JOIN usuarios u ON f.usuario_id = u.id
INNER JOIN categorias c ON f.categoria_id = c.id
ORDER BY f.entrou_em;
```

**Atividade 2:** LEFT JOIN (20 min)
```sql
-- Todas as categorias com contagem de salas
SELECT 
    c.nome AS categoria,
    COUNT(s.id) AS total_salas
FROM categorias c
LEFT JOIN salas s ON c.id = s.categoria_id
GROUP BY c.id, c.nome;

-- Usuários com estatísticas (incluindo sem conversas)
SELECT 
    u.username,
    COALESCE(e.total_conversas, 0) AS conversas,
    COALESCE(e.tempo_total_minutos, 0) AS tempo_minutos
FROM usuarios u
LEFT JOIN estatisticas_usuario e ON u.id = e.usuario_id
ORDER BY conversas DESC;
```

**Atividade 3:** Múltiplos JOINs (20 min)
```sql
-- Relatório completo de usuário
SELECT 
    u.id,
    u.username,
    u.email,
    u.online,
    u.ultimo_login,
    e.total_conversas,
    e.tempo_total_minutos,
    c.nome AS categoria_favorita,
    CASE 
        WHEN EXISTS (SELECT 1 FROM salas WHERE (usuario1_id = u.id OR usuario2_id = u.id) AND ativa = TRUE)
        THEN 'Em conversa'
        WHEN EXISTS (SELECT 1 FROM fila_matching WHERE usuario_id = u.id)
        THEN 'Na fila'
        WHEN u.online THEN 'Online'
        ELSE 'Offline'
    END AS status_atual
FROM usuarios u
LEFT JOIN estatisticas_usuario e ON u.id = e.usuario_id
LEFT JOIN categorias c ON e.categoria_favorita_id = c.id
ORDER BY u.username;
```

### Momento 2: Subconsultas (45 min + 10 min intervalo)

**Atividade 1:** Subconsultas no WHERE (15 min)
```sql
-- Usuários com mais conversas que a média
SELECT username, total_conversas
FROM usuarios u
JOIN estatisticas_usuario e ON u.id = e.usuario_id
WHERE e.total_conversas > (
    SELECT AVG(total_conversas) FROM estatisticas_usuario
)
ORDER BY e.total_conversas DESC;

-- Categorias sem salas ativas
SELECT nome
FROM categorias
WHERE id NOT IN (
    SELECT DISTINCT categoria_id FROM salas WHERE ativa = TRUE
);
```

**Atividade 2:** EXISTS e NOT EXISTS (15 min)
```sql
-- Usuários que já conversaram
SELECT username
FROM usuarios u
WHERE EXISTS (
    SELECT 1 FROM estatisticas_usuario e 
    WHERE e.usuario_id = u.id AND e.total_conversas > 0
);

-- Usuários que nunca conversaram
SELECT username, criado_em
FROM usuarios u
WHERE NOT EXISTS (
    SELECT 1 FROM estatisticas_usuario e 
    WHERE e.usuario_id = u.id AND e.total_conversas > 0
)
ORDER BY criado_em DESC;
```

**Atividade 3:** Subconsultas no SELECT (15 min)
```sql
-- Usuários com contadores inline
SELECT 
    u.username,
    (SELECT COUNT(*) FROM salas 
     WHERE usuario1_id = u.id OR usuario2_id = u.id) AS total_salas,
    (SELECT COUNT(*) FROM salas 
     WHERE (usuario1_id = u.id OR usuario2_id = u.id) AND ativa = TRUE) AS salas_ativas,
    (SELECT total_conversas FROM estatisticas_usuario WHERE usuario_id = u.id) AS conversas
FROM usuarios u
ORDER BY conversas DESC NULLS LAST;
```

### Momento 3: Relatórios MeetStranger (60 min)

**Atividade 1:** Dashboard Executivo (20 min)
```sql
-- Dashboard completo
WITH stats AS (
    SELECT 
        COUNT(*) AS total_usuarios,
        SUM(CASE WHEN online THEN 1 ELSE 0 END) AS usuarios_online,
        SUM(CASE WHEN ultimo_login > DATETIME('now', '-7 days') THEN 1 ELSE 0 END) AS usuarios_ativos_semana
    FROM usuarios
),
salas_stats AS (
    SELECT 
        COUNT(*) AS total_salas,
        SUM(CASE WHEN ativa THEN 1 ELSE 0 END) AS salas_ativas,
        SUM(CASE WHEN DATE(criada_em) = DATE('now') THEN 1 ELSE 0 END) AS salas_hoje
    FROM salas
),
conversas_stats AS (
    SELECT 
        SUM(total_conversas) AS total_conversas,
        ROUND(AVG(total_conversas), 2) AS media_conversas,
        ROUND(SUM(tempo_total_minutos) / 60.0, 2) AS total_horas
    FROM estatisticas_usuario
)
SELECT 
    'Usuários' AS categoria,
    s.total_usuarios AS total,
    s.usuarios_online AS online,
    s.usuarios_ativos_semana AS ativos_semana
FROM stats s
UNION ALL
SELECT 
    'Salas',
    ss.total_salas,
    ss.salas_ativas,
    ss.salas_hoje
FROM salas_stats ss
UNION ALL
SELECT 
    'Conversas',
    cs.total_conversas,
    cs.media_conversas,
    cs.total_horas
FROM conversas_stats cs;
```

**Atividade 2:** Análise por Categoria (20 min)
```sql
-- Performance por categoria
SELECT 
    c.nome AS categoria,
    COUNT(DISTINCT s.id) AS total_salas,
    COUNT(DISTINCT CASE WHEN s.ativa THEN s.id END) AS salas_ativas,
    COUNT(DISTINCT s.usuario1_id) + COUNT(DISTINCT s.usuario2_id) AS usuarios_unicos,
    ROUND(AVG(JULIANDAY(COALESCE(s.encerrada_em, 'now')) - JULIANDAY(s.criada_em)) * 24 * 60, 2) AS duracao_media_min,
    (SELECT COUNT(*) FROM fila_matching WHERE categoria_id = c.id) AS usuarios_na_fila
FROM categorias c
LEFT JOIN salas s ON c.id = s.categoria_id
GROUP BY c.id, c.nome
ORDER BY total_salas DESC;
```

**Atividade 3:** Ranking de Usuários (20 min)
```sql
-- Top 20 usuários mais ativos
SELECT 
    ROW_NUMBER() OVER (ORDER BY e.total_conversas DESC) AS ranking,
    u.username,
    e.total_conversas,
    ROUND(e.tempo_total_minutos / 60.0, 2) AS horas_total,
    c.nome AS categoria_favorita,
    u.criado_em,
    ROUND(JULIANDAY('now') - JULIANDAY(u.criado_em)) AS dias_cadastrado
FROM usuarios u
JOIN estatisticas_usuario e ON u.id = e.usuario_id
LEFT JOIN categorias c ON e.categoria_favorita_id = c.id
WHERE e.total_conversas > 0
ORDER BY e.total_conversas DESC
LIMIT 20;
```

### Momento 4: Avaliação Prática (75 min)

**Atividade 1:** Avaliação Individual (45 min)

**Desafio: Criar Sistema de Relatórios**

```sql
-- PARTE 1: Consultas Obrigatórias (30 pontos)

-- 1. Listar usuários online com tempo desde último login (5 pontos)
-- 2. Salas ativas com duração atual (5 pontos)
-- 3. Fila de matching ordenada por tempo de espera (5 pontos)
-- 4. Top 5 categorias mais populares (5 pontos)
-- 5. Usuários inativos há mais de 30 dias (5 pontos)
-- 6. Estatísticas gerais do sistema (5 pontos)

-- PARTE 2: Consultas Avançadas (40 pontos)

-- 7. Análise de retenção (usuários que voltaram após primeira conversa) (10 pontos)
-- 8. Taxa de conversão (cadastro → primeira conversa) (10 pontos)
-- 9. Horário de pico (hora com mais salas criadas) (10 pontos)
-- 10. Relatório completo de usuário específico (10 pontos)

-- PARTE 3: Otimização (30 pontos)

-- 11. Identificar consultas lentas e propor melhorias (15 pontos)
-- 12. Sugerir índices necessários (15 pontos)
```

**Atividade 2:** Correção e Feedback (20 min)
- Apresentação de soluções
- Discussão de alternativas
- Identificação de boas práticas

**Atividade 3:** Autoavaliação (10 min)
```
Checklist de Competências:
□ Crio tabelas com estrutura adequada
□ Insiro dados com validações
□ Atualizo registros com segurança
□ Deleto dados de forma controlada
□ Recupero dados com SELECT
□ Filtro com WHERE eficientemente
□ Ordeno e limito resultados
□ Uso funções de agregação
□ Faço JOIN entre tabelas
□ Crio subconsultas
□ Gero relatórios complexos
□ Aplico regras de negócio
□ Mantenho integridade dos dados
```

### Momento 5: Integração e Próximos Passos (45 min)

**Atividade 1:** Conexão com Backend (20 min)
```javascript
// Exemplo: Como o backend usará o banco

// Node.js + SQLite
const sqlite3 = require('sqlite3');
const db = new sqlite3.Database('./meetstranger.db');

// Cadastrar usuário
app.post('/api/auth/register', async (req, res) => {
    const { username, email, senha } = req.body;
    
    // Validar duplicatas
    db.get(
        'SELECT id FROM usuarios WHERE username = ? OR email = ?',
        [username, email],
        (err, row) => {
            if (row) {
                return res.status(400).json({ error: 'Usuário já existe' });
            }
            
            // Inserir usuário
            db.run(
                'INSERT INTO usuarios (username, email, senha) VALUES (?, ?, ?)',
                [username, email, hashSenha],
                function(err) {
                    if (err) return res.status(500).json({ error: err.message });
                    
                    // Criar estatísticas
                    db.run(
                        'INSERT INTO estatisticas_usuario (usuario_id) VALUES (?)',
                        [this.lastID]
                    );
                    
                    res.json({ id: this.lastID, username });
                }
            );
        }
    );
});

// Listar usuários online
app.get('/api/users/online', (req, res) => {
    db.all(
        'SELECT username, ultimo_login FROM usuarios WHERE online = TRUE',
        [],
        (err, rows) => {
            if (err) return res.status(500).json({ error: err.message });
            res.json(rows);
        }
    );
});
```

**Atividade 2:** Visão Geral da UC 02 (15 min)
```
Módulos da UC 02:
✅ Parte 1: Lógica de Programação (36h)
✅ Parte 2: Banco de Dados (30h) ← CONCLUÍDO
→ Parte 3: Backend (30h)
→ Parte 4: Frontend Mobile (30h)

Próximos passos:
- Node.js e Express
- API REST
- WebSocket
- Integração com banco
- Integração com frontend
```

**Atividade 3:** Feedback e Encerramento (10 min)
- Feedback da turma sobre o módulo
- Dúvidas finais
- Orientações para próxima parte

### Momento 6: Celebração e Encerramento (30 min)

**Atividade 1:** Retrospectiva (15 min)
```
O que aprendemos:
✅ Modelagem de dados
✅ CREATE DATABASE e TABLE
✅ INSERT, UPDATE, DELETE
✅ SELECT com filtros e ordenação
✅ JOIN e relacionamentos
✅ Funções de agregação
✅ Regras de negócio
✅ Integridade de dados

Conquistas:
✅ Banco MeetStranger completo
✅ Dados populados
✅ Consultas funcionais
✅ Relatórios gerenciais
```

**Atividade 2:** Certificação de Conclusão (10 min)
- Entrega simbólica de certificado
- Reconhecimento de destaques
- Fotos da turma

**Atividade 3:** Próxima Etapa (5 min)
- Data de início da Parte 3
- Materiais necessários
- Preparação prévia

---

## 📝 Avaliação Final do Módulo

### Composição da Nota

| Componente | Peso |
|------------|------|
| Aula 01 | 10% |
| Aula 02 | 15% |
| Aula 03 | 20% |
| Aula 05 | 20% |
| Aula 06 | 20% |
| Aula 07 | 15% |
| **Total** | **100%** |

### Critérios de Aprovação
- Nota mínima: 7.0
- Frequência mínima: 75%
- Banco MeetStranger funcional

---

## 🎯 Competências Desenvolvidas

### Conhecimentos
✅ Modelagem de dados  
✅ SQL (DDL, DML, DQL)  
✅ Integridade referencial  
✅ Normalização básica  
✅ Índices e performance  

### Habilidades
✅ Criar estruturas de banco  
✅ Manipular dados com segurança  
✅ Consultar dados eficientemente  
✅ Aplicar regras de negócio  
✅ Gerar relatórios  

### Atitudes
✅ Atenção à integridade  
✅ Cuidado com dados sensíveis  
✅ Organização  
✅ Documentação  
✅ Trabalho em equipe  

---

## 📚 Recursos Didáticos

### Materiais Finais
- [ ] Banco MeetStranger completo
- [ ] Avaliação prática
- [ ] Certificado de conclusão
- [ ] Guia de integração com backend

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 60 min
- ⏰ Momento 2: 55 min (com intervalo)
- ⏰ Momento 3: 60 min
- ⏰ Momento 4: 75 min
- ⏰ Momento 5: 45 min
- ⏰ Momento 6: 30 min

### Pontos de Atenção
1. **Avaliação**: Ser justo e construtivo
2. **Feedback**: Individual e coletivo
3. **Integração**: Mostrar conexão com backend
4. **Celebração**: Reconhecer esforço da turma
5. **Motivação**: Preparar para próxima etapa

---

## 📝 Observações Finais

```
Data: ___/___/______

Avaliação do módulo:
- Aprovados: ___ alunos
- Nota média: ___
- Destaques: ___

Feedback da turma:
- Pontos positivos:
- Pontos a melhorar:

Preparação para Parte 3:
- Materiais necessários:
- Pré-requisitos:
- Data de início:
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação

---

## 🎉 Parabéns pela Conclusão do Módulo de Banco de Dados!

**Próxima etapa:** Parte 3 - Backend (Node.js + Express + API REST)
