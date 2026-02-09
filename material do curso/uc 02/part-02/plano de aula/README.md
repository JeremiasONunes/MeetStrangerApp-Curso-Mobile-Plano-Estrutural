# 📚 Planos de Aula - UC 02 Parte 02: Banco de Dados

**Curso:** Programador Mobile  
**Unidade Curricular:** 02 - Programação de Dispositivos Móveis  
**Parte:** 02 - Banco de Dados  
**Carga Horária Total:** 30 horas (7 aulas + 1 extra)  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivo Geral da Parte 02

Desenvolver competências em modelagem e manipulação de banco de dados, preparando os estudantes para implementar a persistência de dados do projeto **MeetStranger** através do domínio de:
- Modelagem de dados (ER)
- SQL (DDL, DML, DQL)
- Integridade referencial
- Regras de negócio em banco de dados
- Consultas e relatórios

---

## 📋 Estrutura dos Planos de Aula

### Aula 01 - Introdução a Banco de Dados, SQL e CREATE (4h)
**Arquivo:** `aula-01-introducao-bd-sql-create.md`  
**Data:** 18/03/2026

**Objetivos:**
- Compreender papel do BD em apps mobile
- Diferenciar tipos de bancos (SQL vs NoSQL)
- Executar CREATE DATABASE e TABLE

**Conteúdos:**
- Conceito de BD e SGBD
- Tipos de bancos de dados
- Introdução ao SQL
- Comandos DDL (CREATE)
- Tipos de dados básicos
- Chave primária

**Destaques:**
- Foco em SQLite (mobile)
- Exemplos didáticos (biblioteca, escola)
- Exercício: banco "loja_online"

---

### Aula 02 - Modelagem e CREATE Aplicado ao MeetStranger (4h)
**Arquivo:** `aula-02-modelagem-create-meetstranger.md`  
**Data:** 19/03/2026

**Objetivos:**
- Aplicar modelagem a projeto real
- Criar estrutura completa do MeetStranger
- Implementar chaves estrangeiras

**Conteúdos:**
- Levantamento de requisitos
- Identificação de entidades e atributos
- Modelagem ER simplificada
- CREATE TABLE do projeto
- Chaves primárias e estrangeiras

**Destaques:**
- 5 tabelas implementadas
- Diagrama ER completo
- Índices para performance
- Validação coletiva

---

### Aula 03 - Manipulação de Dados: INSERT, UPDATE e DELETE (4h)
**Arquivo:** `aula-03-insert-update-delete.md`  
**Data:** 20/03/2026

**Objetivos:**
- Manipular dados com segurança
- Aplicar operações CRUD
- Usar transações

**Conteúdos:**
- Comando INSERT
- Comando UPDATE
- Comando DELETE
- Boas práticas
- Riscos e prevenção

**Destaques:**
- Ênfase em WHERE obrigatório
- Transações (BEGIN/COMMIT/ROLLBACK)
- População completa do banco
- Cenários reais simulados

---

### Aula 04 - Revisão Técnica (4h - Extra)
**Arquivo:** `aula-04-revisao-tecnica.md`  
**Data:** 21/03/2026  
**Observação:** Não contabilizada na carga horária

**Objetivos:**
- Consolidar CREATE e CRUD
- Corrigir falhas de modelagem
- Nivelar turma

**Conteúdos:**
- Revisão completa
- Ajustes estruturais
- Atendimento individual
- Trabalho em grupos

**Destaques:**
- Aula de reforço
- 3 estações de atendimento
- 4 grupos com módulos diferentes
- Checklist de validação

---

### Aula 05 - INSERT e UPDATE com Regras de Negócio (4h)
**Arquivo:** `aula-05-insert-update-regras-negocio.md`  
**Data:** 23/03/2026

**Objetivos:**
- Aplicar regras de negócio
- Garantir integridade
- Simular cenários reais

**Conteúdos:**
- Inserções condicionais
- Atualizações baseadas em critérios
- Integridade de dados
- Validações complexas

**Destaques:**
- Cadastro com validações
- Login completo
- Matching com verificações
- Estatísticas automáticas
- Logout com limpeza

---

### Aula 06 - Consultas SQL: SELECT em Tabelas (4h)
**Arquivo:** `aula-06-select-consultas.md`  
**Data:** 24/03/2026

**Objetivos:**
- Recuperar dados eficientemente
- Filtrar e ordenar resultados
- Usar funções de agregação

**Conteúdos:**
- Comando SELECT
- Cláusula WHERE
- ORDER BY e LIMIT
- Funções agregação (COUNT, SUM, AVG, MIN, MAX)
- GROUP BY e HAVING

**Destaques:**
- Operadores relacionais e lógicos
- LIKE, IN, BETWEEN
- Paginação com LIMIT/OFFSET
- Dashboard do MeetStranger

---

### Aula 07 - SELECT Avançado e Encerramento (4h)
**Arquivo:** `aula-07-select-avancado-encerramento.md`  
**Data:** 25/03/2026

**Objetivos:**
- Consolidar SQL no projeto
- Criar consultas complexas
- Finalizar módulo

**Conteúdos:**
- JOIN (INNER, LEFT)
- Subconsultas
- Consultas avançadas
- Avaliação prática
- Integração com backend

**Destaques:**
- Múltiplos JOINs
- EXISTS e NOT EXISTS
- Relatórios gerenciais
- Avaliação final (100 pontos)
- Certificação de conclusão

---

## 🎓 Metodologia Pedagógica

### Abordagem Geral
- **Projeto Real**: Todos os exemplos do MeetStranger
- **Progressão Gradual**: Conceitos básicos → avançados
- **Prática Intensiva**: 70% prática, 30% teoria
- **Validação Contínua**: Verificar estrutura constantemente

### Estrutura de Cada Aula
1. **Retomada** (10-15%): Revisão da aula anterior
2. **Apresentação** (20-25%): Novos conceitos
3. **Prática Guiada** (30-35%): Exercícios orientados
4. **Prática Autônoma** (25-30%): Trabalho individual/grupo
5. **Síntese** (5-10%): Recapitulação

### Recursos Didáticos
- SQLite (banco local)
- VS Code com extensões SQL
- Quadro para diagramas ER
- Scripts SQL prontos
- Documentação do MeetStranger

---

## 📊 Sistema de Avaliação

### Distribuição de Notas

| Aula | Peso | Foco |
|------|------|------|
| Aula 01 | 10% | CREATE básico |
| Aula 02 | 15% | Modelagem MeetStranger |
| Aula 03 | 20% | INSERT, UPDATE, DELETE |
| Aula 04 | - | Revisão (não avaliada) |
| Aula 05 | 20% | Regras de negócio |
| Aula 06 | 20% | SELECT e consultas |
| Aula 07 | 15% | JOIN e avaliação final |
| **Total** | **100%** | **Nota da Parte 2** |

### Critérios de Avaliação

**Conhecimentos (40%):**
- Modelagem de dados
- Sintaxe SQL correta
- Conceitos de integridade

**Habilidades (40%):**
- Criar estruturas adequadas
- Manipular dados com segurança
- Consultar eficientemente

**Atitudes (20%):**
- Atenção à integridade
- Organização
- Documentação

---

## 🎯 Competências Desenvolvidas

### Conhecimentos
✅ Modelagem Entidade-Relacionamento  
✅ SQL (DDL, DML, DQL, DCL)  
✅ Tipos de dados  
✅ Chaves primárias e estrangeiras  
✅ Integridade referencial  
✅ Normalização básica  
✅ Índices e performance  

### Habilidades
✅ Modelar banco de dados  
✅ Criar estruturas (CREATE)  
✅ Inserir dados (INSERT)  
✅ Atualizar dados (UPDATE)  
✅ Deletar dados (DELETE)  
✅ Consultar dados (SELECT)  
✅ Fazer JOIN entre tabelas  
✅ Aplicar regras de negócio  
✅ Gerar relatórios  

### Atitudes
✅ Atenção à integridade dos dados  
✅ Cuidado com dados sensíveis  
✅ Organização e documentação  
✅ Validação antes de executar  
✅ Trabalho colaborativo  

---

## 📚 Progressão de Conteúdos

```
Aula 01: Fundamentos SQL e CREATE
    ↓
Aula 02: Modelagem MeetStranger
    ↓
Aula 03: INSERT, UPDATE, DELETE
    ↓
Aula 04: Revisão e Nivelamento (extra)
    ↓
Aula 05: Regras de Negócio
    ↓
Aula 06: SELECT e Consultas
    ↓
Aula 07: JOIN e Encerramento
    ↓
Preparado para Parte 03: Backend
```

---

## 🔗 Estrutura do Banco MeetStranger

### Tabelas Implementadas

**1. usuarios**
```sql
- id (PK, AUTOINCREMENT)
- username (UNIQUE, NOT NULL)
- email (UNIQUE, NOT NULL)
- senha (NOT NULL)
- criado_em (DATETIME)
- ultimo_login (DATETIME)
- online (BOOLEAN)
```

**2. categorias**
```sql
- id (PK, AUTOINCREMENT)
- nome (UNIQUE, NOT NULL)
- descricao (TEXT)
- icone (TEXT)
- ativa (BOOLEAN)
```

**3. salas**
```sql
- id (PK, AUTOINCREMENT)
- categoria_id (FK → categorias)
- usuario1_id (FK → usuarios)
- usuario2_id (FK → usuarios)
- criada_em (DATETIME)
- encerrada_em (DATETIME)
- ativa (BOOLEAN)
```

**4. fila_matching**
```sql
- id (PK, AUTOINCREMENT)
- usuario_id (FK → usuarios, UNIQUE)
- categoria_id (FK → categorias)
- entrou_em (DATETIME)
- posicao (INTEGER)
```

**5. estatisticas_usuario**
```sql
- id (PK, AUTOINCREMENT)
- usuario_id (FK → usuarios, UNIQUE)
- total_conversas (INTEGER)
- tempo_total_minutos (INTEGER)
- categoria_favorita_id (FK → categorias)
- ultima_atualizacao (DATETIME)
```

### Relacionamentos
```
usuarios 1:N salas (usuario1_id)
usuarios 1:N salas (usuario2_id)
usuarios 1:1 estatisticas_usuario
usuarios 1:1 fila_matching
categorias 1:N salas
categorias 1:N fila_matching
```

---

## 💡 Dicas para o Docente

### Preparação
1. Instalar SQLite em todos os computadores
2. Configurar VS Code com extensões
3. Testar todos os scripts antes
4. Preparar banco de backup
5. Ter exemplos extras prontos

### Durante as Aulas
1. Executar comandos ao vivo
2. Mostrar erros comuns
3. Circular pela sala constantemente
4. Validar estrutura frequentemente
5. Conectar sempre com MeetStranger

### Gestão de Turma
1. Formar grupos mistos
2. Incentivar peer teaching
3. Permitir erros em ambiente seguro
4. Dar feedback imediato
5. Celebrar progressos

### Avaliação
1. Avaliar processo e resultado
2. Dar feedback construtivo
3. Permitir refazer (aula 04)
4. Valorizar evolução
5. Documentar dificuldades

---

## 📁 Estrutura de Arquivos

```
plano de aula/
├── README.md (este arquivo)
├── aula-01-introducao-bd-sql-create.md
├── aula-02-modelagem-create-meetstranger.md
├── aula-03-insert-update-delete.md
├── aula-04-revisao-tecnica.md (extra)
├── aula-05-insert-update-regras-negocio.md
├── aula-06-select-consultas.md
└── aula-07-select-avancado-encerramento.md
```

---

## 🎯 Resultados Esperados

Ao final da Parte 02, o estudante deve ser capaz de:

✅ Modelar banco de dados relacional  
✅ Criar estruturas com CREATE  
✅ Inserir dados com validações  
✅ Atualizar dados com segurança  
✅ Deletar dados de forma controlada  
✅ Consultar dados eficientemente  
✅ Fazer JOIN entre tabelas  
✅ Usar funções de agregação  
✅ Aplicar regras de negócio  
✅ Gerar relatórios gerenciais  
✅ Manter integridade referencial  
✅ Documentar decisões de modelagem  

---

## 🔄 Próximos Passos

### Parte 03 - Backend (30h)
- Node.js e Express
- API REST
- Integração com SQLite
- WebSocket
- Autenticação JWT

### Parte 04 - Frontend Mobile (30h)
- React Native
- Expo
- Integração com API
- Interface completa

---

## 📞 Suporte

### Para Docentes
- Consultar PTD completo: `../ptd-uc02-pt02.md`
- Documentação do projeto: `../../documentacao-projeto/`
- Scripts SQL de apoio

### Para Estudantes
- Revisar planos antes das aulas
- Fazer exercícios para casa
- Participar ativamente
- Tirar dúvidas
- Colaborar com colegas

---

## 📊 Estatísticas dos Planos

| Métrica | Valor |
|---------|-------|
| Total de Aulas | 7 aulas + 1 extra |
| Carga Horária | 30 horas (oficial) |
| Tabelas Criadas | 5 tabelas |
| Comandos SQL | 200+ exemplos |
| Exercícios | 50+ exercícios |
| Consultas Complexas | 30+ exemplos |
| Páginas de Conteúdo | 120+ páginas |

---

## ✅ Checklist de Uso

### Para o Docente

**Antes do Início da Parte 02:**
- [ ] Ler todos os planos de aula
- [ ] Revisar PTD da UC 02 Parte 02
- [ ] Instalar SQLite em todos os computadores
- [ ] Configurar VS Code
- [ ] Preparar banco de exemplo

**Antes de Cada Aula:**
- [ ] Revisar plano específico
- [ ] Testar todos os comandos SQL
- [ ] Preparar scripts
- [ ] Verificar equipamentos
- [ ] Preparar exercícios

**Após Cada Aula:**
- [ ] Registrar frequência
- [ ] Salvar estado do banco
- [ ] Anotar dificuldades
- [ ] Corrigir exercícios
- [ ] Preparar próxima aula

**Ao Final da Parte 02:**
- [ ] Consolidar notas
- [ ] Avaliar aprendizado geral
- [ ] Preparar relatório
- [ ] Planejar Parte 03

---

## 📝 Observações Importantes

### Adaptações
- Planos são flexíveis
- Ajustar ritmo conforme turma
- Incluir exemplos extras se necessário
- Simplificar para turmas iniciantes
- Desafios extras para avançadas

### Contexto Pedagógico
- Todos os exemplos usam MeetStranger
- Conexão constante com projeto real
- Preparação para backend (Parte 03)
- Foco em competências práticas

### Recursos Adicionais
- Scripts SQL disponíveis
- Banco de exemplo pronto
- Vídeos de apoio (se disponíveis)
- Ferramentas online (dbdiagram.io)

---

## 🎓 Referências Bibliográficas

### Principais
- **SQLite Documentation**: https://www.sqlite.org/docs.html
- **W3Schools SQL**: https://www.w3schools.com/sql/
- **SQL Tutorial**: https://www.sqltutorial.org/

### Complementares
- DATE, C. J. **Introdução a Sistemas de Bancos de Dados**. Campus, 2004.
- ELMASRI, R.; NAVATHE, S. **Sistemas de Banco de Dados**. 6ª ed. Pearson, 2011.

### Online
- SQLite Browser: https://sqlitebrowser.org/
- DB Diagram: https://dbdiagram.io/
- SQL Fiddle: http://sqlfiddle.com/

---

## 📄 Licença e Uso

**Elaborado por:** Jeremias O Nunes  
**Instituição:** SENAC  
**Curso:** Programador Mobile  
**Ano:** 2024  
**Versão:** 1.0

**Uso:**
- Material pedagógico para sala de aula
- Pode ser adaptado conforme necessidade
- Manter créditos ao adaptar
- Compartilhar melhorias

---

## 🚀 Status do Material

| Item | Status |
|------|--------|
| Planos de Aula | ✅ Completos (7 + 1 extra) |
| Scripts SQL | ✅ Completos |
| Exercícios | ✅ Completos |
| Gabaritos | ✅ Completos |
| Banco MeetStranger | ✅ Implementado |
| Avaliações | ✅ Definidas |

---

**Última Atualização:** 2024  
**Próxima Revisão:** Após aplicação com primeira turma

---

## 💬 Feedback

Sugestões de melhoria são bem-vindas!
- Docentes: anotar observações após cada aplicação
- Estudantes: compartilhar dificuldades e sugestões
- Coordenação: avaliar resultados e propor ajustes

---

✨ **Bons estudos e ótimas aulas de Banco de Dados!** ✨

🎉 **Parabéns por concluir a Parte 02!** 🎉
