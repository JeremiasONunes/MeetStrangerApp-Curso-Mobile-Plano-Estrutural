# 📐 Escopo do Projeto - MeetStranger

## 1. Definição do Escopo

### 1.1 Objetivo do Documento
Definir claramente o que está incluído e excluído do projeto MeetStranger MVP, estabelecendo limites e entregas esperadas.

### 1.2 Versão do Projeto
**MVP (Minimum Viable Product)** - Versão 1.0

## 2. Escopo do Produto

### 2.1 Visão Geral
Desenvolver um aplicativo mobile multiplataforma de chat anônimo P2P, organizado por tópicos de interesse, com foco em privacidade e simplicidade.

### 2.2 Objetivos do Produto
1. ✅ Conectar pessoas com interesses similares
2. ✅ Garantir privacidade e anonimato total
3. ✅ Proporcionar experiência de uso simples e intuitiva
4. ✅ Permitir conversas em tempo real
5. ✅ Funcionar em iOS e Android

## 3. Dentro do Escopo (MVP)

### 3.1 Funcionalidades Incluídas

#### ✅ Autenticação
- Cadastro de usuário (email + senha)
- Login de usuário
- Logout
- Validação de sessão
- Recuperação de senha (básica)

#### ✅ Seleção de Tópicos
- Exibição de 3 tópicos fixos:
  - 🎬 Filmes
  - 🎮 Jogos
  - 📺 Séries
- Seleção de tópico pelo usuário
- Indicação de usuários online (opcional)

#### ✅ Chat P2P
- Conexão 1-para-1 com outro usuário
- Envio de mensagens de texto
- Recebimento de mensagens em tempo real
- Indicador de "digitando..."
- Troca de parceiro ("Próximo")
- Sair da conversa
- Notificação de desconexão do parceiro

#### ✅ Interface Mobile
- Tela de boas-vindas
- Tela de login
- Tela de cadastro
- Tela principal (home)
- Tela de seleção de tópicos
- Tela de chat
- Tela "Sobre o app"
- Navegação fluida entre telas
- Design responsivo

#### ✅ Backend
- API REST completa
- Autenticação com JWT
- WebSocket para chat em tempo real
- Gerenciamento de sessões
- Validações de dados
- Tratamento de erros

#### ✅ Banco de Dados
- Modelagem ER
- Tabelas: users, topics, chat_sessions
- CRUD completo
- Integridade referencial
- Índices otimizados

#### ✅ Segurança
- HTTPS obrigatório
- Senhas com hash (bcrypt)
- Tokens JWT
- Validação de inputs
- Rate limiting básico
- Proteção contra ataques comuns

#### ✅ Qualidade
- Testes unitários (básicos)
- Testes de integração
- Testes funcionais
- Testes de usabilidade
- Documentação técnica completa

### 3.2 Plataformas Suportadas
- ✅ iOS 13+
- ✅ Android API 21+ (Android 5.0+)
- ✅ Emuladores/Simuladores

### 3.3 Tecnologias Utilizadas
- ✅ React Native + Expo
- ✅ TypeScript
- ✅ Node.js + Express
- ✅ PostgreSQL ou MySQL
- ✅ Socket.io
- ✅ JWT

### 3.4 Entregas Esperadas

| Entrega | Descrição | UC | Prazo |
|---------|-----------|-----|-------|
| Documentação de Requisitos | RF, RNF, Regras de Negócio | UC 01 | Semana 4 |
| Protótipos | Wireframes e mockups | UC 01 | Semana 4 |
| Modelagem de Dados | Diagrama ER, Scripts SQL | UC 02-2 | Semana 11 |
| API Backend | Endpoints REST + WebSocket | UC 02-3 | Semana 15 |
| Aplicativo Mobile | App completo iOS/Android | UC 02-4 | Semana 19 |
| Relatório de Testes | Plano e execução de testes | UC 03 | Semana 23 |
| Código-Fonte | Repositório Git completo | Todas | Semana 23 |
| Apresentação Final | Demo + documentação | Todas | Semana 24 |

## 4. Fora do Escopo (MVP)

### 4.1 Funcionalidades NÃO Incluídas

#### ❌ Comunicação Avançada
- Chamadas de voz
- Chamadas de vídeo
- Compartilhamento de imagens
- Compartilhamento de vídeos
- Compartilhamento de arquivos
- Emojis personalizados
- GIFs animados
- Stickers

#### ❌ Social Features
- Sistema de amizades
- Perfis de usuário
- Fotos de perfil
- Status/bio
- Lista de contatos
- Favoritos
- Bloqueio de usuários
- Denúncias

#### ❌ Histórico e Persistência
- Histórico de conversas
- Salvar conversas
- Busca em mensagens antigas
- Exportar conversas
- Backup de mensagens

#### ❌ Notificações
- Push notifications
- Notificações de nova mensagem
- Notificações de novo parceiro
- Badges de notificação

#### ❌ Gamificação
- Sistema de pontos
- Conquistas/badges
- Ranking de usuários
- Níveis de usuário

#### ❌ Monetização
- Anúncios
- Assinaturas premium
- Compras in-app
- Doações

#### ❌ Moderação
- Sistema de moderação automática
- Filtro de conteúdo impróprio (IA)
- Banimento de usuários
- Relatórios de abuso
- Moderadores humanos

#### ❌ Personalização
- Temas (dark mode completo)
- Customização de cores
- Tamanho de fonte ajustável
- Sons personalizados
- Wallpapers de chat

#### ❌ Recursos Avançados
- Tradução automática
- Transcrição de áudio
- Reconhecimento de voz
- Chatbots
- IA conversacional

#### ❌ Integrações
- Login social (Google, Facebook)
- Compartilhar em redes sociais
- Integração com outros apps
- APIs públicas

#### ❌ Analytics
- Dashboard de métricas
- Análise de comportamento
- Relatórios de uso
- Heatmaps

#### ❌ Plataformas Adicionais
- Versão web completa
- Aplicativo desktop
- Smartwatch
- TV

### 4.2 Tópicos Adicionais
- ❌ Mais de 3 tópicos no MVP
- ❌ Tópicos customizados por usuário
- ❌ Subtópicos
- ❌ Tags/hashtags

### 4.3 Recursos de Infraestrutura
- ❌ Deploy em produção (cloud)
- ❌ CDN
- ❌ Load balancer
- ❌ Auto-scaling
- ❌ Monitoramento avançado
- ❌ CI/CD pipeline completo

## 5. Restrições do Projeto

### 5.1 Restrições de Tempo
- **Duração Total**: 192 horas (24 semanas)
- **Distribuição**:
  - UC 01: 36h (4 semanas)
  - UC 02: 120h (15 semanas)
  - UC 03: 36h (4 semanas)
  - Buffer: 1 semana

### 5.2 Restrições de Recursos
- **Equipe**: Estudantes do curso (variável)
- **Infraestrutura**: Ambiente educacional
- **Orçamento**: R$ 0,00 (ferramentas gratuitas)
- **Hardware**: Computadores da instituição + dispositivos pessoais

### 5.3 Restrições Técnicas
- **Ferramentas**: Apenas gratuitas/open-source
- **Hospedagem**: Localhost ou free tier
- **Banco de Dados**: PostgreSQL ou MySQL (gratuito)
- **Ambiente**: Desenvolvimento apenas (não produção)

### 5.4 Restrições Pedagógicas
- Seguir cronograma das UCs
- Aplicar conceitos de todas as UCs
- Documentação obrigatória
- Testes obrigatórios
- Apresentação final obrigatória

## 6. Premissas do Projeto

### 6.1 Premissas Técnicas
- ✅ Estudantes têm conhecimento básico de programação
- ✅ Computadores com Windows 11 disponíveis
- ✅ Acesso à internet estável
- ✅ Dispositivos móveis para testes (próprios ou emuladores)
- ✅ Ferramentas de desenvolvimento instaladas

### 6.2 Premissas de Negócio
- ✅ Projeto é educacional (não comercial)
- ✅ Dados são fictícios/simulados
- ✅ Não há usuários reais no MVP
- ✅ Foco em aprendizado, não em produção

### 6.3 Premissas de Usuário
- ✅ Usuários têm smartphones modernos
- ✅ Usuários têm conexão à internet
- ✅ Usuários entendem conceito de chat anônimo
- ✅ Usuários aceitam termos de uso

## 7. Dependências

### 7.1 Dependências Internas
- UC 02 Parte 2 depende de UC 02 Parte 1
- UC 02 Parte 3 depende de UC 02 Parte 2
- UC 02 Parte 4 depende de UC 02 Parte 3
- UC 03 depende de todas as UC 02

### 7.2 Dependências Externas
- Disponibilidade de internet
- Funcionamento de serviços de terceiros (Expo, npm)
- Acesso a documentações online
- Disponibilidade de ferramentas gratuitas

### 7.3 Dependências de Conhecimento
- Conceitos de UC 01 para UC 02
- Lógica de programação para backend/frontend
- SQL para integração backend/banco
- React Native para desenvolvimento mobile

## 8. Critérios de Aceitação do Projeto

### 8.1 Critérios Funcionais
- ✅ Todas as funcionalidades do escopo implementadas
- ✅ Aplicativo funciona em iOS e Android
- ✅ Chat em tempo real operacional
- ✅ Autenticação segura funcionando
- ✅ Banco de dados integrado

### 8.2 Critérios de Qualidade
- ✅ Código limpo e organizado
- ✅ Documentação completa
- ✅ Testes executados e aprovados
- ✅ Sem bugs críticos
- ✅ Performance aceitável (conforme RNFs)

### 8.3 Critérios Pedagógicos
- ✅ Todos os conceitos das UCs aplicados
- ✅ Entregas dentro dos prazos
- ✅ Participação ativa dos estudantes
- ✅ Apresentação final realizada

### 8.4 Critérios de Documentação
- ✅ Requisitos documentados
- ✅ Arquitetura documentada
- ✅ Código comentado
- ✅ README atualizado
- ✅ Diagramas criados

## 9. Riscos e Mitigações

### 9.1 Riscos Técnicos

| Risco | Probabilidade | Impacto | Mitigação |
|-------|--------------|---------|-----------|
| Dificuldade com React Native | Alta | Alto | Tutoriais, documentação, suporte docente |
| Problemas de integração | Média | Alto | Testes incrementais, documentação de APIs |
| Performance ruim | Média | Médio | Otimizações, testes de performance |
| Bugs críticos | Média | Alto | Testes contínuos, code review |

### 9.2 Riscos de Projeto

| Risco | Probabilidade | Impacto | Mitigação |
|-------|--------------|---------|-----------|
| Atraso no cronograma | Média | Alto | Buffer de tempo, priorização |
| Escopo creep | Baixa | Médio | Escopo bem definido, controle rígido |
| Falta de recursos | Baixa | Médio | Ferramentas gratuitas, alternativas |
| Desmotivação da equipe | Média | Médio | Metodologias ativas, feedback constante |

### 9.3 Riscos Pedagógicos

| Risco | Probabilidade | Impacto | Mitigação |
|-------|--------------|---------|-----------|
| Dificuldade de aprendizado | Média | Alto | Suporte individualizado, materiais extras |
| Desnivelamento da turma | Alta | Médio | Atividades em grupo, peer learning |
| Falta de pré-requisitos | Baixa | Alto | Nivelamento inicial, revisões |

## 10. Plano de Comunicação

### 10.1 Stakeholders
- **Docente**: Jeremias O Nunes
- **Estudantes**: Turma Programador Mobile
- **Coordenação**: SENAC

### 10.2 Canais de Comunicação
- Aulas presenciais (principal)
- Email institucional
- Grupo de WhatsApp/Discord (opcional)
- GitHub (código e issues)

### 10.3 Frequência de Comunicação
- **Aulas**: 2-3x por semana
- **Feedback**: Contínuo durante aulas
- **Avaliações**: Ao final de cada UC
- **Apresentações**: Intermediárias e final

## 11. Cronograma Macro

| Fase | Período | Duração | Entregável Principal |
|------|---------|---------|---------------------|
| **UC 01** | Semanas 1-4 | 36h | Documentação + Protótipos |
| **UC 02-1** | Semanas 5-8 | 30h | Algoritmos + Lógica |
| **UC 02-2** | Semanas 9-11 | 30h | Banco de Dados |
| **UC 02-3** | Semanas 12-15 | 30h | Backend API |
| **UC 02-4** | Semanas 16-19 | 30h | Aplicativo Mobile |
| **UC 03** | Semanas 20-23 | 36h | Testes + Qualidade |
| **Apresentação** | Semana 24 | 4h | Demo Final |

## 12. Aprovações

### 12.1 Aprovação do Escopo
- [ ] Docente Responsável
- [ ] Coordenação do Curso
- [ ] Representantes dos Estudantes

### 12.2 Controle de Mudanças
Qualquer mudança no escopo deve:
1. Ser documentada
2. Ser aprovada pelo docente
3. Ser comunicada a todos os stakeholders
4. Ser avaliada quanto ao impacto no cronograma

### 12.3 Revisões do Escopo
- **Revisão 1**: Após UC 01 (ajustes de requisitos)
- **Revisão 2**: Após UC 02-2 (ajustes técnicos)
- **Revisão 3**: Após UC 03 (lições aprendidas)

---

**Documento:** Escopo do Projeto  
**Versão:** 1.0  
**Data:** 2024  
**Status:** ✅ Aprovado  
**Próxima Revisão:** Após UC 01
