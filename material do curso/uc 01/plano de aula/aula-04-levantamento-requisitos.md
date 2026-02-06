# PLANO DE TRABALHO DOCENTE 

## MODELO PEDAGÓGICO SENAC 

**Curso:** Programador Mobile  
**Carga Horária Total:** 192h  
**Carga Horária da UC:** 36h  

**Docente:** Jeremias O Nunes  

---

## PLANO DE AULA – Análise e Levantamento Inicial de Requisitos - MeetStranger

📌 **Disciplina:** UC 01 - Planejar o Desenvolvimento de Softwares  
👨🏫 **Mentor(a):** Jeremias O Nunes  
📆 **Data:** 12/02/2026 (Quinta-feira) - Aula nº 4  
⏰ **Duração:** 4 horas  

---

## 📖 Planejamento

### 📌 Conteúdo Formativo
- Técnicas de levantamento de requisitos
- Identificação de necessidades do cliente
- Mapeamento de requisitos funcionais do MeetStranger
- Mapeamento de requisitos não funcionais do MeetStranger
- Priorização de requisitos

### 🎯 Objetivo Geral
Identificar e documentar os requisitos iniciais do projeto MeetStranger através de trabalho colaborativo, aplicando técnicas de levantamento e análise de requisitos.

### 💡 Habilidades e Competências
✅ Ler, interpretar e elaborar documentos técnicos  
✅ Trabalhar em equipe multi e interdisciplinar  
✅ Localizar e selecionar informações necessárias ao desenvolvimento do trabalho  
✅ Negociar com pessoas em situações adversas, identificando problemas e possíveis soluções  

### 📌 Materiais Necessários
📌 Briefing do projeto MeetStranger  
📌 Template de documentação de requisitos  
📌 Post-its coloridos (amarelo para RF, azul para RNF)  
📌 Quadro branco ou flipchart  
📌 Computadores para documentação  

---

## 🎓 Estratégias de Ensino e Aprendizagem

### Introdução e Contextualização (20min)
**Metodologia Ativa - Retomada e Contextualização:**  
- Revisão rápida da aula anterior sobre RF e RNF
- Apresentação dos objetivos da aula
- Explicação da dinâmica de trabalho em grupo
- Formação de grupos de 4-5 alunos
- Distribuição de materiais (post-its, templates)

---

### **Tópico 1: Técnicas de Levantamento de Requisitos (40min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Aula Expositiva com Exemplos Práticos:**  
O docente apresenta as principais técnicas de levantamento:

1. **Entrevistas** - Conversar com stakeholders
2. **Brainstorming** - Geração livre de ideias
3. **Análise de Documentos** - Estudar briefing, documentação existente
4. **Observação** - Analisar sistemas similares
5. **Prototipação** - Criar mockups para validar ideias

**Aplicação ao MeetStranger:**
- Análise do briefing como documento base
- Observação de apps similares (Omegle, Chatroulette)
- Brainstorming de funcionalidades

#### 📌 Atividade Prática 1:
🎯 **Objetivo:** Compreender e aplicar técnicas de levantamento  
📝 **Tarefa:**  
- **Metodologia Ativa - Análise Guiada em Grupo:**  
Cada grupo recebe o briefing do MeetStranger e deve:
1. Ler atentamente o documento (10min)
2. Destacar todas as funcionalidades mencionadas
3. Identificar necessidades implícitas (não escritas mas necessárias)
4. Listar perguntas que fariam ao "cliente"

**Parte do Projeto Construída:** Compreensão profunda das necessidades do projeto

---

### **Tópico 2: Brainstorming de Requisitos Funcionais (50min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Brainstorming Estruturado:**  
O docente explica a dinâmica:
- Fase 1: Geração livre de ideias (sem críticas)
- Fase 2: Organização por categorias
- Fase 3: Refinamento e priorização

**Categorias de RF para o MeetStranger:**
1. **Autenticação** - Cadastro, login, logout
2. **Tópicos** - Listar, selecionar tópicos
3. **Chat** - Conectar, enviar, receber mensagens
4. **Navegação** - Transições entre telas
5. **Informações** - Sobre o app, políticas

#### 📌 Atividade Prática 2:
🎯 **Objetivo:** Levantar todos os requisitos funcionais possíveis  
📝 **Tarefa:**  
- **Metodologia Ativa - Brainstorming em Grupo:**  

**Fase 1 - Geração (20min):**
- Cada grupo usa post-its amarelos
- Cada post-it = 1 requisito funcional
- Escrever no formato: "O sistema deve [ação]"
- Colar no quadro/parede organizando por categoria
- Meta: mínimo 15 requisitos por grupo

**Fase 2 - Organização (15min):**
- Agrupar requisitos similares
- Eliminar duplicatas
- Categorizar por módulo do sistema

**Fase 3 - Refinamento (15min):**
- Revisar cada requisito
- Garantir clareza e objetividade
- Adicionar detalhes se necessário

**Parte do Projeto Construída:** Lista inicial de requisitos funcionais

---

### **Tópico 3: Mapeamento de Requisitos Não Funcionais (50min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Apresentação com Exemplos do Projeto:**  
O docente relembra as categorias de RNF e dá exemplos específicos do MeetStranger:

**Desempenho:**
- "O tempo de resposta da API deve ser < 2 segundos"
- "O app deve suportar 50 usuários simultâneos"

**Segurança:**
- "Senhas devem ser armazenadas com hash bcrypt"
- "Comunicação deve usar HTTPS"

**Usabilidade:**
- "Interface deve ser intuitiva (máximo 3 cliques)"
- "Mensagens de erro devem ser claras"

**Confiabilidade:**
- "Sistema deve ter 95% de disponibilidade"
- "Reconexão automática em caso de queda"

#### 📌 Atividade Prática 3:
🎯 **Objetivo:** Identificar requisitos não funcionais do MeetStranger  
📝 **Tarefa:**  
- **Metodologia Ativa - Mapeamento por Categoria:**  

Cada grupo recebe uma categoria de RNF para focar:
- **Grupo 1:** Desempenho e Escalabilidade
- **Grupo 2:** Segurança e Privacidade
- **Grupo 3:** Usabilidade e Acessibilidade
- **Grupo 4:** Confiabilidade e Disponibilidade
- **Grupo 5:** Manutenibilidade e Portabilidade

**Tarefa (30min):**
1. Usar post-its azuis para RNF
2. Listar mínimo 5 RNF da sua categoria
3. Garantir que sejam mensuráveis
4. Incluir métrica quando possível
5. Colar no quadro organizado por categoria

**Apresentação (20min):**
- Cada grupo apresenta seus RNF (4min cada)
- Turma discute e valida
- Docente complementa com RNF importantes não mencionados

**Parte do Projeto Construída:** Lista inicial de requisitos não funcionais

---

### **Tópico 4: Documentação e Priorização de Requisitos (40min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Demonstração de Template:**  
O docente apresenta o template de documentação de requisitos:

**Estrutura de um RF:**
```
ID: RF001
Título: Cadastro de Usuário
Descrição: O sistema deve permitir que novos usuários criem uma conta
Prioridade: Alta
Critérios de Aceitação:
- Usuário informa email e senha
- Email deve ser válido
- Senha deve ter mínimo 6 caracteres
```

**Estrutura de um RNF:**
```
ID: RNF001
Título: Tempo de Resposta da API
Categoria: Desempenho
Descrição: As requisições à API devem ser processadas rapidamente
Métrica: < 2 segundos para 95% das requisições
Prioridade: Alta
```

#### 📌 Atividade Prática 4:
🎯 **Objetivo:** Documentar formalmente os requisitos levantados  
📝 **Tarefa:**  
- **Metodologia Ativa - Documentação Colaborativa:**  

**Parte 1 - Seleção (10min):**
- Cada grupo seleciona os 5 requisitos mais importantes que levantaram
- 3 RF + 2 RNF

**Parte 2 - Documentação (20min):**
- Documentar cada requisito seguindo o template
- Usar computador/Google Docs compartilhado
- Incluir todos os campos obrigatórios
- Definir prioridade: Alta, Média ou Baixa

**Parte 3 - Validação (10min):**
- Trocar documentos entre grupos
- Revisar e dar feedback
- Identificar melhorias

**Parte do Projeto Construída:** Primeiros requisitos formalmente documentados

---

### Encerramento e Reflexão (20min)
#### 📌 Discussão em grupo:
**Metodologia Ativa - Galeria de Requisitos:**  
- Todos os post-its ficam expostos no quadro
- Turma faz uma "caminhada" observando todos os requisitos
- Discussão: "Conseguimos cobrir todas as funcionalidades do MeetStranger?"
- Identificação de gaps (requisitos faltantes)

#### 📌 Desafio para a próxima aula:
**Metodologia Ativa - Pesquisa e Reflexão:**  
Cada aluno deve:
1. Revisar os requisitos levantados hoje
2. Pensar em 2 requisitos que faltaram
3. Pesquisar sobre "Scrum" e "Kanban" (próxima aula)
4. Trazer dúvidas sobre os requisitos documentados

---

### 📌 Objetos de Aprendizagem
📝 **Materiais Didáticos Utilizados:**  
- Briefing do projeto MeetStranger
- Template de documentação de requisitos
- Post-its coloridos para brainstorming
- Quadro para organização visual
- Exemplos de requisitos de sistemas reais

---

## 🎯 Avaliação

### **Avaliação Formativa (Durante a aula):**
✅ Participação ativa no brainstorming  
✅ Qualidade dos requisitos levantados  
✅ Colaboração no trabalho em grupo  
✅ Capacidade de categorizar requisitos corretamente  
✅ Clareza na documentação  

### **Avaliação Somativa (Entregáveis):**
✅ Lista de requisitos funcionais levantados (em grupo)  
✅ Lista de requisitos não funcionais levantados (em grupo)  
✅ 5 requisitos formalmente documentados (em grupo)  

### **Critérios de Qualidade:**
- **Excelente (9-10):** Levantou 15+ requisitos relevantes, documentação clara e completa, todos os campos preenchidos corretamente, priorização coerente  
- **Bom (7-8):** Levantou 10-14 requisitos relevantes, documentação adequada, campos principais preenchidos, priorização razoável  
- **Satisfatório (6-7):** Levantou 7-9 requisitos, documentação básica, alguns campos faltando, priorização simples  
- **Insatisfatório (<6):** Menos de 7 requisitos, documentação incompleta ou confusa, campos importantes faltando  

---

## 🎓 Conclusão

### **Aprendizado Esperado:**
🎯 **Conhecimento Técnico:**  
- Técnicas de levantamento de requisitos
- Diferenciação prática entre RF e RNF
- Estrutura de documentação de requisitos
- Priorização de requisitos

🎯 **Aplicação Prática:**  
- Levantamento de requisitos do MeetStranger
- Trabalho colaborativo em equipe
- Documentação técnica profissional
- Organização e categorização de informações

🎯 **Competências Profissionais:**  
- Trabalho em equipe
- Comunicação técnica
- Análise crítica
- Documentação profissional
- Negociação e consenso em grupo

### **Conexão com o Projeto:**  
Esta aula é crucial para o MeetStranger. Os requisitos levantados hoje são a base de TUDO que será desenvolvido nas próximas UCs. Cada linha de código, cada tela, cada funcionalidade virá destes requisitos.

### **Preparação para Próxima Aula:**  
Na próxima aula (Recuperação), estudaremos metodologias ágeis (Scrum e Kanban) que nos ajudarão a organizar o desenvolvimento destes requisitos. Os alunos devem pesquisar sobre estas metodologias.

---

## 📝 Observações para o Docente

### Preparação Prévia
- Imprimir templates de requisitos (1 por grupo)
- Preparar post-its em 2 cores diferentes
- Revisar briefing do MeetStranger
- Preparar exemplos de requisitos bem e mal escritos
- Testar acesso ao Google Docs compartilhado

### Durante a Aula
- Circular entre os grupos durante brainstorming
- Auxiliar grupos com dificuldade
- Garantir que todos participem
- Fotografar o quadro com todos os post-its ao final
- Coletar documentos produzidos

### Após a Aula
- Consolidar todos os requisitos levantados
- Criar documento único com todos os requisitos
- Identificar gaps para abordar na aula 6
- Preparar feedback individual por grupo
