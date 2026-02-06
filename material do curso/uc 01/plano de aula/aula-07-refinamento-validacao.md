# PLANO DE TRABALHO DOCENTE 

## MODELO PEDAGÓGICO SENAC 

**Curso:** Programador Mobile  
**Carga Horária Total:** 192h  
**Carga Horária da UC:** 36h  

**Docente:** Mateus  

---

## PLANO DE AULA – Continuação do Levantamento e Documentação

📌 **Disciplina:** UC 01 - Planejar o Desenvolvimento de Softwares  
👨🏫 **Mentor(a):** Mateus  
📆 **Data:** 19/02/2026 (Quinta-feira) - Aula nº 7  
⏰ **Duração:** 4 horas  

---

## 📖 Planejamento

### 📌 Conteúdo Formativo
- Refinamento de requisitos documentados
- Regras de negócio do MeetStranger
- Casos de uso principais
- Validação cruzada de documentação
- Garantia de consistência e completude
- Preparação para prototipação

### 🎯 Objetivo Geral
Refinar, validar e finalizar a documentação de requisitos do MeetStranger, garantindo clareza, consistência e completude, além de documentar regras de negócio e casos de uso principais.

### 💡 Habilidades e Competências
✅ Ler, interpretar e elaborar documentos técnicos  
✅ Trabalhar em equipe multi e interdisciplinar  
✅ Negociar com pessoas em situações adversas, identificando problemas e possíveis soluções  
✅ Desenvolver senso crítico frente ao processo de trabalho  

### 📌 Materiais Necessários
📌 Documentação produzida na aula 6  
📌 Template de regras de negócio  
📌 Template de casos de uso  
📌 Checklist de validação de requisitos  
📌 Computadores com acesso aos documentos  

---

## 🎓 Estratégias de Ensino e Aprendizagem

### Introdução e Contextualização (15min)
**Metodologia Ativa - Retomada e Planejamento:**  
- Revisão do que foi produzido na aula anterior
- Apresentação dos objetivos da aula
- Explicação da dinâmica: refinamento → regras de negócio → casos de uso → validação
- Distribuição dos documentos produzidos na aula 6
- Formação dos mesmos grupos de trabalho

---

### **Tópico 1: Refinamento e Peer Review de Requisitos (60min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Apresentação de Checklist de Qualidade:**  

**Checklist de Validação de Requisitos:**

**Para Requisitos Funcionais:**
- [ ] ID único e sequencial?
- [ ] Título claro e objetivo?
- [ ] Descrição usa linguagem "O sistema deve..."?
- [ ] Tem mínimo 5 critérios de aceitação?
- [ ] Fluxo principal está completo (passo a passo)?
- [ ] Tem pelo menos 2 fluxos alternativos?
- [ ] Regras de negócio estão identificadas?
- [ ] Prioridade está definida (MoSCoW)?
- [ ] Relacionamentos estão mapeados?
- [ ] Português está correto?

**Para Requisitos Não Funcionais:**
- [ ] ID único e sequencial?
- [ ] Categoria está correta?
- [ ] Descrição é clara?
- [ ] Tem métrica mensurável? (CRÍTICO)
- [ ] Métrica é objetiva (números, percentuais)?
- [ ] Explica como testar?
- [ ] Descreve impacto se não atendido?
- [ ] Prioridade está definida?
- [ ] Relacionamentos com RF estão mapeados?

**Critérios de Consistência:**
- IDs não se repetem
- Nomenclatura padronizada
- Mesmo nível de detalhamento
- Sem contradições entre requisitos
- Sem duplicatas

#### 📌 Atividade Prática 1:
🎯 **Objetivo:** Refinar e validar requisitos documentados  
📝 **Tarefa:**  
- **Metodologia Ativa - Peer Review Estruturado:**  

**Rodada 1 - Auto-revisão (20min):**
- Cada grupo revisa seus próprios requisitos
- Usar checklist de validação
- Identificar e corrigir problemas
- Completar campos faltantes
- Melhorar descrições vagas

**Rodada 2 - Troca de Documentos (25min):**
- Grupos trocam documentos em rotação:
  - Grupo 1 → Grupo 2 → Grupo 3 → Grupo 4 → Grupo 5 → Grupo 1
- Revisar documento recebido usando checklist
- Anotar sugestões de melhoria
- Identificar inconsistências
- Marcar pontos fortes

**Rodada 3 - Aplicação de Feedback (15min):**
- Grupos recebem documento de volta com feedback
- Aplicar melhorias sugeridas
- Discutir pontos controversos
- Finalizar ajustes

**Parte do Projeto Construída:** Requisitos refinados e validados

---

### **Tópico 2: Documentação de Regras de Negócio (55min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Apresentação com Exemplos do MeetStranger:**  

**O que são Regras de Negócio?**
- Políticas, restrições e condições que governam o sistema
- Derivam dos requisitos
- Independentes de tecnologia
- Validam e restringem comportamentos

**Estrutura de uma Regra de Negócio:**
```
ID: RN001
Módulo: Autenticação
Título: Unicidade de Email

Descrição:
Cada email pode estar associado a apenas uma conta no sistema.

Justificativa:
Garantir identificação única de usuários e evitar duplicação 
de contas.

Condição:
Quando um usuário tenta se cadastrar com um email já existente.

Ação:
Sistema deve rejeitar o cadastro e exibir mensagem de erro.

Relacionado a:
- RF001: Cadastro de Usuário
- RNF10: Privacidade de Dados

Prioridade: Must Have
```

**Exemplos de Regras de Negócio do MeetStranger:**

**RN01:** Email deve ser único no sistema  
**RN02:** Senha deve ter mínimo 6 caracteres  
**RN03:** Usuário só pode estar em 1 chat por vez  
**RN04:** Mensagens não são armazenadas permanentemente  
**RN05:** Tópicos são fixos (Filmes, Jogos, Séries)  
**RN06:** Conexão é sempre 1-para-1 (P2P)  
**RN07:** Nomes de usuário são gerados aleatoriamente  
**RN08:** Sessão expira após 24 horas de inatividade  
**RN09:** Máximo 3 tentativas de login incorretas  
**RN10:** Mensagem não pode estar vazia  

#### 📌 Atividade Prática 2:
🎯 **Objetivo:** Identificar e documentar regras de negócio  
📝 **Tarefa:**  
- **Metodologia Ativa - Extração de Regras de Negócio:**  

**Passo 1 - Identificação (20min):**
- Cada grupo analisa seus requisitos documentados
- Identificar regras de negócio implícitas
- Listar todas as regras encontradas
- Categorizar por módulo

**Passo 2 - Documentação (25min):**
- Documentar mínimo 5 regras de negócio
- Usar template fornecido
- Incluir todos os campos obrigatórios
- Relacionar com requisitos correspondentes

**Passo 3 - Compartilhamento (10min):**
- Cada grupo apresenta 2 regras principais (1min cada)
- Turma valida se são realmente regras de negócio
- Docente complementa com regras não identificadas

**Parte do Projeto Construída:** Regras de negócio documentadas

---

### **Tópico 3: Criação de Casos de Uso (60min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Modelagem Guiada:**  

**O que são Casos de Uso?**
- Descrevem interação entre usuário (ator) e sistema
- Focam no "o que" o sistema faz, não no "como"
- Complementam requisitos funcionais
- Base para testes de aceitação

**Estrutura de um Caso de Uso:**
```
ID: UC01
Nome: Fazer Login
Ator Principal: Usuário
Objetivo: Autenticar usuário no sistema

Pré-condições:
- Usuário possui conta cadastrada
- Usuário está na tela de login

Fluxo Principal:
1. Usuário informa email
2. Usuário informa senha
3. Usuário clica em "Entrar"
4. Sistema valida credenciais
5. Sistema gera token JWT
6. Sistema armazena token localmente
7. Sistema redireciona para tela Home
8. Caso de uso encerrado com sucesso

Fluxos Alternativos:
FA1: Credenciais Inválidas (passo 4)
  4a. Sistema identifica credenciais incorretas
  4b. Sistema exibe mensagem de erro
  4c. Sistema incrementa contador de tentativas
  4d. Retorna ao passo 1

FA2: Conta Bloqueada (passo 4)
  4a. Sistema identifica 3 tentativas incorretas
  4b. Sistema bloqueia conta por 15 minutos
  4c. Sistema exibe mensagem de bloqueio
  4d. Caso de uso encerrado com falha

Pós-condições:
- Usuário está autenticado
- Token JWT está armazenado
- Usuário está na tela Home

Requisitos Relacionados:
- RF02: Login de Usuário
- RNF08: Autenticação Segura
- RN04: Token expira em 24h
- RN09: Máximo 3 tentativas

Frequência de Uso: Alta
Prioridade: Must Have
```

**Casos de Uso Principais do MeetStranger:**
1. UC01: Fazer Login
2. UC02: Fazer Cadastro
3. UC03: Selecionar Tópico
4. UC04: Conectar com Parceiro
5. UC05: Enviar Mensagem
6. UC06: Trocar de Parceiro
7. UC07: Sair do Chat

#### 📌 Atividade Prática 3:
🎯 **Objetivo:** Criar casos de uso principais  
📝 **Tarefa:**  
- **Metodologia Ativa - Modelagem em Grupo:**  

**Distribuição de Casos de Uso:**
- **Grupo 1:** UC01 (Login) + UC02 (Cadastro)
- **Grupo 2:** UC03 (Selecionar Tópico) + UC04 (Conectar)
- **Grupo 3:** UC05 (Enviar Mensagem) + UC06 (Trocar Parceiro)
- **Grupo 4:** UC07 (Sair do Chat) + UC08 (Fazer Logout)
- **Grupo 5:** UC09 (Visualizar Sobre) + Revisão geral

**Tarefa (40min):**
1. Modelar os casos de uso designados
2. Incluir todos os campos obrigatórios
3. Detalhar fluxo principal (mínimo 5 passos)
4. Incluir mínimo 2 fluxos alternativos
5. Relacionar com requisitos e regras de negócio

**Apresentação (20min):**
- Cada grupo apresenta 1 caso de uso (3min)
- Turma faz perguntas e sugestões
- Docente valida e complementa

**Parte do Projeto Construída:** Casos de uso principais documentados

---

### **Tópico 4: Validação Final e Consolidação (45min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Validação Cruzada:**  

**Critérios de Validação Final:**

**Completude:**
- [ ] Todos os módulos têm requisitos documentados?
- [ ] Todos os RF têm critérios de aceitação?
- [ ] Todos os RNF têm métricas?
- [ ] Regras de negócio estão completas?
- [ ] Casos de uso principais estão criados?

**Consistência:**
- [ ] IDs estão sequenciais e únicos?
- [ ] Nomenclatura está padronizada?
- [ ] Não há contradições entre requisitos?
- [ ] Relacionamentos estão corretos?
- [ ] Prioridades são coerentes?

**Clareza:**
- [ ] Descrições são objetivas?
- [ ] Linguagem é técnica mas compreensível?
- [ ] Não há ambiguidades?
- [ ] Português está correto?

**Rastreabilidade:**
- [ ] RF relacionados com RNF?
- [ ] Requisitos relacionados com regras de negócio?
- [ ] Casos de uso relacionados com requisitos?
- [ ] Matriz de rastreabilidade está completa?

#### 📌 Atividade Prática 4:
🎯 **Objetivo:** Validar e consolidar toda a documentação  
📝 **Tarefa:**  
- **Metodologia Ativa - Validação Coletiva:**  

**Passo 1 - Checklist Final (15min):**
- Cada grupo usa checklist de validação final
- Verificar completude de toda documentação
- Identificar gaps ou inconsistências
- Fazer últimos ajustes

**Passo 2 - Apresentação Executiva (20min):**
- Cada grupo apresenta resumo da sua documentação (3min):
  - Quantos RF, RNF, RN, UC documentados
  - Principais funcionalidades cobertas
  - Desafios encontrados
  - Lições aprendidas

**Passo 3 - Consolidação (10min):**
- Docente consolida estatísticas gerais:
  - Total de requisitos documentados
  - Distribuição por prioridade
  - Cobertura de módulos
  - Próximos passos

**Parte do Projeto Construída:** Documentação completa e validada

---

### Encerramento e Reflexão (20min)
#### 📌 Discussão em grupo:
**Metodologia Ativa - Reflexão Coletiva:**  
- "O que aprendemos sobre documentação de requisitos?"
- "Como essa documentação vai facilitar o desenvolvimento?"
- "Quais foram os maiores desafios?"
- "O que faríamos diferente em um próximo projeto?"

#### 📌 Desafio para a próxima aula:
**Metodologia Ativa - Preparação para Prototipação:**  
Cada aluno deve:
1. Revisar toda a documentação produzida
2. Pensar em como as telas do MeetStranger devem ser
3. Pesquisar sobre prototipação de interfaces
4. Criar conta no Canva (gratuita)
5. Trazer ideias de layout para as telas principais

---

### 📌 Objetos de Aprendizagem
📝 **Materiais Didáticos Utilizados:**  
- Checklist de validação de requisitos
- Template de regras de negócio
- Template de casos de uso
- Exemplos de casos de uso completos
- Matriz de rastreabilidade

---

## 🎯 Avaliação

### **Avaliação Formativa (Durante a aula):**
✅ Qualidade do refinamento dos requisitos  
✅ Identificação correta de regras de negócio  
✅ Completude dos casos de uso  
✅ Participação na validação cruzada  
✅ Aplicação de feedback recebido  
✅ Colaboração no trabalho em grupo  

### **Avaliação Somativa (Entregáveis):**
✅ Requisitos refinados e validados (em grupo)  
✅ Mínimo 5 regras de negócio documentadas (em grupo)  
✅ Mínimo 2 casos de uso completos (em grupo)  
✅ Checklist de validação preenchido (em grupo)  

### **Critérios de Qualidade:**
- **Excelente (9-10):** Documentação completa, refinada, sem inconsistências, regras de negócio claras, casos de uso detalhados, todos os checklists OK  
- **Bom (7-8):** Documentação adequada, refinamento aplicado, regras de negócio identificadas, casos de uso completos, poucos itens pendentes  
- **Satisfatório (6-7):** Documentação básica, refinamento parcial, regras de negócio simples, casos de uso funcionais, alguns itens pendentes  
- **Insatisfatório (<6):** Documentação incompleta, pouco refinamento, regras de negócio vagas, casos de uso incompletos, muitos itens pendentes  

---

## 🎓 Conclusão

### **Aprendizado Esperado:**
🎯 **Conhecimento Técnico:**  
- Técnicas de refinamento de requisitos
- Estrutura de regras de negócio
- Modelagem de casos de uso
- Validação cruzada de documentação
- Garantia de consistência e completude

🎯 **Aplicação Prática:**  
- Refinamento de requisitos do MeetStranger
- Documentação de regras de negócio reais
- Criação de casos de uso principais
- Validação completa da documentação
- Preparação para próximas fases

🎯 **Competências Profissionais:**  
- Atenção a detalhes
- Pensamento crítico
- Trabalho colaborativo
- Comunicação técnica
- Garantia de qualidade

### **Conexão com o Projeto:**  
Esta aula finaliza a documentação de requisitos do MeetStranger. A partir de agora, temos um guia completo e validado para todo o desenvolvimento. Nas próximas aulas, transformaremos essa documentação em protótipos visuais.

### **Preparação para Próxima Aula:**  
Na próxima aula, começaremos a prototipação das telas no Canva. Os alunos devem criar conta na ferramenta e revisar os requisitos para entender quais telas precisam ser criadas.

---

## 📝 Observações para o Docente

### Preparação Prévia
- Revisar toda documentação produzida na aula 6
- Preparar checklist de validação impresso
- Criar templates de regras de negócio e casos de uso
- Preparar exemplos completos
- Ter estatísticas consolidadas prontas

### Durante a Aula
- Circular entre grupos durante refinamento
- Auxiliar na identificação de regras de negócio
- Validar casos de uso sendo criados
- Garantir que todos os grupos estão progredindo
- Fotografar documentação final

### Após a Aula
- Consolidar TODA a documentação em documento único
- Criar versão final formatada e organizada
- Compartilhar com todos os alunos
- Preparar material para prototipação
- Dar feedback individual por grupo

### Dicas Importantes
- Enfatizar que documentação está quase completa
- Celebrar o trabalho realizado até aqui
- Mostrar como documentação será usada nas próximas UCs
- Preparar transição para fase de prototipação
- Motivar para as próximas aulas práticas
