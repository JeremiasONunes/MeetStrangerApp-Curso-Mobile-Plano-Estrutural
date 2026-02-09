# Aula 02 - Modelagem e CREATE Aplicado ao Projeto MeetStranger

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas  
**Data:** 19/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Aplicar** conceitos de modelagem de dados a um projeto real
2. **Identificar** entidades e atributos do MeetStranger
3. **Criar** estrutura completa do banco de dados do projeto
4. **Implementar** chaves primárias e estrangeiras

---

## 📚 Conteúdos Programáticos

### 1. Levantamento de Requisitos de Dados (45 min)
- Análise dos requisitos do MeetStranger
- Identificação de dados necessários
- Mapeamento de funcionalidades x dados

### 2. Identificação de Entidades e Atributos (45 min)
- Conceito de entidade
- Definição de atributos
- Tipos de dados apropriados
- Restrições necessárias

### 3. Modelagem Lógica Simplificada (45 min)
- Diagrama Entidade-Relacionamento básico
- Relacionamentos entre entidades
- Cardinalidade

### 4. CREATE TABLE Aplicado ao Projeto (60 min)
- Criação do banco MeetStranger
- Implementação das tabelas
- Chaves primárias e estrangeiras

### 5. Validação e Refinamento (45 min)
- Revisão coletiva da estrutura
- Ajustes necessários
- Testes básicos

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Retomada e Contextualização (30 min)

**Atividade:** Revisão + Apresentação do Projeto

**Revisão Rápida (10 min):**
- CREATE DATABASE
- CREATE TABLE
- Tipos de dados
- PRIMARY KEY

**Contexto do MeetStranger (20 min):**
```
Funcionalidades principais:
1. Cadastro de usuários
2. Login/Autenticação
3. Seleção de categoria (Filmes, Jogos, Séries)
4. Matching P2P
5. Chat em tempo real
6. Trocar de parceiro
7. Sair do chat

Quais dados precisamos armazenar?
```

### Momento 2: Levantamento de Requisitos (45 min)

**Atividade 1:** Análise de Funcionalidades (20 min)

**Cadastro de Usuários - Dados necessários:**
```
- Username (identificação)
- Email (login)
- Senha (autenticação)
- Data de cadastro (auditoria)
- Status online (disponibilidade)
- Última conexão (controle)
```

**Matching e Chat - Dados necessários:**
```
- Categoria escolhida
- Sala de chat atual
- Histórico de conversas (opcional)
- Estatísticas de uso
```

**Atividade 2:** Discussão em Grupos (15 min)
- Dividir turma em 3 grupos
- Cada grupo analisa uma funcionalidade
- Listar dados necessários

**Atividade 3:** Consolidação (10 min)
- Apresentação dos grupos
- Consolidar lista de dados
- Priorizar dados essenciais

### Momento 3: Identificação de Entidades (45 min)

**Atividade 1:** Conceito de Entidade (15 min)
```
Entidade: "Coisa" sobre a qual queremos armazenar dados

Exemplos:
- Usuário (pessoa que usa o app)
- Sala (local de conversa)
- Mensagem (conteúdo trocado)
- Categoria (tópico de conversa)

Como identificar:
- Substantivos nos requisitos
- Dados que se repetem
- Objetos do mundo real
```

**Atividade 2:** Entidades do MeetStranger (20 min)

**Entidade: USUÁRIO**
```
Atributos:
- id (identificador único)
- username (nome de usuário)
- email (email único)
- senha (hash da senha)
- criado_em (data de cadastro)
- ultimo_login (última conexão)
- online (status atual)

Tipos de dados:
- id: INTEGER PRIMARY KEY
- username: TEXT NOT NULL UNIQUE
- email: TEXT NOT NULL UNIQUE
- senha: TEXT NOT NULL
- criado_em: DATETIME DEFAULT CURRENT_TIMESTAMP
- ultimo_login: DATETIME
- online: BOOLEAN DEFAULT FALSE
```

**Entidade: SALA**
```
Atributos:
- id (identificador único)
- categoria (Filmes, Jogos, Séries)
- usuario1_id (primeiro usuário)
- usuario2_id (segundo usuário)
- criada_em (quando foi criada)
- ativa (se está em uso)

Tipos de dados:
- id: INTEGER PRIMARY KEY
- categoria: TEXT NOT NULL
- usuario1_id: INTEGER NOT NULL
- usuario2_id: INTEGER NOT NULL
- criada_em: DATETIME DEFAULT CURRENT_TIMESTAMP
- ativa: BOOLEAN DEFAULT TRUE
```

**Atividade 3:** Exercício em Duplas (10 min)
```
Definir atributos para entidade CATEGORIA:
- Quais dados são necessários?
- Quais tipos de dados?
- Quais restrições?
```

### Momento 4: Modelagem Lógica (45 min + 10 min intervalo)

**Atividade 1:** Diagrama ER Simplificado (20 min)
```
Representação visual:

┌─────────────┐
│   USUÁRIO   │
├─────────────┤
│ id (PK)     │
│ username    │
│ email       │
│ senha       │
│ criado_em   │
│ online      │
└─────────────┘
       │
       │ participa
       │
       ▼
┌─────────────┐
│    SALA     │
├─────────────┤
│ id (PK)     │
│ categoria   │
│ usuario1_id │ (FK → USUÁRIO)
│ usuario2_id │ (FK → USUÁRIO)
│ criada_em   │
│ ativa       │
└─────────────┘

PK = Primary Key (Chave Primária)
FK = Foreign Key (Chave Estrangeira)
```

**Atividade 2:** Relacionamentos (15 min)
```
USUÁRIO ←→ SALA
- Um usuário pode estar em 0 ou 1 sala
- Uma sala tem exatamente 2 usuários

Cardinalidade: N:M (muitos para muitos)
Implementação: Através de chaves estrangeiras
```

**Atividade 3:** Chave Estrangeira (10 min)
```
Chave Estrangeira (FOREIGN KEY):
- Referencia chave primária de outra tabela
- Garante integridade referencial
- Não pode referenciar registro inexistente

Exemplo:
sala.usuario1_id → usuario.id
sala.usuario2_id → usuario.id
```

### Momento 5: CREATE TABLE do MeetStranger (60 min)

**Atividade 1:** Criar Banco de Dados (10 min)
```sql
-- Criar banco do projeto
CREATE DATABASE meetstranger;

-- Usar o banco
USE meetstranger;

-- Verificar
SHOW DATABASES;
```

**Atividade 2:** Tabela USUÁRIO (20 min)
```sql
-- Tabela principal de usuários
CREATE TABLE usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    email TEXT NOT NULL UNIQUE,
    senha TEXT NOT NULL,
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    ultimo_login DATETIME,
    online BOOLEAN DEFAULT FALSE,
    
    -- Restrições adicionais
    CHECK (LENGTH(username) >= 3),
    CHECK (LENGTH(senha) >= 6)
);

-- Verificar estrutura
DESCRIBE usuarios;
```

**Atividade 3:** Tabela CATEGORIA (15 min)
```sql
-- Tabela de categorias de conversa
CREATE TABLE categorias (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL UNIQUE,
    descricao TEXT,
    ativa BOOLEAN DEFAULT TRUE
);

-- Inserir categorias padrão
INSERT INTO categorias (nome, descricao) VALUES
    ('Filmes', 'Converse sobre cinema e filmes'),
    ('Jogos', 'Discuta sobre games e jogos'),
    ('Séries', 'Fale sobre suas séries favoritas');
```

**Atividade 4:** Tabela SALA (15 min)
```sql
-- Tabela de salas de chat
CREATE TABLE salas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    categoria_id INTEGER NOT NULL,
    usuario1_id INTEGER NOT NULL,
    usuario2_id INTEGER NOT NULL,
    criada_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    encerrada_em DATETIME,
    ativa BOOLEAN DEFAULT TRUE,
    
    -- Chaves estrangeiras
    FOREIGN KEY (categoria_id) REFERENCES categorias(id),
    FOREIGN KEY (usuario1_id) REFERENCES usuarios(id),
    FOREIGN KEY (usuario2_id) REFERENCES usuarios(id),
    
    -- Garantir que usuários são diferentes
    CHECK (usuario1_id != usuario2_id)
);
```

### Momento 6: Tabelas Complementares (30 min)

**Atividade 1:** Tabela FILA_MATCHING (15 min)
```sql
-- Fila de espera para matching
CREATE TABLE fila_matching (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario_id INTEGER NOT NULL,
    categoria_id INTEGER NOT NULL,
    entrou_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id),
    FOREIGN KEY (categoria_id) REFERENCES categorias(id),
    
    -- Usuário só pode estar em uma fila por vez
    UNIQUE (usuario_id)
);
```

**Atividade 2:** Tabela ESTATISTICAS (opcional) (15 min)
```sql
-- Estatísticas de uso do usuário
CREATE TABLE estatisticas_usuario (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario_id INTEGER NOT NULL UNIQUE,
    total_conversas INTEGER DEFAULT 0,
    tempo_total_minutos INTEGER DEFAULT 0,
    categoria_favorita_id INTEGER,
    
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id),
    FOREIGN KEY (categoria_favorita_id) REFERENCES categorias(id)
);
```

### Momento 7: Validação Coletiva (45 min)

**Atividade 1:** Revisão da Estrutura (20 min)
- Apresentar todas as tabelas criadas
- Verificar relacionamentos
- Identificar possíveis problemas

**Checklist de Validação:**
```
✅ Todas as entidades identificadas?
✅ Atributos suficientes?
✅ Tipos de dados adequados?
✅ Chaves primárias definidas?
✅ Chaves estrangeiras corretas?
✅ Restrições necessárias?
✅ Nomes consistentes?
```

**Atividade 2:** Testes Básicos (15 min)
```sql
-- Verificar todas as tabelas
SHOW TABLES;

-- Ver estrutura de cada tabela
DESCRIBE usuarios;
DESCRIBE categorias;
DESCRIBE salas;
DESCRIBE fila_matching;

-- Verificar dados iniciais
SELECT * FROM categorias;
```

**Atividade 3:** Ajustes e Melhorias (10 min)
- Discussão sobre melhorias
- Ajustes necessários
- Documentar decisões

### Momento 8: Fechamento (30 min)

**Atividade 1:** Síntese (15 min)
- Recapitular processo de modelagem
- Importância de planejar antes de implementar
- Conexão com próxima aula (INSERT, UPDATE, DELETE)

**Atividade 2:** Documentação (10 min)
- Criar documento com estrutura do banco
- Explicar cada tabela
- Descrever relacionamentos

**Atividade 3:** Exercício para Casa (5 min)
- Entregar e explicar

---

## 📝 Atividades Práticas

### Exercício Completo: Banco MeetStranger

```sql
-- ============================================
-- BANCO DE DADOS: MEETSTRANGER
-- Versão: 1.0
-- Data: 19/03/2026
-- ============================================

-- 1. CRIAR BANCO DE DADOS
CREATE DATABASE meetstranger;
USE meetstranger;

-- 2. TABELA: USUÁRIOS
CREATE TABLE usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    email TEXT NOT NULL UNIQUE,
    senha TEXT NOT NULL,
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    ultimo_login DATETIME,
    online BOOLEAN DEFAULT FALSE,
    
    CHECK (LENGTH(username) >= 3 AND LENGTH(username) <= 20),
    CHECK (LENGTH(senha) >= 6),
    CHECK (email LIKE '%@%.%')
);

-- 3. TABELA: CATEGORIAS
CREATE TABLE categorias (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL UNIQUE,
    descricao TEXT,
    icone TEXT,
    ativa BOOLEAN DEFAULT TRUE
);

-- Inserir categorias padrão
INSERT INTO categorias (nome, descricao, icone) VALUES
    ('Filmes', 'Converse sobre cinema e filmes', '🎬'),
    ('Jogos', 'Discuta sobre games e jogos', '🎮'),
    ('Séries', 'Fale sobre suas séries favoritas', '📺');

-- 4. TABELA: SALAS
CREATE TABLE salas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    categoria_id INTEGER NOT NULL,
    usuario1_id INTEGER NOT NULL,
    usuario2_id INTEGER NOT NULL,
    criada_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    encerrada_em DATETIME,
    ativa BOOLEAN DEFAULT TRUE,
    
    FOREIGN KEY (categoria_id) REFERENCES categorias(id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE,
    FOREIGN KEY (usuario1_id) REFERENCES usuarios(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    FOREIGN KEY (usuario2_id) REFERENCES usuarios(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    
    CHECK (usuario1_id != usuario2_id)
);

-- 5. TABELA: FILA DE MATCHING
CREATE TABLE fila_matching (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario_id INTEGER NOT NULL,
    categoria_id INTEGER NOT NULL,
    entrou_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    posicao INTEGER,
    
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
        ON DELETE CASCADE,
    FOREIGN KEY (categoria_id) REFERENCES categorias(id)
        ON DELETE CASCADE,
    
    UNIQUE (usuario_id)
);

-- 6. TABELA: ESTATÍSTICAS
CREATE TABLE estatisticas_usuario (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario_id INTEGER NOT NULL UNIQUE,
    total_conversas INTEGER DEFAULT 0,
    tempo_total_minutos INTEGER DEFAULT 0,
    categoria_favorita_id INTEGER,
    ultima_atualizacao DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
        ON DELETE CASCADE,
    FOREIGN KEY (categoria_favorita_id) REFERENCES categorias(id)
        ON DELETE SET NULL,
    
    CHECK (total_conversas >= 0),
    CHECK (tempo_total_minutos >= 0)
);

-- 7. ÍNDICES PARA PERFORMANCE
CREATE INDEX idx_usuarios_email ON usuarios(email);
CREATE INDEX idx_usuarios_username ON usuarios(username);
CREATE INDEX idx_salas_ativa ON salas(ativa);
CREATE INDEX idx_fila_categoria ON fila_matching(categoria_id);

-- 8. VERIFICAR ESTRUTURA
SHOW TABLES;
```

### Diagrama ER Completo

```
┌─────────────────────┐
│     USUÁRIOS        │
├─────────────────────┤
│ id (PK)             │
│ username (UNIQUE)   │
│ email (UNIQUE)      │
│ senha               │
│ criado_em           │
│ ultimo_login        │
│ online              │
└─────────────────────┘
         │ 1
         │
         │ N
         ▼
┌─────────────────────┐         ┌─────────────────────┐
│   FILA_MATCHING     │    N    │    CATEGORIAS       │
├─────────────────────┤ ──────► ├─────────────────────┤
│ id (PK)             │    1    │ id (PK)             │
│ usuario_id (FK)     │         │ nome (UNIQUE)       │
│ categoria_id (FK)   │         │ descricao           │
│ entrou_em           │         │ icone               │
│ posicao             │         │ ativa               │
└─────────────────────┘         └─────────────────────┘
         │                               │ 1
         │                               │
         │ 1                             │ N
         ▼                               ▼
┌─────────────────────┐         ┌─────────────────────┐
│       SALAS         │         │  ESTATISTICAS_      │
├─────────────────────┤         │     USUARIO         │
│ id (PK)             │         ├─────────────────────┤
│ categoria_id (FK)   │         │ id (PK)             │
│ usuario1_id (FK)    │         │ usuario_id (FK)     │
│ usuario2_id (FK)    │         │ total_conversas     │
│ criada_em           │         │ tempo_total_minutos │
│ encerrada_em        │         │ categoria_fav_id    │
│ ativa               │         │ ultima_atualizacao  │
└─────────────────────┘         └─────────────────────┘
```

### Exercício para Casa

**Parte 1: Análise e Documentação**

Criar documento explicando:

1. **Cada Tabela:**
   - Propósito
   - Atributos e justificativas
   - Relacionamentos

2. **Decisões de Modelagem:**
   - Por que essas entidades?
   - Por que esses atributos?
   - Por que esses tipos de dados?

3. **Melhorias Futuras:**
   - O que poderia ser adicionado?
   - Que funcionalidades novas precisariam de novas tabelas?

**Parte 2: Extensão (Opcional)**

Criar tabela adicional:

**MENSAGENS** (para histórico opcional)
```sql
CREATE TABLE mensagens (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    sala_id INTEGER NOT NULL,
    usuario_id INTEGER NOT NULL,
    conteudo TEXT NOT NULL,
    enviada_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (sala_id) REFERENCES salas(id),
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id),
    
    CHECK (LENGTH(conteudo) > 0 AND LENGTH(conteudo) <= 500)
);
```

Justificar:
- Por que adicionar?
- Impacto na privacidade
- Quando seria útil?

**Formato de Entrega:**
- Arquivo .sql com comandos (se fez Parte 2)
- Documento .pdf ou .txt com análise

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Compreensão de CREATE TABLE
- Conhecimento sobre o projeto

### Avaliação Formativa

**Critérios:**
- ✅ Identifica entidades corretamente
- ✅ Define atributos adequados
- ✅ Escolhe tipos de dados apropriados
- ✅ Implementa chaves primárias
- ✅ Cria chaves estrangeiras
- ✅ Aplica restrições (CHECK, UNIQUE)
- ✅ Documenta decisões

**Instrumentos:**
- Participação nas discussões
- Exercícios em grupo
- Estrutura do banco criada
- Documentação

### Avaliação Somativa
- Participação e exercícios: 40%
- Exercício para casa: 60%

**Peso da Aula:** 15% da nota da Parte 2

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Analisa requisitos e identifica dados necessários  
✅ Define entidades e atributos corretamente  
✅ Cria diagrama ER básico  
✅ Implementa tabelas com estrutura adequada  
✅ Define chaves primárias e estrangeiras  
✅ Aplica restrições de integridade  
✅ Documenta decisões de modelagem  
✅ Valida estrutura criada  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Computadores com SQLite
- [ ] VS Code configurado
- [ ] Projetor/TV
- [ ] Quadro branco (para diagramas)
- [ ] Documentação do MeetStranger
- [ ] Folhas para modelagem

### Ferramentas de Modelagem
- **Draw.io**: Diagramas ER online
- **dbdiagram.io**: Modelagem de banco
- **SQLite Browser**: Visualizar estrutura

### Referências
- Documentação do projeto: `../../documentacao-projeto/`
- Requisitos funcionais e não funcionais
- Arquitetura do sistema

---

## 🔄 Conexão com Outras Aulas

### Revisão da Aula 01
- CREATE DATABASE
- CREATE TABLE
- Tipos de dados
- PRIMARY KEY

### Preparação para Aula 03
- INSERT (inserir dados)
- UPDATE (atualizar dados)
- DELETE (excluir dados)
- Manipulação de dados do MeetStranger

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 45 min
- ⏰ Momento 3: 45 min
- ⏰ Momento 4: 55 min (com intervalo)
- ⏰ Momento 5: 60 min
- ⏰ Momento 6: 30 min
- ⏰ Momento 7: 45 min
- ⏰ Momento 8: 30 min

### Pontos de Atenção
1. **Modelagem**: Processo mais importante que resultado
2. **Chave Estrangeira**: Conceito novo, explicar bem
3. **Relacionamentos**: Usar exemplos visuais
4. **Projeto Real**: Conectar sempre com MeetStranger
5. **Validação**: Envolver toda a turma

### Estratégias
- Desenhar diagramas no quadro
- Fazer modelagem colaborativa
- Discutir alternativas
- Mostrar impacto de decisões erradas
- Testar estrutura criada

### Adaptações
- **Turma iniciante**: Simplificar diagrama ER
- **Turma avançada**: Adicionar mais tabelas
- **EAD**: Usar ferramentas online de modelagem

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Revisar documentação do MeetStranger
- [ ] Preparar diagrama ER
- [ ] Testar todos os comandos SQL
- [ ] Preparar exemplos de modelagem
- [ ] Criar exercícios

### Durante a Aula
- [ ] Revisar aula anterior
- [ ] Conduzir levantamento de requisitos
- [ ] Facilitar identificação de entidades
- [ ] Desenhar diagrama ER coletivamente
- [ ] Implementar tabelas passo a passo
- [ ] Validar estrutura com turma
- [ ] Entregar exercício para casa

### Após a Aula
- [ ] Registrar frequência
- [ ] Salvar estrutura do banco criada
- [ ] Anotar dúvidas e dificuldades
- [ ] Preparar próxima aula

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Compreensão da turma:
- Levantamento de requisitos: ___/10
- Identificação de entidades: ___/10
- Modelagem ER: ___/10
- Chaves estrangeiras: ___/10

Participação:
- Discussões: ___/10
- Exercícios em grupo: ___/10

Estrutura criada:
- Completa: Sim ( ) Não ( )
- Funcional: Sim ( ) Não ( )

Dificuldades principais:
- 

Ajustes necessários:
- 

Tempo real: _____ min
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
