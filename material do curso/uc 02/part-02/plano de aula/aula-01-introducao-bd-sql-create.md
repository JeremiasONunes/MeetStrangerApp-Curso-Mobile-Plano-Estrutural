# Aula 01 - Introdução a Banco de Dados, SQL e CREATE

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária:** 4 horas  
**Data:** 18/03/2026  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Compreender** o papel do banco de dados em aplicações mobile
2. **Diferenciar** tipos de bancos de dados (relacional e não relacional)
3. **Executar** comandos CREATE DATABASE e CREATE TABLE
4. **Aplicar** tipos de dados básicos e chaves primárias

---

## 📚 Conteúdos Programáticos

### 1. Conceito de Banco de Dados e SGBD (45 min)
- O que é banco de dados
- Sistema Gerenciador de Banco de Dados (SGBD)
- Importância em aplicações mobile
- Exemplos práticos

### 2. Tipos de Bancos de Dados (30 min)
- Bancos relacionais (SQL)
- Bancos não relacionais (NoSQL)
- Quando usar cada tipo
- Foco em bancos relacionais

### 3. Introdução à Linguagem SQL (45 min)
- O que é SQL
- Categorias de comandos (DDL, DML, DQL, DCL)
- Sintaxe básica
- Ferramentas (SQLite, MySQL, PostgreSQL)

### 4. Comandos DDL - CREATE (60 min)
- CREATE DATABASE
- CREATE TABLE
- Tipos de dados básicos
- Chave primária (PRIMARY KEY)

### 5. Prática Guiada (60 min)
- Criar banco de dados didático
- Criar tabelas simples
- Exercícios progressivos

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Contextualização (30 min)

**Problema Motivador:**
```
Situação: App de lista de tarefas

Sem banco de dados:
- Dados perdidos ao fechar app
- Não compartilha entre dispositivos
- Sem histórico

Com banco de dados:
- Dados persistentes
- Sincronização
- Histórico completo
```

**Discussão:**
- Onde os apps guardam dados?
- O que acontece quando desinstala?
- Como apps funcionam offline?

### Momento 2: Conceitos Fundamentais (45 min)

**Atividade 1:** O que é Banco de Dados? (15 min)
```
Banco de Dados: Coleção organizada de dados

Analogia: Biblioteca
- Livros = Dados
- Estantes = Tabelas
- Catálogo = Índices
- Bibliotecário = SGBD
```

**Atividade 2:** SGBD (15 min)
```
Sistema Gerenciador de Banco de Dados

Funções:
- Armazenar dados
- Recuperar dados
- Garantir segurança
- Manter integridade
- Controlar acesso

Exemplos:
- SQLite (mobile, local)
- MySQL (web, servidor)
- PostgreSQL (empresarial)
- MongoDB (NoSQL)
```

**Atividade 3:** Por que usar em Mobile? (15 min)
- Persistência de dados
- Consultas rápidas
- Organização estruturada
- Relacionamentos entre dados
- Segurança

### Momento 3: Tipos de Bancos de Dados (30 min)

**Atividade:** Comparação Visual

**Relacional (SQL):**
```
Estrutura: Tabelas com linhas e colunas

Exemplo: Usuários
┌────┬──────────┬────────────────────┐
│ id │ username │ email              │
├────┼──────────┼────────────────────┤
│ 1  │ joao123  │ joao@email.com     │
│ 2  │ maria456 │ maria@email.com    │
└────┴──────────┴────────────────────┘

Características:
✅ Estrutura rígida
✅ Relacionamentos claros
✅ SQL padrão
✅ ACID (transações)

Uso: Apps com dados estruturados
```

**Não Relacional (NoSQL):**
```
Estrutura: Documentos, chave-valor, grafos

Exemplo: Documento JSON
{
  "id": 1,
  "username": "joao123",
  "email": "joao@email.com",
  "preferencias": {
    "tema": "escuro",
    "notificacoes": true
  }
}

Características:
✅ Estrutura flexível
✅ Escalabilidade horizontal
✅ Sem esquema fixo

Uso: Apps com dados não estruturados
```

**Para o MeetStranger:** Usaremos **SQL (SQLite)** por ser ideal para mobile.

### Momento 4: Introdução ao SQL (45 min + 10 min intervalo)

**Atividade 1:** O que é SQL? (15 min)
```
SQL: Structured Query Language
Linguagem para gerenciar bancos relacionais

Características:
- Declarativa (diz O QUE, não COMO)
- Padrão internacional
- Usada em todos os SGBDs relacionais
```

**Atividade 2:** Categorias de Comandos (20 min)
```
DDL (Data Definition Language):
- CREATE: criar estruturas
- ALTER: modificar estruturas
- DROP: remover estruturas

DML (Data Manipulation Language):
- INSERT: inserir dados
- UPDATE: atualizar dados
- DELETE: excluir dados

DQL (Data Query Language):
- SELECT: consultar dados

DCL (Data Control Language):
- GRANT: dar permissões
- REVOKE: remover permissões
```

**Atividade 3:** Sintaxe Básica (10 min)
```sql
-- Comentário de linha única

/* 
   Comentário
   de múltiplas
   linhas
*/

-- Comandos terminam com ;
CREATE DATABASE exemplo;

-- SQL não é case-sensitive (mas convenção: MAIÚSCULAS)
CREATE DATABASE exemplo;
create database exemplo;  -- mesmo resultado
```

### Momento 5: Comandos CREATE (60 min)

**Atividade 1:** CREATE DATABASE (20 min)
```sql
-- Sintaxe básica
CREATE DATABASE nome_banco;

-- Exemplo
CREATE DATABASE escola;

-- Verificar bancos existentes
SHOW DATABASES;

-- Selecionar banco para usar
USE escola;
```

**Atividade 2:** CREATE TABLE (25 min)
```sql
-- Sintaxe básica
CREATE TABLE nome_tabela (
    coluna1 TIPO,
    coluna2 TIPO,
    coluna3 TIPO
);

-- Exemplo: Tabela de alunos
CREATE TABLE alunos (
    id INTEGER,
    nome TEXT,
    idade INTEGER,
    email TEXT
);

-- Verificar tabelas
SHOW TABLES;

-- Ver estrutura da tabela
DESCRIBE alunos;
```

**Atividade 3:** Tipos de Dados Básicos (15 min)
```sql
-- Tipos mais comuns

INTEGER ou INT
- Números inteiros
- Exemplo: idade, quantidade

REAL ou FLOAT ou DECIMAL
- Números decimais
- Exemplo: preço, nota

TEXT ou VARCHAR(tamanho)
- Texto/string
- Exemplo: nome, email

BOOLEAN
- Verdadeiro ou Falso
- Exemplo: ativo, online

DATE, TIME, DATETIME
- Datas e horas
- Exemplo: data_nascimento, criado_em
```

### Momento 6: Chave Primária (30 min)

**Atividade 1:** Conceito (10 min)
```
Chave Primária (PRIMARY KEY):
- Identifica UNICAMENTE cada registro
- Não pode ser NULL
- Não pode repetir
- Geralmente é um ID

Analogia: CPF, RG, matrícula
```

**Atividade 2:** Implementação (20 min)
```sql
-- Tabela COM chave primária
CREATE TABLE alunos (
    id INTEGER PRIMARY KEY,
    nome TEXT,
    idade INTEGER,
    email TEXT
);

-- Com auto-incremento (SQLite)
CREATE TABLE alunos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    idade INTEGER,
    email TEXT UNIQUE
);

-- Restrições:
-- NOT NULL: campo obrigatório
-- UNIQUE: valor único na tabela
-- PRIMARY KEY: chave primária
-- AUTOINCREMENT: incrementa automaticamente
```

### Momento 7: Prática Guiada (60 min)

**Atividade 1:** Criar Banco Didático (15 min)
```sql
-- Criar banco de dados
CREATE DATABASE biblioteca;

-- Usar o banco
USE biblioteca;

-- Verificar
SHOW DATABASES;
```

**Atividade 2:** Criar Tabela de Livros (20 min)
```sql
CREATE TABLE livros (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    titulo TEXT NOT NULL,
    autor TEXT NOT NULL,
    ano_publicacao INTEGER,
    isbn TEXT UNIQUE,
    disponivel BOOLEAN DEFAULT TRUE
);

-- Verificar estrutura
DESCRIBE livros;
```

**Atividade 3:** Criar Tabela de Autores (15 min)
```sql
CREATE TABLE autores (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    nacionalidade TEXT,
    data_nascimento DATE
);
```

**Atividade 4:** Exercício Individual (10 min)
```
Criar tabela "categorias" com:
- id (chave primária, auto-incremento)
- nome (texto, obrigatório, único)
- descricao (texto)
```

### Momento 8: Fechamento (30 min)

**Atividade 1:** Discussão sobre Modelagem (15 min)
- Por que planejar antes de criar?
- O que acontece se criar errado?
- Como corrigir depois?

**Atividade 2:** Síntese (10 min)
- Recapitular conceitos principais
- Conexão com próxima aula (MeetStranger)

**Atividade 3:** Exercício para Casa (5 min)
- Entregar e explicar

---

## 📝 Atividades Práticas

### Exercício 1: Banco de Dados de Escola

```sql
-- 1. Criar banco de dados
CREATE DATABASE escola;
USE escola;

-- 2. Criar tabela de estudantes
CREATE TABLE estudantes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    matricula TEXT UNIQUE NOT NULL,
    data_nascimento DATE,
    email TEXT UNIQUE,
    ativo BOOLEAN DEFAULT TRUE
);

-- 3. Criar tabela de cursos
CREATE TABLE cursos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    carga_horaria INTEGER,
    descricao TEXT
);

-- 4. Verificar estruturas
DESCRIBE estudantes;
DESCRIBE cursos;
```

### Exercício 2: Tipos de Dados

```sql
-- Criar tabela com diversos tipos
CREATE TABLE exemplo_tipos (
    id INTEGER PRIMARY KEY,
    texto TEXT,
    inteiro INTEGER,
    decimal REAL,
    booleano BOOLEAN,
    data DATE,
    hora TIME,
    data_hora DATETIME
);
```

### Exercício 3: Restrições

```sql
-- Tabela com várias restrições
CREATE TABLE usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    email TEXT NOT NULL UNIQUE,
    senha TEXT NOT NULL,
    idade INTEGER CHECK (idade >= 13),
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### Exercício para Casa

**Parte 1: Criar Banco de Dados de Loja**

Criar banco "loja_online" com as seguintes tabelas:

1. **produtos**
   - id (chave primária, auto-incremento)
   - nome (texto, obrigatório)
   - preco (decimal, obrigatório)
   - estoque (inteiro, padrão 0)
   - ativo (booleano, padrão verdadeiro)

2. **clientes**
   - id (chave primária, auto-incremento)
   - nome (texto, obrigatório)
   - email (texto, único, obrigatório)
   - telefone (texto)
   - data_cadastro (data/hora, padrão atual)

3. **categorias**
   - id (chave primária, auto-incremento)
   - nome (texto, único, obrigatório)
   - descricao (texto)

**Parte 2: Documentar**

Para cada tabela, descrever:
- Qual o propósito?
- Por que cada campo é necessário?
- Por que escolheu cada tipo de dado?

**Formato de Entrega:**
- Arquivo .sql com os comandos
- Documento .txt com as descrições

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Conhecimento prévio sobre bancos de dados
- Experiência com SQL

### Avaliação Formativa

**Critérios:**
- ✅ Compreende conceito de banco de dados
- ✅ Diferencia tipos de bancos
- ✅ Executa CREATE DATABASE corretamente
- ✅ Cria tabelas com tipos adequados
- ✅ Aplica chaves primárias
- ✅ Usa restrições (NOT NULL, UNIQUE)

**Instrumentos:**
- Observação durante prática
- Exercícios em aula
- Participação nas discussões

### Avaliação Somativa
- Exercícios em aula: 40%
- Exercício para casa: 60%

**Peso da Aula:** 10% da nota da Parte 2

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Explica o papel do banco de dados em apps mobile  
✅ Diferencia bancos relacionais de não relacionais  
✅ Cria bancos de dados com CREATE DATABASE  
✅ Cria tabelas com estrutura adequada  
✅ Escolhe tipos de dados apropriados  
✅ Define chaves primárias corretamente  
✅ Aplica restrições (NOT NULL, UNIQUE)  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Computadores com SQLite instalado
- [ ] VS Code com extensão SQLite
- [ ] Projetor/TV
- [ ] Slides da aula
- [ ] Quadro branco
- [ ] Exercícios impressos

### Ferramentas

**SQLite:**
- Leve e portátil
- Ideal para mobile
- Sem servidor
- Arquivo único

**Instalação:**
```bash
# Windows (via Chocolatey)
choco install sqlite

# Ou baixar: https://www.sqlite.org/download.html
```

**VS Code Extensions:**
- SQLite Viewer
- SQLite Explorer
- SQL Formatter

### Referências
- **SQLite Documentation**: https://www.sqlite.org/docs.html
- **W3Schools SQL**: https://www.w3schools.com/sql/
- **SQL Tutorial**: https://www.sqltutorial.org/

---

## 🔄 Conexão com Outras Aulas

### Revisão da Parte 01
- Algoritmos e lógica
- Estruturas de dados (listas)
- Conceito de CRUD

### Preparação para Aula 02
- Modelagem do MeetStranger
- CREATE TABLE aplicado ao projeto
- Chaves estrangeiras

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 45 min
- ⏰ Momento 3: 30 min
- ⏰ Momento 4: 55 min (com intervalo)
- ⏰ Momento 5: 60 min
- ⏰ Momento 6: 30 min
- ⏰ Momento 7: 60 min
- ⏰ Momento 8: 30 min

### Pontos de Atenção
1. **Primeira aula de SQL**: Ir devagar, explicar bem
2. **Sintaxe**: Enfatizar ponto e vírgula
3. **Tipos de dados**: Variam entre SGBDs
4. **Chave primária**: Conceito fundamental
5. **Prática**: Mais importante que teoria

### Estratégias
- Usar analogias do mundo real
- Mostrar exemplos de apps conhecidos
- Executar comandos ao vivo
- Deixar estudantes experimentarem
- Errar e corrigir junto com a turma

### Adaptações
- **Turma iniciante**: Mais tempo em conceitos básicos
- **Turma avançada**: Introduzir constraints avançados
- **EAD**: Gravar execução de comandos

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Instalar SQLite em todos os computadores
- [ ] Testar VS Code com extensões
- [ ] Preparar slides
- [ ] Criar exemplos de demonstração
- [ ] Preparar exercícios

### Durante a Aula
- [ ] Apresentar conceitos fundamentais
- [ ] Demonstrar comandos ao vivo
- [ ] Conduzir prática guiada
- [ ] Circular pela sala
- [ ] Dar feedback imediato
- [ ] Entregar exercício para casa

### Após a Aula
- [ ] Registrar frequência
- [ ] Anotar dificuldades
- [ ] Verificar se todos conseguiram instalar
- [ ] Preparar próxima aula

---

## 📝 Gabarito - Exercício para Casa

```sql
-- PARTE 1: Criar Banco e Tabelas

-- 1. Criar banco de dados
CREATE DATABASE loja_online;
USE loja_online;

-- 2. Tabela produtos
CREATE TABLE produtos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    preco REAL NOT NULL,
    estoque INTEGER DEFAULT 0,
    ativo BOOLEAN DEFAULT TRUE
);

-- 3. Tabela clientes
CREATE TABLE clientes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    telefone TEXT,
    data_cadastro DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- 4. Tabela categorias
CREATE TABLE categorias (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT UNIQUE NOT NULL,
    descricao TEXT
);

-- Verificar estruturas
DESCRIBE produtos;
DESCRIBE clientes;
DESCRIBE categorias;
```

**PARTE 2: Documentação**

**Tabela produtos:**
- Propósito: Armazenar informações dos produtos da loja
- id: Identificador único do produto
- nome: Nome do produto (obrigatório para identificação)
- preco: Valor do produto (REAL para aceitar centavos)
- estoque: Quantidade disponível (INTEGER, padrão 0)
- ativo: Se produto está à venda (BOOLEAN)

**Tabela clientes:**
- Propósito: Cadastro de clientes da loja
- id: Identificador único do cliente
- nome: Nome completo (obrigatório)
- email: Email único para login (UNIQUE para evitar duplicatas)
- telefone: Contato opcional
- data_cadastro: Registro automático da data

**Tabela categorias:**
- Propósito: Organizar produtos por categoria
- id: Identificador único
- nome: Nome da categoria (UNIQUE para evitar duplicatas)
- descricao: Detalhes sobre a categoria

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Compreensão da turma:
- Conceitos: ___/10
- CREATE DATABASE: ___/10
- CREATE TABLE: ___/10
- Tipos de dados: ___/10

Dificuldades encontradas:
- 

Instalação do SQLite:
- Sucesso: ___ alunos
- Problemas: ___ alunos

Ajustes necessários:
- 

Tempo real por momento:
1. _____ min
2. _____ min
3. _____ min
4. _____ min
5. _____ min
6. _____ min
7. _____ min
8. _____ min
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
