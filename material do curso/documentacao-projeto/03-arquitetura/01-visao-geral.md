# 🏗️ Arquitetura do Sistema - Visão Geral

## 1. Introdução

### 1.1 Objetivo
Este documento apresenta a arquitetura completa do sistema MeetStranger, descrevendo componentes, tecnologias, integrações e fluxos de dados.

### 1.2 Escopo
Arquitetura do MVP (Minimum Viable Product) do MeetStranger.

## 2. Visão Geral da Arquitetura

### 2.1 Diagrama de Alto Nível

```
┌─────────────────────────────────────────────────────────────┐
│                     CAMADA DE APRESENTAÇÃO                   │
│                                                              │
│  ┌──────────────────┐              ┌──────────────────┐    │
│  │   iOS App        │              │   Android App    │    │
│  │  (React Native)  │              │  (React Native)  │    │
│  └────────┬─────────┘              └────────┬─────────┘    │
│           │                                  │               │
│           └──────────────┬───────────────────┘               │
└──────────────────────────┼─────────────────────────────────┘
                           │
                    HTTPS / WSS
                           │
┌──────────────────────────┼─────────────────────────────────┐
│                          ▼                                   │
│                  CAMADA DE APLICAÇÃO                        │
│                                                              │
│  ┌────────────────────────────────────────────────┐        │
│  │           API REST + WebSocket Server          │        │
│  │              (Node.js + Express)               │        │
│  │                                                 │        │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐    │        │
│  │  │  Auth    │  │   Chat   │  │  Topics  │    │        │
│  │  │ Service  │  │ Service  │  │ Service  │    │        │
│  │  └──────────┘  └──────────┘  └──────────┘    │        │
│  └────────────────────┬───────────────────────────┘        │
└───────────────────────┼────────────────────────────────────┘
                        │
                     SQL / ORM
                        │
┌───────────────────────┼────────────────────────────────────┐
│                       ▼                                     │
│                 CAMADA DE DADOS                            │
│                                                             │
│  ┌─────────────────────────────────────────────┐          │
│  │      Banco de Dados Relacional              │          │
│  │        (PostgreSQL / MySQL)                 │          │
│  │                                              │          │
│  │  ┌────────┐  ┌────────┐  ┌──────────────┐ │          │
│  │  │ users  │  │ topics │  │chat_sessions │ │          │
│  │  └────────┘  └────────┘  └──────────────┘ │          │
│  └─────────────────────────────────────────────┘          │
└────────────────────────────────────────────────────────────┘
```

### 2.2 Arquitetura em Camadas

#### Camada 1: Apresentação (Frontend Mobile)
- **Tecnologia**: React Native + Expo
- **Responsabilidade**: Interface do usuário, navegação, experiência
- **Comunicação**: HTTP/HTTPS para REST, WSS para WebSocket

#### Camada 2: Aplicação (Backend)
- **Tecnologia**: Node.js + Express + Socket.io
- **Responsabilidade**: Lógica de negócio, autenticação, gerenciamento de chat
- **Comunicação**: SQL para banco de dados

#### Camada 3: Dados (Banco de Dados)
- **Tecnologia**: PostgreSQL ou MySQL
- **Responsabilidade**: Persistência de dados, integridade referencial
- **Comunicação**: Queries SQL via ORM

## 3. Componentes Principais

### 3.1 Frontend Mobile (React Native)

#### Estrutura de Pastas
```
primeiroApp/
├── app/                    # Telas (Expo Router)
│   ├── auth/              # Autenticação
│   ├── chat/              # Chat
│   ├── home/              # Home
│   └── about/             # Sobre
├── design-system/         # Componentes reutilizáveis
│   ├── components/        # Button, Input, Card, etc.
│   ├── tokens/            # Cores, tipografia, espaçamento
│   └── animations/        # Animações
├── styles/                # Estilos separados
│   └── screens/           # Estilos por tela
├── hooks/                 # Custom hooks
│   ├── useAuth.tsx        # Autenticação
│   └── useChat.tsx        # Chat
└── constants/             # Constantes e configurações
```

#### Componentes Principais
1. **Telas**:
   - Welcome, Login, Register
   - Home, Chat Select, Chat Room
   - About

2. **Componentes Reutilizáveis**:
   - Button (4 variantes)
   - Input (com validação)
   - Card (3 variantes)
   - ChatBubble

3. **Hooks Customizados**:
   - useAuth (gerenciamento de autenticação)
   - useChat (gerenciamento de chat)

4. **Navegação**:
   - Expo Router (file-based routing)
   - Stack navigation

### 3.2 Backend (Node.js + Express)

#### Estrutura de Pastas
```
backend/
├── src/
│   ├── controllers/       # Controladores (rotas)
│   │   ├── authController.js
│   │   ├── chatController.js
│   │   └── topicController.js
│   ├── services/          # Lógica de negócio
│   │   ├── authService.js
│   │   ├── chatService.js
│   │   └── topicService.js
│   ├── models/            # Modelos de dados (ORM)
│   │   ├── User.js
│   │   ├── Topic.js
│   │   └── ChatSession.js
│   ├── middlewares/       # Middlewares
│   │   ├── auth.js
│   │   ├── validation.js
│   │   └── errorHandler.js
│   ├── routes/            # Definição de rotas
│   │   ├── auth.js
│   │   ├── chat.js
│   │   └── topics.js
│   ├── config/            # Configurações
│   │   ├── database.js
│   │   └── jwt.js
│   ├── utils/             # Utilitários
│   │   ├── logger.js
│   │   └── validators.js
│   └── socket/            # WebSocket
│       └── chatSocket.js
├── tests/                 # Testes
└── server.js              # Entry point
```

#### Módulos Principais

1. **Autenticação**:
   - Registro de usuário
   - Login com JWT
   - Validação de token
   - Middleware de autenticação

2. **Gerenciamento de Chat**:
   - Conexão de usuários
   - Envio/recebimento de mensagens
   - Troca de parceiros
   - Desconexão

3. **Tópicos**:
   - Listagem de tópicos
   - Gerenciamento de usuários por tópico

4. **WebSocket**:
   - Conexões em tempo real
   - Broadcast de mensagens
   - Gerenciamento de salas

### 3.3 Banco de Dados

#### Modelo Entidade-Relacionamento

```
┌─────────────────┐
│     users       │
├─────────────────┤
│ id (PK)         │
│ email (UNIQUE)  │
│ password_hash   │
│ created_at      │
│ updated_at      │
└────────┬────────┘
         │
         │ 1:N
         │
┌────────▼────────────┐
│  chat_sessions      │
├─────────────────────┤
│ id (PK)             │
│ user1_id (FK)       │
│ user2_id (FK)       │
│ topic_id (FK)       │
│ started_at          │
│ ended_at            │
│ status              │
└────────┬────────────┘
         │
         │ N:1
         │
┌────────▼────────┐
│     topics      │
├─────────────────┤
│ id (PK)         │
│ name            │
│ icon            │
│ description     │
└─────────────────┘
```

#### Tabelas Principais

1. **users**
   - Armazena dados de autenticação
   - Senha com hash bcrypt
   - Timestamps de criação/atualização

2. **topics**
   - Tópicos de conversa (Filmes, Jogos, Séries)
   - Dados estáticos (seed)

3. **chat_sessions**
   - Sessões de chat ativas
   - Relaciona 2 usuários e 1 tópico
   - Status: active, ended

4. **messages** (opcional - não persistido no MVP)
   - Apenas em memória durante sessão ativa
   - Não armazenado no banco

## 4. Fluxos de Dados

### 4.1 Fluxo de Autenticação

```
┌─────────┐         ┌─────────┐         ┌──────────┐
│  Mobile │         │   API   │         │    DB    │
└────┬────┘         └────┬────┘         └────┬─────┘
     │                   │                    │
     │ POST /register    │                    │
     ├──────────────────>│                    │
     │                   │ INSERT user        │
     │                   ├───────────────────>│
     │                   │                    │
     │                   │<───────────────────┤
     │   201 Created     │                    │
     │<──────────────────┤                    │
     │                   │                    │
     │ POST /login       │                    │
     ├──────────────────>│                    │
     │                   │ SELECT user        │
     │                   ├───────────────────>│
     │                   │                    │
     │                   │<───────────────────┤
     │                   │ Validate password  │
     │                   │ Generate JWT       │
     │   200 + token     │                    │
     │<──────────────────┤                    │
     │                   │                    │
```

### 4.2 Fluxo de Chat

```
┌─────────┐    ┌─────────┐    ┌──────────┐    ┌─────────┐
│ User A  │    │   API   │    │  Socket  │    │ User B  │
└────┬────┘    └────┬────┘    └────┬─────┘    └────┬────┘
     │              │              │               │
     │ Select Topic │              │               │
     ├─────────────>│              │               │
     │              │ Find Partner │               │
     │              ├─────────────>│               │
     │              │              │ Match Found   │
     │              │              ├──────────────>│
     │              │<─────────────┤               │
     │ Connect WS   │              │               │
     ├──────────────┼─────────────>│               │
     │              │              │<──────────────┤
     │              │              │  Connect WS   │
     │              │              │               │
     │ Send Message │              │               │
     ├──────────────┼─────────────>│               │
     │              │              │ Broadcast     │
     │              │              ├──────────────>│
     │              │              │               │
```

### 4.3 Fluxo de Seleção de Tópico

```
┌─────────┐         ┌─────────┐         ┌──────────┐
│  Mobile │         │   API   │         │    DB    │
└────┬────┘         └────┬────┘         └────┬─────┘
     │                   │                    │
     │ GET /topics       │                    │
     ├──────────────────>│                    │
     │                   │ SELECT topics      │
     │                   ├───────────────────>│
     │                   │                    │
     │                   │<───────────────────┤
     │   200 + topics    │                    │
     │<──────────────────┤                    │
     │                   │                    │
     │ POST /chat/connect│                    │
     │ {topicId: 1}      │                    │
     ├──────────────────>│                    │
     │                   │ Find available user│
     │                   │ Create session     │
     │                   ├───────────────────>│
     │                   │                    │
     │   200 + sessionId │                    │
     │<──────────────────┤                    │
     │                   │                    │
```

## 5. Tecnologias e Ferramentas

### 5.1 Frontend Mobile

| Tecnologia | Versão | Propósito |
|-----------|--------|-----------|
| React Native | Latest | Framework mobile |
| Expo | SDK 54 | Plataforma de desenvolvimento |
| TypeScript | 5.x | Tipagem estática |
| Expo Router | Latest | Navegação |
| Axios | Latest | Cliente HTTP |
| Socket.io Client | Latest | WebSocket |
| AsyncStorage | Latest | Armazenamento local |

### 5.2 Backend

| Tecnologia | Versão | Propósito |
|-----------|--------|-----------|
| Node.js | 18+ | Runtime JavaScript |
| Express | 4.x | Framework web |
| Socket.io | 4.x | WebSocket |
| JWT | Latest | Autenticação |
| bcrypt | Latest | Hash de senhas |
| Sequelize/Prisma | Latest | ORM |
| dotenv | Latest | Variáveis de ambiente |
| cors | Latest | CORS |
| helmet | Latest | Segurança |

### 5.3 Banco de Dados

| Tecnologia | Versão | Propósito |
|-----------|--------|-----------|
| PostgreSQL | 14+ | Banco relacional (opção 1) |
| MySQL | 8+ | Banco relacional (opção 2) |

### 5.4 Desenvolvimento e Testes

| Ferramenta | Propósito |
|-----------|-----------|
| VS Code | IDE |
| Git | Controle de versão |
| GitHub | Repositório |
| Postman | Testes de API |
| Jest | Testes unitários |
| TestLink | Gerenciamento de testes |
| Mantis | Rastreamento de bugs |
| Expo Go | Testes mobile |

## 6. Segurança

### 6.1 Camadas de Segurança

```
┌─────────────────────────────────────────┐
│  1. Transporte (HTTPS/WSS)              │
│     - TLS 1.2+                          │
│     - Certificado SSL                   │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│  2. Autenticação (JWT)                  │
│     - Tokens assinados                  │
│     - Expiração 24h                     │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│  3. Autorização (Middleware)            │
│     - Validação de token                │
│     - Verificação de permissões         │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│  4. Dados (Criptografia)                │
│     - Senhas com bcrypt                 │
│     - Dados sensíveis protegidos        │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│  5. Aplicação (Validação)               │
│     - Input validation                  │
│     - Sanitização                       │
│     - Rate limiting                     │
└─────────────────────────────────────────┘
```

### 6.2 Medidas de Segurança Implementadas

1. **Transporte Seguro**
   - HTTPS obrigatório
   - WebSocket Secure (WSS)

2. **Autenticação**
   - JWT com expiração
   - Senhas com hash bcrypt (cost 10+)

3. **Proteção de Dados**
   - Validação de inputs
   - Sanitização de dados
   - Prepared statements (SQL Injection)

4. **Rate Limiting**
   - 100 requisições/minuto por IP
   - Proteção contra brute force

5. **Privacidade**
   - Coleta mínima de dados
   - Mensagens não persistidas
   - Anonimato garantido

## 7. Escalabilidade e Performance

### 7.1 Estratégias de Performance

1. **Frontend**
   - Lazy loading de componentes
   - Memoização de componentes pesados
   - Otimização de re-renders
   - Imagens otimizadas

2. **Backend**
   - Connection pooling
   - Caching (futuro: Redis)
   - Queries otimizadas
   - Índices no banco

3. **Banco de Dados**
   - Índices em colunas de busca
   - Normalização adequada
   - Limpeza de dados antigos

### 7.2 Preparação para Escalabilidade (Futuro)

```
┌──────────────────────────────────────────┐
│         Load Balancer (Nginx)            │
└────────────┬─────────────────────────────┘
             │
      ┌──────┴──────┐
      │             │
┌─────▼────┐  ┌────▼─────┐
│ Server 1 │  │ Server 2 │  (Horizontal Scaling)
└─────┬────┘  └────┬─────┘
      │             │
      └──────┬──────┘
             │
      ┌──────▼──────┐
      │    Redis    │  (Session Store)
      └──────┬──────┘
             │
      ┌──────▼──────┐
      │  Database   │  (Master-Slave Replication)
      └─────────────┘
```

## 8. Monitoramento e Logs

### 8.1 Logs (MVP)
- Console logs estruturados
- Logs de erro
- Logs de acesso

### 8.2 Monitoramento (Futuro)
- Uptime monitoring
- Performance monitoring
- Error tracking (Sentry)
- Analytics

## 9. Deployment (Futuro)

### 9.1 Ambientes

| Ambiente | Propósito | URL |
|----------|-----------|-----|
| Development | Desenvolvimento local | localhost |
| Staging | Testes (futuro) | TBD |
| Production | Produção (futuro) | TBD |

### 9.2 CI/CD (Futuro)
- GitHub Actions
- Testes automatizados
- Deploy automático
- Rollback automático

## 10. Documentação Técnica

### 10.1 Documentos Relacionados
- [Requisitos Funcionais](../02-requisitos/01-requisitos-funcionais.md)
- [Requisitos Não Funcionais](../02-requisitos/02-requisitos-nao-funcionais.md)
- [Modelo de Dados](./04-banco-dados.md)
- [API Documentation](./03-backend-api.md)

### 10.2 Diagramas
- [Diagrama de Casos de Uso](../04-diagramas/01-diagrama-casos-uso.md)
- [Diagrama de Classes](../04-diagramas/02-diagrama-classes.md)
- [Modelo ER](../04-diagramas/03-modelo-entidade-relacionamento.md)

---

**Documento:** Arquitetura do Sistema - Visão Geral  
**Versão:** 1.0  
**Data:** 2024  
**Arquiteto:** Equipe MeetStranger  
**Aprovação:** Pendente
