# 🎓 Contexto Pedagógico - Projeto MeetStranger

## 1. Visão Geral Pedagógica

### 1.1 Propósito Educacional
O projeto **MeetStranger** foi concebido como um **projeto integrador** que perpassa todas as Unidades Curriculares do curso **Programador Mobile**, servindo como fio condutor para aplicação prática dos conceitos teóricos.

### 1.2 Abordagem Metodológica
- **Aprendizagem Baseada em Projetos (PBL)** - Desenvolvimento incremental
- **Metodologias Ágeis** - Scrum e Kanban aplicados
- **Aprendizagem Ativa** - Hands-on em todas as etapas
- **Desenvolvimento Incremental** - Evolução por UCs

## 2. Conexão com as Unidades Curriculares

### 2.1 UC 01 - Planejar o Desenvolvimento de Softwares (36h)

#### Objetivos de Aprendizagem
- Analisar requisitos do cliente
- Identificar recursos tecnológicos adequados
- Aplicar metodologias de desenvolvimento
- Documentar regras de negócio

#### Aplicação no MeetStranger
| Atividade | Entregável | Competência Desenvolvida |
|-----------|-----------|-------------------------|
| Análise de requisitos | Documento de requisitos funcionais e não funcionais | Leitura e interpretação de demandas |
| Definição de regras de negócio | Documento de regras de negócio | Análise sistêmica |
| Escolha de metodologia | Quadros Scrum/Kanban | Organização de trabalho |
| Prototipação | Protótipos no Canva/Stitch | Comunicação visual |
| Planejamento técnico | Arquitetura do sistema | Visão técnica |

#### Indicadores Avaliados
1. ✅ Analisa os requisitos do cliente de forma a atender a suas demandas
2. ✅ Identifica os melhores recursos tecnológicos para atender à proposta

#### Elementos de Competência
**Conhecimentos:**
- Regras de negócio: conceitos, características, tipos
- Requisitos funcionais e não funcionais
- Metodologias ágeis: Scrum, Kanban

**Habilidades:**
- Comunicar-se com clareza
- Ler e interpretar documentos técnicos
- Trabalhar em equipe

**Atitudes:**
- Comportamento ético
- Visão sistêmica
- Atitude colaborativa

---

### 2.2 UC 02 Parte 1 - Lógica de Programação (30h)

#### Objetivos de Aprendizagem
- Desenvolver raciocínio lógico
- Construir algoritmos estruturados
- Manipular estruturas de dados
- Aplicar conceitos de POO

#### Aplicação no MeetStranger
| Atividade | Entregável | Competência Desenvolvida |
|-----------|-----------|-------------------------|
| Algoritmos de validação | Validação de cadastro | Lógica condicional |
| Estruturas de repetição | Listagem de usuários | Iteração de dados |
| Manipulação de arrays | Gerenciamento de mensagens | Estruturas de dados |
| Modelagem de classes | Classes User, Message, Topic | Orientação a objetos |

#### Conceitos Aplicados
- ✅ Variáveis e constantes (dados de usuário, tópicos)
- ✅ Operadores lógicos (validações)
- ✅ Estruturas condicionais (fluxo de autenticação)
- ✅ Estruturas de repetição (listagem de mensagens)
- ✅ Arrays e listas (coleção de usuários/mensagens)
- ✅ Funções (modularização do código)

#### Elementos de Competência
**Conhecimentos:**
- Algoritmos e lógica de programação
- Estruturas de dados (pilhas, filas, listas)
- Fundamentos de orientação a objetos

**Habilidades:**
- Resolver problemas lógicos
- Construir expressões lógicas
- Organizar código

---

### 2.3 UC 02 Parte 2 - Banco de Dados (30h)

#### Objetivos de Aprendizagem
- Modelar banco de dados relacional
- Implementar SQL (DDL e DML)
- Garantir integridade referencial
- Aplicar normalização

#### Aplicação no MeetStranger
| Atividade | Entregável | Competência Desenvolvida |
|-----------|-----------|-------------------------|
| Modelagem conceitual | Diagrama ER | Análise de dados |
| Criação de tabelas | Scripts SQL (CREATE) | Implementação de estruturas |
| CRUD de usuários | Scripts SQL (INSERT, UPDATE, DELETE, SELECT) | Manipulação de dados |
| Consultas avançadas | Queries com JOIN, filtros | Recuperação eficiente |
| Segurança de dados | Controle de acesso | Proteção de informações |

#### Entidades Principais
1. **users** - Dados de autenticação
2. **topics** - Categorias de conversa
3. **chat_sessions** - Sessões de chat
4. **messages** - Mensagens trocadas (temporárias)

#### Elementos de Competência
**Conhecimentos:**
- Modelagem de dados (ER)
- SQL: DDL e DML
- Normalização
- Integridade referencial
- Segurança de banco de dados

**Habilidades:**
- Modelar estruturas de dados
- Escrever consultas SQL
- Otimizar queries

---

### 2.4 UC 02 Parte 3 - Backend com Node.js (30h)

#### Objetivos de Aprendizagem
- Desenvolver APIs REST
- Integrar backend com banco de dados
- Implementar autenticação
- Tratar erros e exceções

#### Aplicação no MeetStranger
| Atividade | Entregável | Competência Desenvolvida |
|-----------|-----------|-------------------------|
| Configuração do servidor | Servidor Express | Setup de ambiente |
| Rotas de autenticação | POST /login, /register | APIs REST |
| CRUD de usuários | Endpoints completos | Integração com BD |
| WebSocket para chat | Socket.io implementado | Comunicação real-time |
| Middleware de segurança | JWT, validações | Segurança de APIs |

#### Endpoints Principais
```
POST   /api/auth/register      - Cadastro
POST   /api/auth/login         - Login
GET    /api/topics             - Listar tópicos
POST   /api/chat/connect       - Conectar ao chat
POST   /api/chat/disconnect    - Desconectar
WS     /socket.io              - WebSocket
```

#### Elementos de Competência
**Conhecimentos:**
- Node.js e Express
- APIs REST
- Autenticação (JWT)
- WebSocket
- Tratamento de erros

**Habilidades:**
- Desenvolver servidores web
- Integrar sistemas
- Implementar segurança

---

### 2.5 UC 02 Parte 4 - Frontend Mobile (30h)

#### Objetivos de Aprendizagem
- Desenvolver interfaces mobile
- Implementar navegação
- Consumir APIs REST
- Gerenciar estado da aplicação

#### Aplicação no MeetStranger
| Atividade | Entregável | Competência Desenvolvida |
|-----------|-----------|-------------------------|
| Setup React Native | Projeto configurado | Ambiente mobile |
| Telas de autenticação | Login/Register | Formulários e validação |
| Navegação | Expo Router | Fluxo de telas |
| Seleção de tópicos | Tela de escolha | Componentes interativos |
| Chat em tempo real | Tela de chat | WebSocket no mobile |
| Design System | Componentes reutilizáveis | UI/UX |

#### Telas Desenvolvidas
1. **Welcome** - Apresentação do app
2. **Login** - Autenticação
3. **Register** - Cadastro
4. **Home** - Tela principal
5. **Chat Select** - Escolha de tópico
6. **Chat Room** - Conversa P2P
7. **About** - Informações do app

#### Elementos de Competência
**Conhecimentos:**
- React Native
- Componentes e Props
- Hooks (useState, useEffect)
- Navegação mobile
- Consumo de APIs

**Habilidades:**
- Desenvolver interfaces
- Integrar frontend/backend
- Gerenciar estado

---

### 2.6 UC 03 - Testes de Software (36h)

#### Objetivos de Aprendizagem
- Planejar estratégias de teste
- Executar testes manuais e automatizados
- Documentar defeitos
- Recomendar melhorias

#### Aplicação no MeetStranger
| Atividade | Entregável | Competência Desenvolvida |
|-----------|-----------|-------------------------|
| Plano de testes | Documento de estratégia | Planejamento de QA |
| Casos de teste | TestLink | Modelagem de testes |
| Testes funcionais | Relatório de execução | Validação funcional |
| Testes de performance | Análise de carga | Qualidade não funcional |
| Testes de segurança | Relatório de vulnerabilidades | Segurança |
| Registro de bugs | Mantis | Rastreamento de defeitos |
| Testes automatizados | Scripts Jest | Automação |

#### Níveis de Teste Aplicados
1. **Unitário** - Funções isoladas (validações, formatações)
2. **Integração** - Frontend + Backend + BD
3. **Sistema** - Fluxo completo do app
4. **Aceitação** - Validação com critérios de negócio

#### Tipos de Teste Executados
- ✅ Funcional (todas as features)
- ✅ Regressão (após mudanças)
- ✅ Desempenho (tempo de resposta)
- ✅ Carga (múltiplos usuários)
- ✅ Segurança (autenticação, dados)
- ✅ Usabilidade (UX)
- ✅ Exploratório (cenários não previstos)

#### Elementos de Competência
**Conhecimentos:**
- Conceitos de teste
- Níveis e tipos de teste
- Técnicas de modelagem
- Ferramentas de teste

**Habilidades:**
- Planejar testes
- Executar testes
- Documentar resultados
- Analisar qualidade

---

## 3. Progressão de Complexidade

### 3.1 Evolução do Projeto por UC

```
UC 01: PLANEJAMENTO
├─ Requisitos documentados
├─ Protótipos criados
└─ Arquitetura definida
    ↓
UC 02-1: LÓGICA
├─ Algoritmos estruturados
├─ Classes modeladas
└─ Estruturas de dados definidas
    ↓
UC 02-2: BANCO DE DADOS
├─ Modelagem ER completa
├─ Tabelas criadas
└─ CRUD implementado em SQL
    ↓
UC 02-3: BACKEND
├─ API REST funcional
├─ Integração com BD
└─ WebSocket implementado
    ↓
UC 02-4: FRONTEND
├─ Aplicativo mobile completo
├─ Integração frontend/backend
└─ UX finalizada
    ↓
UC 03: TESTES
├─ Qualidade validada
├─ Bugs corrigidos
└─ Produto final entregue
```

### 3.2 Complexidade Crescente

| UC | Complexidade | Dependências | Autonomia do Aluno |
|----|-------------|--------------|-------------------|
| UC 01 | Baixa | Nenhuma | Alta (conceitual) |
| UC 02-1 | Média | UC 01 | Média (prática guiada) |
| UC 02-2 | Média-Alta | UC 01, 02-1 | Média (SQL) |
| UC 02-3 | Alta | UC 01, 02-1, 02-2 | Baixa (integração) |
| UC 02-4 | Alta | Todas anteriores | Baixa (integração) |
| UC 03 | Média | Todas anteriores | Alta (validação) |

## 4. Metodologias Ativas Aplicadas

### 4.1 Por Tipo de Atividade

| Metodologia | Aplicação no Projeto | UC |
|-------------|---------------------|-----|
| **PBL** (Project-Based Learning) | Projeto integrador completo | Todas |
| **Peer Learning** | Trabalho em equipe, code review | Todas |
| **Hands-on** | Desenvolvimento prático em todas as aulas | UC 02, 03 |
| **Design Thinking** | Prototipação e UX | UC 01, 02-4 |
| **Scrum** | Sprints de desenvolvimento | UC 01, 02 |
| **Estudo de Caso** | Análise de apps similares | UC 01, 03 |

### 4.2 Dinâmicas de Aula

#### Aulas Expositivas (30%)
- Conceitos teóricos fundamentais
- Demonstrações práticas do docente
- Apresentação de ferramentas

#### Aulas Práticas (60%)
- Desenvolvimento guiado
- Exercícios hands-on
- Resolução de problemas

#### Aulas Colaborativas (10%)
- Discussões em grupo
- Apresentações de alunos
- Code review coletivo

## 5. Avaliação Integrada

### 5.1 Instrumentos de Avaliação

| Instrumento | Tipo | Peso | UC |
|-------------|------|------|-----|
| Documentação de requisitos | Formativa | 15% | UC 01 |
| Protótipos | Formativa | 10% | UC 01 |
| Algoritmos e código | Formativa | 15% | UC 02-1 |
| Modelagem e SQL | Formativa | 15% | UC 02-2 |
| API funcional | Formativa | 15% | UC 02-3 |
| Aplicativo mobile | Somativa | 20% | UC 02-4 |
| Relatório de testes | Somativa | 10% | UC 03 |

### 5.2 Critérios de Qualidade

#### Excelente (9-10)
- Todos os requisitos implementados
- Código limpo e documentado
- Testes completos e aprovados
- Apresentação profissional

#### Bom (7-8)
- Requisitos principais implementados
- Código funcional com pequenas melhorias
- Testes básicos executados
- Documentação adequada

#### Satisfatório (6-7)
- Funcionalidades essenciais funcionando
- Código funcional mas desorganizado
- Testes mínimos
- Documentação incompleta

#### Insatisfatório (<6)
- Requisitos não atendidos
- Código não funcional
- Sem testes
- Documentação ausente

## 6. Competências Desenvolvidas

### 6.1 Técnicas (Hard Skills)
- ✅ Programação em JavaScript/TypeScript
- ✅ Desenvolvimento mobile (React Native)
- ✅ Desenvolvimento backend (Node.js)
- ✅ Banco de dados SQL
- ✅ APIs REST
- ✅ Controle de versão (Git)
- ✅ Testes de software
- ✅ Metodologias ágeis

### 6.2 Comportamentais (Soft Skills)
- ✅ Trabalho em equipe
- ✅ Comunicação técnica
- ✅ Resolução de problemas
- ✅ Pensamento crítico
- ✅ Organização e planejamento
- ✅ Adaptabilidade
- ✅ Ética profissional

### 6.3 Profissionais
- ✅ Visão sistêmica de projetos
- ✅ Documentação técnica
- ✅ Boas práticas de código
- ✅ Segurança da informação
- ✅ Qualidade de software
- ✅ Gestão de tempo
- ✅ Atualização contínua

## 7. Recursos Didáticos

### 7.1 Materiais de Apoio
- 📚 PTDs de cada UC
- 📄 Esta documentação completa
- 🎨 Protótipos no Canva/Stitch
- 💻 Código-fonte comentado
- 📊 Diagramas técnicos
- 🎥 Vídeos de demonstração (opcional)

### 7.2 Ferramentas Utilizadas
- **Desenvolvimento**: VS Code, Node.js, Expo
- **Banco de Dados**: PostgreSQL/MySQL
- **Versionamento**: Git, GitHub
- **Testes**: Jest, TestLink, Mantis
- **Prototipação**: Canva, Stitch
- **Gestão**: Trello/Jira (Scrum/Kanban)

## 8. Orientações para Docentes

### 8.1 Preparação das Aulas
1. Revisar PTD da UC correspondente
2. Consultar esta documentação técnica
3. Preparar ambiente de desenvolvimento
4. Testar exemplos práticos previamente
5. Preparar materiais de apoio

### 8.2 Condução das Atividades
1. Contextualizar com o projeto MeetStranger
2. Demonstrar conceitos na prática
3. Orientar desenvolvimento hands-on
4. Circular pela sala auxiliando individualmente
5. Promover discussões e code review

### 8.3 Avaliação Contínua
1. Observar progresso individual e em grupo
2. Dar feedback constante
3. Identificar dificuldades precocemente
4. Ajustar ritmo conforme necessidade
5. Documentar evolução dos alunos

## 9. Orientações para Estudantes

### 9.1 Como Aproveitar o Projeto
1. Leia toda a documentação antes de começar
2. Siga a sequência das UCs
3. Não pule etapas
4. Documente seu código
5. Teste continuamente
6. Peça ajuda quando necessário
7. Colabore com colegas

### 9.2 Organização Pessoal
- 📅 Acompanhe o cronograma
- 💾 Faça commits frequentes
- 📝 Mantenha anotações
- 🔍 Pesquise além do conteúdo
- 🎯 Foque nos objetivos de cada UC

### 9.3 Portfólio Profissional
Este projeto pode ser usado como:
- ✅ Portfólio no GitHub
- ✅ Projeto para entrevistas
- ✅ Base para projetos futuros
- ✅ Demonstração de habilidades completas

---

**Documento:** Contexto Pedagógico  
**Versão:** 1.0  
**Data:** 2024  
**Alinhamento:** PTDs UC 01, 02 e 03
