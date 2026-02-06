# 📋 Requisitos Funcionais - MeetStranger

## 1. Introdução

### 1.1 Objetivo do Documento
Este documento especifica todos os requisitos funcionais do sistema MeetStranger, descrevendo o que o sistema deve fazer para atender às necessidades dos usuários.

### 1.2 Escopo
Requisitos funcionais para o MVP (Minimum Viable Product) do aplicativo mobile MeetStranger.

### 1.3 Convenções
- **RF** = Requisito Funcional
- **Prioridade**: Alta (essencial), Média (importante), Baixa (desejável)
- **Status**: Planejado, Em Desenvolvimento, Implementado, Testado

## 2. Módulo de Autenticação

### RF01 - Cadastro de Usuário
**Descrição**: O sistema deve permitir que novos usuários criem uma conta.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4

**Critérios de Aceitação**:
- ✅ Usuário informa email e senha
- ✅ Email deve ser válido (formato correto)
- ✅ Senha deve ter no mínimo 6 caracteres
- ✅ Sistema valida se email já está cadastrado
- ✅ Sistema criptografa a senha antes de armazenar
- ✅ Sistema retorna confirmação de cadastro bem-sucedido
- ✅ Sistema redireciona para tela de login após cadastro

**Regras de Negócio**:
- RN01: Email deve ser único no sistema
- RN02: Senha deve ser armazenada com hash (bcrypt)
- RN03: Não coletar dados pessoais além de email

**Fluxo Principal**:
1. Usuário acessa tela de cadastro
2. Usuário preenche email e senha
3. Usuário confirma senha
4. Sistema valida dados
5. Sistema cria conta
6. Sistema exibe mensagem de sucesso
7. Sistema redireciona para login

**Fluxos Alternativos**:
- FA01: Email já cadastrado → Exibir erro
- FA02: Senhas não conferem → Exibir erro
- FA03: Email inválido → Exibir erro
- FA04: Senha muito curta → Exibir erro

---

### RF02 - Login de Usuário
**Descrição**: O sistema deve permitir que usuários cadastrados façam login.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4

**Critérios de Aceitação**:
- ✅ Usuário informa email e senha
- ✅ Sistema valida credenciais
- ✅ Sistema gera token JWT
- ✅ Sistema armazena token localmente
- ✅ Sistema redireciona para tela principal
- ✅ Sessão permanece ativa até logout

**Regras de Negócio**:
- RN04: Token JWT expira em 24 horas
- RN05: Máximo 3 tentativas de login incorretas
- RN06: Após 3 tentativas, bloquear por 15 minutos

**Fluxo Principal**:
1. Usuário acessa tela de login
2. Usuário preenche email e senha
3. Sistema valida credenciais
4. Sistema gera token JWT
5. Sistema armazena token
6. Sistema redireciona para home

**Fluxos Alternativos**:
- FA05: Credenciais inválidas → Exibir erro
- FA06: Conta bloqueada → Exibir mensagem de bloqueio
- FA07: Erro de conexão → Exibir erro de rede

---

### RF03 - Logout de Usuário
**Descrição**: O sistema deve permitir que usuários façam logout.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Usuário clica em botão de logout
- ✅ Sistema remove token local
- ✅ Sistema desconecta de chat ativo (se houver)
- ✅ Sistema redireciona para tela de boas-vindas

**Fluxo Principal**:
1. Usuário clica em "Sair"
2. Sistema confirma ação
3. Sistema remove token
4. Sistema desconecta chat
5. Sistema redireciona para welcome

---

### RF04 - Validação de Sessão
**Descrição**: O sistema deve validar sessão do usuário em cada requisição.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3

**Critérios de Aceitação**:
- ✅ Sistema verifica token JWT em cada requisição
- ✅ Sistema valida expiração do token
- ✅ Sistema redireciona para login se token inválido
- ✅ Sistema renova token próximo à expiração

**Regras de Negócio**:
- RN07: Token inválido = logout automático
- RN08: Renovar token se faltarem < 2h para expirar

---

## 3. Módulo de Tópicos

### RF05 - Listar Tópicos Disponíveis
**Descrição**: O sistema deve exibir os tópicos de conversa disponíveis.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 2, 3, 4

**Critérios de Aceitação**:
- ✅ Sistema exibe 3 tópicos: Filmes, Jogos, Séries
- ✅ Cada tópico tem ícone e nome
- ✅ Tópicos são clicáveis
- ✅ Sistema indica número de usuários online por tópico (opcional)

**Fluxo Principal**:
1. Usuário acessa tela de seleção
2. Sistema carrega tópicos do banco
3. Sistema exibe tópicos em cards
4. Usuário visualiza opções

---

### RF06 - Selecionar Tópico
**Descrição**: O sistema deve permitir que usuário escolha um tópico.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Usuário clica em um tópico
- ✅ Sistema registra escolha
- ✅ Sistema busca parceiro no mesmo tópico
- ✅ Sistema redireciona para sala de chat

**Regras de Negócio**:
- RN09: Usuário só pode estar em 1 tópico por vez
- RN10: Tópico deve ter pelo menos 1 outro usuário disponível

**Fluxo Principal**:
1. Usuário clica em tópico
2. Sistema valida disponibilidade
3. Sistema busca parceiro
4. Sistema cria sessão de chat
5. Sistema redireciona para chat

**Fluxos Alternativos**:
- FA08: Nenhum usuário disponível → Exibir "Aguardando..."
- FA09: Erro de conexão → Exibir erro

---

## 4. Módulo de Chat

### RF07 - Conectar com Parceiro
**Descrição**: O sistema deve conectar dois usuários do mesmo tópico.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4

**Critérios de Aceitação**:
- ✅ Sistema busca usuário disponível no mesmo tópico
- ✅ Sistema cria sessão de chat única
- ✅ Sistema conecta ambos via WebSocket
- ✅ Sistema exibe nome anônimo do parceiro
- ✅ Sistema notifica ambos da conexão

**Regras de Negócio**:
- RN11: Conexão é sempre 1-para-1
- RN12: Nomes são gerados aleatoriamente (ex: "Usuário #1234")
- RN13: Sessão é temporária (não persistida)

**Fluxo Principal**:
1. Sistema recebe solicitação de conexão
2. Sistema busca parceiro disponível
3. Sistema cria ID de sessão único
4. Sistema conecta ambos via WebSocket
5. Sistema notifica início do chat

**Fluxos Alternativos**:
- FA10: Nenhum parceiro disponível → Entrar em fila de espera
- FA11: Parceiro desconecta durante conexão → Buscar novo parceiro

---

### RF08 - Enviar Mensagem
**Descrição**: O sistema deve permitir envio de mensagens de texto.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4

**Critérios de Aceitação**:
- ✅ Usuário digita mensagem (máx 500 caracteres)
- ✅ Usuário clica em "Enviar"
- ✅ Sistema valida mensagem não vazia
- ✅ Sistema envia via WebSocket
- ✅ Sistema exibe mensagem na tela do remetente
- ✅ Sistema entrega mensagem ao destinatário
- ✅ Sistema exibe timestamp

**Regras de Negócio**:
- RN14: Mensagem não pode estar vazia
- RN15: Máximo 500 caracteres por mensagem
- RN16: Mensagens não são armazenadas permanentemente
- RN17: Filtrar palavras ofensivas (opcional)

**Fluxo Principal**:
1. Usuário digita mensagem
2. Usuário clica em enviar
3. Sistema valida mensagem
4. Sistema envia via WebSocket
5. Sistema exibe para ambos usuários

**Fluxos Alternativos**:
- FA12: Mensagem vazia → Não enviar
- FA13: Conexão perdida → Exibir erro e tentar reconectar
- FA14: Mensagem muito longa → Truncar ou exibir erro

---

### RF09 - Receber Mensagem
**Descrição**: O sistema deve receber e exibir mensagens do parceiro.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3, 4

**Critérios de Aceitação**:
- ✅ Sistema escuta WebSocket
- ✅ Sistema recebe mensagem
- ✅ Sistema exibe mensagem na tela
- ✅ Sistema diferencia visualmente mensagens próprias e do parceiro
- ✅ Sistema faz scroll automático para última mensagem

**Fluxo Principal**:
1. Sistema recebe evento WebSocket
2. Sistema valida mensagem
3. Sistema adiciona à lista de mensagens
4. Sistema renderiza na tela
5. Sistema faz scroll para baixo

---

### RF10 - Trocar de Parceiro
**Descrição**: O sistema deve permitir trocar de parceiro de conversa.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Usuário clica em "Próximo"
- ✅ Sistema desconecta do parceiro atual
- ✅ Sistema limpa histórico de mensagens
- ✅ Sistema busca novo parceiro no mesmo tópico
- ✅ Sistema conecta com novo parceiro

**Regras de Negócio**:
- RN18: Histórico de mensagens é apagado
- RN19: Parceiro anterior é notificado da desconexão
- RN20: Não conectar com o mesmo parceiro imediatamente

**Fluxo Principal**:
1. Usuário clica em "Próximo"
2. Sistema confirma ação
3. Sistema desconecta parceiro atual
4. Sistema limpa mensagens
5. Sistema busca novo parceiro
6. Sistema conecta com novo parceiro

**Fluxos Alternativos**:
- FA15: Nenhum novo parceiro disponível → Exibir "Aguardando..."

---

### RF11 - Sair do Chat
**Descrição**: O sistema deve permitir sair da sala de chat.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Usuário clica em "Sair"
- ✅ Sistema desconecta do parceiro
- ✅ Sistema limpa histórico
- ✅ Sistema notifica parceiro
- ✅ Sistema redireciona para seleção de tópicos

**Fluxo Principal**:
1. Usuário clica em "Sair"
2. Sistema confirma ação
3. Sistema desconecta WebSocket
4. Sistema limpa dados da sessão
5. Sistema redireciona para seleção

---

### RF12 - Indicador de Digitação
**Descrição**: O sistema deve mostrar quando parceiro está digitando.

**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Sistema detecta quando usuário está digitando
- ✅ Sistema envia evento via WebSocket
- ✅ Sistema exibe "Usuário está digitando..." para parceiro
- ✅ Indicador desaparece após 3 segundos sem digitação

**Regras de Negócio**:
- RN21: Enviar evento a cada 2 segundos enquanto digita
- RN22: Timeout de 3 segundos para remover indicador

---

### RF13 - Notificação de Desconexão
**Descrição**: O sistema deve notificar quando parceiro desconecta.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Sistema detecta desconexão do parceiro
- ✅ Sistema exibe mensagem "Parceiro desconectou"
- ✅ Sistema oferece opções: "Buscar Novo" ou "Sair"
- ✅ Sistema limpa mensagens após escolha

**Fluxo Principal**:
1. Sistema detecta desconexão
2. Sistema exibe notificação
3. Sistema exibe opções
4. Usuário escolhe ação
5. Sistema executa ação escolhida

---

## 5. Módulo de Informações

### RF14 - Visualizar Sobre o App
**Descrição**: O sistema deve exibir informações sobre o aplicativo.

**Prioridade**: Baixa  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Usuário acessa tela "Sobre"
- ✅ Sistema exibe descrição do app
- ✅ Sistema exibe versão
- ✅ Sistema exibe política de privacidade
- ✅ Sistema exibe termos de uso

**Conteúdo**:
- Nome do app
- Versão
- Descrição
- Política de privacidade
- Termos de uso
- Contato/suporte

---

### RF15 - Política de Privacidade
**Descrição**: O sistema deve exibir política de privacidade.

**Prioridade**: Alta (legal)  
**UC Relacionada**: UC 01, 02 Parte 4

**Critérios de Aceitação**:
- ✅ Usuário acessa política de privacidade
- ✅ Sistema exibe texto completo
- ✅ Sistema destaca: "Não coletamos dados pessoais"
- ✅ Sistema explica dados coletados (apenas email)

---

## 6. Requisitos de Interface

### RF16 - Navegação entre Telas
**Descrição**: O sistema deve permitir navegação fluida entre telas.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Transições suaves entre telas
- ✅ Botão "Voltar" funcional
- ✅ Navegação intuitiva
- ✅ Estado preservado ao voltar

**Fluxo de Navegação**:
```
Welcome → Login/Register → Home → Chat Select → Chat Room
                ↓                      ↓            ↓
              About                  About        Sair
```

---

### RF17 - Feedback Visual
**Descrição**: O sistema deve fornecer feedback visual para ações.

**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Loading spinner durante carregamento
- ✅ Mensagens de sucesso (verde)
- ✅ Mensagens de erro (vermelho)
- ✅ Animações suaves
- ✅ Estados de botão (normal, pressionado, desabilitado)

---

### RF18 - Responsividade
**Descrição**: O sistema deve funcionar em diferentes tamanhos de tela.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Layout adaptável a diferentes resoluções
- ✅ Funcional em smartphones (5" a 7")
- ✅ Funcional em tablets
- ✅ Orientação portrait e landscape

---

## 7. Requisitos de Dados

### RF19 - Persistência Local
**Descrição**: O sistema deve armazenar dados localmente quando necessário.

**Prioridade**: Média  
**UC Relacionada**: UC 02 Parte 4

**Critérios de Aceitação**:
- ✅ Token JWT armazenado localmente
- ✅ Preferências do usuário (opcional)
- ✅ Dados limpos ao fazer logout

**Dados Armazenados**:
- Token de autenticação
- Email do usuário (opcional)
- Configurações (futuro)

---

### RF20 - Limpeza de Dados
**Descrição**: O sistema deve limpar dados temporários regularmente.

**Prioridade**: Alta  
**UC Relacionada**: UC 02 Parte 3

**Critérios de Aceitação**:
- ✅ Mensagens de chat não são persistidas
- ✅ Sessões expiradas são removidas
- ✅ Dados temporários limpos ao sair

**Regras de Negócio**:
- RN23: Mensagens existem apenas durante sessão ativa
- RN24: Sessões inativas > 30min são encerradas
- RN25: Dados de chat são voláteis (apenas em memória)

---

## 8. Matriz de Rastreabilidade

| RF | Prioridade | UC | Status | Testes |
|----|-----------|-----|--------|--------|
| RF01 | Alta | 02-3, 02-4 | Planejado | TC01-TC05 |
| RF02 | Alta | 02-3, 02-4 | Planejado | TC06-TC10 |
| RF03 | Alta | 02-4 | Planejado | TC11-TC12 |
| RF04 | Alta | 02-3 | Planejado | TC13-TC15 |
| RF05 | Alta | 02-2, 02-3, 02-4 | Planejado | TC16-TC17 |
| RF06 | Alta | 02-4 | Planejado | TC18-TC20 |
| RF07 | Alta | 02-3, 02-4 | Planejado | TC21-TC25 |
| RF08 | Alta | 02-3, 02-4 | Planejado | TC26-TC30 |
| RF09 | Alta | 02-3, 02-4 | Planejado | TC31-TC33 |
| RF10 | Alta | 02-4 | Planejado | TC34-TC36 |
| RF11 | Alta | 02-4 | Planejado | TC37-TC38 |
| RF12 | Média | 02-4 | Planejado | TC39-TC40 |
| RF13 | Alta | 02-4 | Planejado | TC41-TC42 |
| RF14 | Baixa | 02-4 | Planejado | TC43 |
| RF15 | Alta | 01, 02-4 | Planejado | TC44 |
| RF16 | Alta | 02-4 | Planejado | TC45-TC47 |
| RF17 | Média | 02-4 | Planejado | TC48-TC50 |
| RF18 | Alta | 02-4 | Planejado | TC51-TC53 |
| RF19 | Média | 02-4 | Planejado | TC54-TC55 |
| RF20 | Alta | 02-3 | Planejado | TC56-TC57 |

## 9. Resumo Quantitativo

- **Total de Requisitos Funcionais**: 20
- **Prioridade Alta**: 15 (75%)
- **Prioridade Média**: 4 (20%)
- **Prioridade Baixa**: 1 (5%)

### Por Módulo
- **Autenticação**: 4 requisitos
- **Tópicos**: 2 requisitos
- **Chat**: 7 requisitos
- **Informações**: 2 requisitos
- **Interface**: 3 requisitos
- **Dados**: 2 requisitos

---

**Documento:** Requisitos Funcionais  
**Versão:** 1.0  
**Data:** 2024  
**Próxima Revisão:** Após UC 01  
**Aprovação:** Pendente
