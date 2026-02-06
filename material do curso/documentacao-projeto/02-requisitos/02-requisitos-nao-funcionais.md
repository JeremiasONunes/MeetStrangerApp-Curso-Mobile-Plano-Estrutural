# ⚙️ Requisitos Não Funcionais - MeetStranger

## 1. Introdução

### 1.1 Objetivo do Documento
Este documento especifica os requisitos não funcionais do sistema MeetStranger, definindo atributos de qualidade, desempenho, segurança e restrições técnicas.

### 1.2 Categorias
- **Desempenho** - Tempo de resposta e throughput
- **Segurança** - Proteção de dados e privacidade
- **Usabilidade** - Facilidade de uso
- **Confiabilidade** - Disponibilidade e recuperação
- **Manutenibilidade** - Facilidade de manutenção
- **Portabilidade** - Compatibilidade de plataformas
- **Escalabilidade** - Capacidade de crescimento

### 1.3 Convenções
- **RNF** = Requisito Não Funcional
- **Prioridade**: Alta, Média, Baixa
- **Mensurável**: Sim/Não

## 2. Requisitos de Desempenho

### RNF01 - Tempo de Resposta da API
**Categoria**: Desempenho  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, UC 03

**Descrição**: As requisições à API devem ser processadas rapidamente.

**Critérios Mensuráveis**:
- ✅ Requisições GET: < 500ms (95% dos casos)
- ✅ Requisições POST: < 1s (95% dos casos)
- ✅ Autenticação: < 800ms
- ✅ Conexão WebSocket: < 300ms

**Métrica de Teste**:
- Usar ferramentas de performance testing
- Medir tempo médio, mediano e percentil 95
- Testar com carga normal (10 usuários simultâneos)

**Justificativa**: Garantir experiência fluida e responsiva.

---

### RNF02 - Tempo de Carregamento de Telas
**Categoria**: Desempenho  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4, UC 03

**Descrição**: As telas do aplicativo devem carregar rapidamente.

**Critérios Mensuráveis**:
- ✅ Tela inicial: < 2s
- ✅ Transição entre telas: < 500ms
- ✅ Carregamento de lista de tópicos: < 1s
- ✅ Entrada na sala de chat: < 1.5s

**Métrica de Teste**:
- Medir com React Native Performance Monitor
- Testar em dispositivos de diferentes capacidades
- Considerar conexões 3G, 4G e WiFi

---

### RNF03 - Latência de Mensagens
**Categoria**: Desempenho  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4, UC 03

**Descrição**: Mensagens devem ser entregues em tempo real.

**Critérios Mensuráveis**:
- ✅ Latência de envio: < 200ms
- ✅ Latência de recebimento: < 300ms
- ✅ Latência total (envio + recebimento): < 500ms

**Métrica de Teste**:
- Timestamp de envio vs recebimento
- Testar em diferentes condições de rede
- Medir em ambiente real (não localhost)

---

### RNF04 - Capacidade de Usuários Simultâneos
**Categoria**: Desempenho/Escalabilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 03

**Descrição**: O sistema deve suportar múltiplos usuários simultâneos.

**Critérios Mensuráveis**:
- ✅ MVP: 50 usuários simultâneos
- ✅ Produção (futuro): 1000+ usuários simultâneos
- ✅ Degradação graceful acima da capacidade

**Métrica de Teste**:
- Testes de carga com JMeter ou Artillery
- Monitorar uso de CPU e memória
- Identificar gargalos

---

### RNF05 - Consumo de Recursos Mobile
**Categoria**: Desempenho  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 4, UC 03

**Descrição**: O aplicativo deve consumir recursos de forma eficiente.

**Critérios Mensuráveis**:
- ✅ Uso de memória: < 150MB
- ✅ Uso de CPU: < 30% em idle, < 60% em uso ativo
- ✅ Consumo de bateria: < 5% por hora de uso
- ✅ Uso de dados: < 1MB por 10 minutos de chat

**Métrica de Teste**:
- Profiling com React Native Debugger
- Monitorar em dispositivos reais
- Testar por períodos prolongados

---

## 3. Requisitos de Segurança

### RNF06 - Criptografia de Dados em Trânsito
**Categoria**: Segurança  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, UC 03

**Descrição**: Todos os dados transmitidos devem ser criptografados.

**Critérios Mensuráveis**:
- ✅ HTTPS obrigatório (TLS 1.2+)
- ✅ WebSocket Secure (WSS)
- ✅ Certificado SSL válido
- ✅ Sem comunicação em texto plano

**Métrica de Teste**:
- Verificar certificado SSL
- Testar com ferramentas de análise de tráfego
- Validar que HTTP redireciona para HTTPS

**Justificativa**: Proteger dados durante transmissão.

---

### RNF07 - Armazenamento Seguro de Senhas
**Categoria**: Segurança  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3

**Descrição**: Senhas devem ser armazenadas com segurança.

**Critérios Mensuráveis**:
- ✅ Hash com bcrypt (cost factor ≥ 10)
- ✅ Salt único por senha
- ✅ Senhas nunca armazenadas em texto plano
- ✅ Senhas nunca retornadas em APIs

**Métrica de Teste**:
- Inspecionar banco de dados
- Verificar código de hash
- Testar que API não retorna senha

---

### RNF08 - Autenticação Segura
**Categoria**: Segurança  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3

**Descrição**: Sistema de autenticação deve ser robusto.

**Critérios Mensuráveis**:
- ✅ Tokens JWT com expiração (24h)
- ✅ Tokens assinados com chave secreta forte
- ✅ Refresh token implementado (futuro)
- ✅ Proteção contra brute force (rate limiting)

**Métrica de Teste**:
- Tentar acessar rotas sem token
- Tentar usar token expirado
- Tentar múltiplos logins incorretos

---

### RNF09 - Proteção contra Ataques Comuns
**Categoria**: Segurança  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, UC 03

**Descrição**: Sistema deve estar protegido contra ataques conhecidos.

**Critérios Mensuráveis**:
- ✅ Proteção contra SQL Injection (usar ORM/prepared statements)
- ✅ Proteção contra XSS (sanitização de inputs)
- ✅ Proteção contra CSRF (tokens CSRF)
- ✅ Rate limiting em APIs (100 req/min por IP)
- ✅ Validação de inputs no backend

**Métrica de Teste**:
- Testes de penetração básicos
- Tentar injetar SQL malicioso
- Tentar scripts XSS
- Testar rate limiting

---

### RNF10 - Privacidade de Dados
**Categoria**: Segurança/Privacidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 01, UC 02, UC 03

**Descrição**: Sistema deve garantir privacidade total dos usuários.

**Critérios Mensuráveis**:
- ✅ Apenas email armazenado (necessário para login)
- ✅ Nenhum dado pessoal adicional coletado
- ✅ Mensagens não persistidas no banco
- ✅ Histórico de conversas não armazenado
- ✅ IPs não registrados
- ✅ Logs anonimizados

**Métrica de Teste**:
- Auditar banco de dados
- Verificar logs do servidor
- Confirmar que mensagens não são salvas

**Justificativa**: Garantir anonimato prometido.

---

## 4. Requisitos de Usabilidade

### RNF11 - Facilidade de Uso
**Categoria**: Usabilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4, UC 03

**Descrição**: Interface deve ser intuitiva e fácil de usar.

**Critérios Mensuráveis**:
- ✅ Novo usuário consegue usar sem tutorial
- ✅ Máximo 3 cliques para qualquer ação principal
- ✅ Feedback visual em todas as ações
- ✅ Mensagens de erro claras e acionáveis

**Métrica de Teste**:
- Testes de usabilidade com usuários reais
- Medir tempo para completar tarefas
- Taxa de sucesso em tarefas principais

---

### RNF12 - Acessibilidade
**Categoria**: Usabilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 4

**Descrição**: Aplicativo deve ser acessível a diferentes usuários.

**Critérios Mensuráveis**:
- ✅ Contraste de cores adequado (WCAG AA)
- ✅ Tamanho de fonte legível (mínimo 14px)
- ✅ Áreas de toque adequadas (mínimo 44x44px)
- ✅ Suporte a leitores de tela (básico)

**Métrica de Teste**:
- Verificar contraste com ferramentas
- Testar com diferentes tamanhos de fonte
- Testar com leitor de tela

---

### RNF13 - Consistência Visual
**Categoria**: Usabilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 4

**Descrição**: Interface deve ser consistente em todo o app.

**Critérios Mensuráveis**:
- ✅ Design System implementado
- ✅ Cores, fontes e espaçamentos padronizados
- ✅ Componentes reutilizáveis
- ✅ Padrões de interação consistentes

**Métrica de Teste**:
- Revisão visual de todas as telas
- Verificar uso do Design System
- Validar componentes reutilizados

---

### RNF14 - Internacionalização (Futuro)
**Categoria**: Usabilidade  
**Prioridade**: Baixa  
**UC Relacionada**: Futuro

**Descrição**: Preparar app para múltiplos idiomas.

**Critérios Mensuráveis**:
- ✅ Textos externalizados (não hardcoded)
- ✅ Suporte a PT-BR (MVP)
- ✅ Estrutura para adicionar EN, ES (futuro)

---

## 5. Requisitos de Confiabilidade

### RNF15 - Disponibilidade do Sistema
**Categoria**: Confiabilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 03

**Descrição**: Sistema deve estar disponível a maior parte do tempo.

**Critérios Mensuráveis**:
- ✅ MVP: 95% de uptime (permitir ~36h downtime/mês)
- ✅ Produção (futuro): 99% de uptime
- ✅ Manutenções programadas fora de horário de pico

**Métrica de Teste**:
- Monitoramento com uptime monitoring
- Logs de disponibilidade
- Alertas de downtime

---

### RNF16 - Recuperação de Falhas
**Categoria**: Confiabilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 3, 4, UC 03

**Descrição**: Sistema deve se recuperar graciosamente de falhas.

**Critérios Mensuráveis**:
- ✅ Reconexão automática de WebSocket (até 3 tentativas)
- ✅ Retry de requisições falhadas (até 2 tentativas)
- ✅ Mensagens de erro amigáveis
- ✅ Estado do app preservado após crash

**Métrica de Teste**:
- Simular perda de conexão
- Simular falha de servidor
- Verificar comportamento de retry

---

### RNF17 - Tratamento de Erros
**Categoria**: Confiabilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4, UC 03

**Descrição**: Erros devem ser tratados adequadamente.

**Critérios Mensuráveis**:
- ✅ Try-catch em todas as operações críticas
- ✅ Logs de erro estruturados
- ✅ Mensagens de erro para usuário (não técnicas)
- ✅ Fallbacks para funcionalidades críticas

**Métrica de Teste**:
- Forçar erros em diferentes cenários
- Verificar logs
- Validar mensagens ao usuário

---

### RNF18 - Backup e Recuperação de Dados
**Categoria**: Confiabilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 2

**Descrição**: Dados críticos devem ter backup.

**Critérios Mensuráveis**:
- ✅ Backup diário do banco de dados
- ✅ Retenção de 7 dias de backups
- ✅ Procedimento de restore documentado
- ✅ Teste de restore mensal

**Métrica de Teste**:
- Executar restore de backup
- Verificar integridade dos dados
- Medir tempo de recuperação

---

## 6. Requisitos de Manutenibilidade

### RNF19 - Qualidade de Código
**Categoria**: Manutenibilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 (todas as partes)

**Descrição**: Código deve ser limpo e bem organizado.

**Critérios Mensuráveis**:
- ✅ Seguir padrões de código (ESLint)
- ✅ Funções com responsabilidade única
- ✅ Máximo 200 linhas por arquivo
- ✅ Nomes descritivos de variáveis/funções
- ✅ Sem código duplicado (DRY)

**Métrica de Teste**:
- Análise estática com ESLint
- Code review
- Métricas de complexidade ciclomática

---

### RNF20 - Documentação de Código
**Categoria**: Manutenibilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 02 (todas as partes)

**Descrição**: Código deve ser documentado adequadamente.

**Critérios Mensuráveis**:
- ✅ Comentários em funções complexas
- ✅ JSDoc em funções públicas
- ✅ README atualizado
- ✅ Documentação de APIs (Swagger/Postman)

**Métrica de Teste**:
- Revisão de documentação
- Verificar cobertura de comentários
- Validar README está atualizado

---

### RNF21 - Modularidade
**Categoria**: Manutenibilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4

**Descrição**: Sistema deve ser modular e desacoplado.

**Critérios Mensuráveis**:
- ✅ Separação clara de camadas (MVC/Clean Architecture)
- ✅ Componentes reutilizáveis
- ✅ Baixo acoplamento entre módulos
- ✅ Alta coesão dentro de módulos

**Métrica de Teste**:
- Análise de dependências
- Verificar estrutura de pastas
- Testar isolamento de módulos

---

### RNF22 - Versionamento
**Categoria**: Manutenibilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 (todas as partes)

**Descrição**: Código deve ser versionado adequadamente.

**Critérios Mensuráveis**:
- ✅ Git para controle de versão
- ✅ Commits descritivos
- ✅ Branches para features
- ✅ Tags para releases
- ✅ Histórico limpo (sem commits desnecessários)

**Métrica de Teste**:
- Revisar histórico do Git
- Verificar mensagens de commit
- Validar estratégia de branching

---

## 7. Requisitos de Portabilidade

### RNF23 - Compatibilidade de Plataformas
**Categoria**: Portabilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4, UC 03

**Descrição**: App deve funcionar em múltiplas plataformas.

**Critérios Mensuráveis**:
- ✅ iOS 13+
- ✅ Android API 21+ (Android 5.0+)
- ✅ Funcionalidade idêntica em ambas plataformas
- ✅ UI adaptada a guidelines de cada plataforma

**Métrica de Teste**:
- Testar em dispositivos iOS reais
- Testar em dispositivos Android reais
- Verificar funcionalidades em ambos

---

### RNF24 - Compatibilidade de Dispositivos
**Categoria**: Portabilidade  
**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4, UC 03

**Descrição**: App deve funcionar em diferentes dispositivos.

**Critérios Mensuráveis**:
- ✅ Smartphones (5" a 7")
- ✅ Tablets (opcional)
- ✅ Diferentes resoluções
- ✅ Diferentes densidades de tela

**Métrica de Teste**:
- Testar em pelo menos 5 dispositivos diferentes
- Testar em emuladores de diferentes tamanhos
- Verificar layout responsivo

---

### RNF25 - Compatibilidade de Rede
**Categoria**: Portabilidade  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 3, 4, UC 03

**Descrição**: App deve funcionar em diferentes condições de rede.

**Critérios Mensuráveis**:
- ✅ Funcional em WiFi
- ✅ Funcional em 4G
- ✅ Funcional em 3G (degradado)
- ✅ Modo offline para telas estáticas

**Métrica de Teste**:
- Testar em diferentes tipos de conexão
- Simular conexões lentas
- Verificar comportamento offline

---

## 8. Requisitos de Escalabilidade

### RNF26 - Escalabilidade Horizontal
**Categoria**: Escalabilidade  
**Prioridade**: Baixa (futuro)  
**UC Relacionada**: Futuro

**Descrição**: Sistema deve poder escalar horizontalmente.

**Critérios Mensuráveis**:
- ✅ Backend stateless
- ✅ Sessões em cache distribuído (Redis)
- ✅ Load balancer preparado
- ✅ Banco de dados com replicação

**Justificativa**: Preparar para crescimento futuro.

---

### RNF27 - Otimização de Banco de Dados
**Categoria**: Escalabilidade/Desempenho  
**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 2, UC 03

**Descrição**: Banco de dados deve ser otimizado.

**Critérios Mensuráveis**:
- ✅ Índices em colunas de busca frequente
- ✅ Queries otimizadas (sem N+1)
- ✅ Connection pooling configurado
- ✅ Limpeza de dados antigos automatizada

**Métrica de Teste**:
- Analisar planos de execução de queries
- Medir tempo de queries
- Monitorar uso de índices

---

## 9. Requisitos de Conformidade

### RNF28 - LGPD (Lei Geral de Proteção de Dados)
**Categoria**: Conformidade Legal  
**Prioridade**: Alta  
**UC Relacionada**: UC 01, UC 03

**Descrição**: Sistema deve estar em conformidade com LGPD.

**Critérios Mensuráveis**:
- ✅ Coleta mínima de dados
- ✅ Consentimento explícito (termos de uso)
- ✅ Direito de exclusão de conta
- ✅ Política de privacidade clara
- ✅ Dados armazenados no Brasil (futuro)

**Métrica de Teste**:
- Auditoria de conformidade
- Verificar política de privacidade
- Testar exclusão de conta

---

### RNF29 - Termos de Uso
**Categoria**: Conformidade Legal  
**Prioridade**: Alta  
**UC Relacionada**: UC 01

**Descrição**: Sistema deve ter termos de uso claros.

**Critérios Mensuráveis**:
- ✅ Termos de uso acessíveis
- ✅ Aceitação obrigatória no cadastro
- ✅ Regras de conduta definidas
- ✅ Consequências de violação claras

---

## 10. Matriz de Rastreabilidade

| RNF | Categoria | Prioridade | UC | Mensurável |
|-----|-----------|-----------|-----|-----------|
| RNF01 | Desempenho | Alta | 02-3, 03 | Sim |
| RNF02 | Desempenho | Alta | 02-4, 03 | Sim |
| RNF03 | Desempenho | Alta | 02-3, 02-4, 03 | Sim |
| RNF04 | Desempenho | Média | 03 | Sim |
| RNF05 | Desempenho | Média | 02-4, 03 | Sim |
| RNF06 | Segurança | Alta | 02-3, 03 | Sim |
| RNF07 | Segurança | Alta | 02-3 | Sim |
| RNF08 | Segurança | Alta | 02-3 | Sim |
| RNF09 | Segurança | Alta | 02-3, 03 | Sim |
| RNF10 | Segurança | Alta | 01, 02, 03 | Sim |
| RNF11 | Usabilidade | Alta | 02-4, 03 | Parcial |
| RNF12 | Usabilidade | Média | 02-4 | Sim |
| RNF13 | Usabilidade | Média | 02-4 | Parcial |
| RNF14 | Usabilidade | Baixa | Futuro | Sim |
| RNF15 | Confiabilidade | Alta | 03 | Sim |
| RNF16 | Confiabilidade | Média | 02-3, 02-4, 03 | Sim |
| RNF17 | Confiabilidade | Alta | 02-3, 02-4, 03 | Sim |
| RNF18 | Confiabilidade | Média | 02-2 | Sim |
| RNF19 | Manutenibilidade | Alta | 02 (todas) | Sim |
| RNF20 | Manutenibilidade | Média | 02 (todas) | Parcial |
| RNF21 | Manutenibilidade | Alta | 02-3, 02-4 | Parcial |
| RNF22 | Manutenibilidade | Alta | 02 (todas) | Sim |
| RNF23 | Portabilidade | Alta | 02-4, 03 | Sim |
| RNF24 | Portabilidade | Alta | 02-4, 03 | Sim |
| RNF25 | Portabilidade | Média | 02-3, 02-4, 03 | Sim |
| RNF26 | Escalabilidade | Baixa | Futuro | Sim |
| RNF27 | Escalabilidade | Média | 02-2, 03 | Sim |
| RNF28 | Conformidade | Alta | 01, 03 | Parcial |
| RNF29 | Conformidade | Alta | 01 | Sim |

## 11. Resumo Quantitativo

- **Total de Requisitos Não Funcionais**: 29
- **Prioridade Alta**: 19 (66%)
- **Prioridade Média**: 8 (27%)
- **Prioridade Baixa**: 2 (7%)

### Por Categoria
- **Desempenho**: 5 requisitos
- **Segurança**: 5 requisitos
- **Usabilidade**: 4 requisitos
- **Confiabilidade**: 4 requisitos
- **Manutenibilidade**: 4 requisitos
- **Portabilidade**: 3 requisitos
- **Escalabilidade**: 2 requisitos
- **Conformidade**: 2 requisitos

---

**Documento:** Requisitos Não Funcionais  
**Versão:** 1.0  
**Data:** 2024  
**Próxima Revisão:** Após UC 03  
**Aprovação:** Pendente
