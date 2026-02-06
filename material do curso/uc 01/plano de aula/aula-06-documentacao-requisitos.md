# PLANO DE TRABALHO DOCENTE 

## MODELO PEDAGÓGICO SENAC 

**Curso:** Programador Mobile  
**Carga Horária Total:** 192h  
**Carga Horária da UC:** 36h  

**Docente:** Jeremias O Nunes  

---

## PLANO DE AULA – Levantamento de Requisitos e Construção de Documentação

📌 **Disciplina:** UC 01 - Planejar o Desenvolvimento de Softwares  
👨🏫 **Mentor(a):** Jeremias O Nunes  
📆 **Data:** 18/02/2026 (Quarta-feira) - Aula nº 6  
⏰ **Duração:** 4 horas  

---

## 📖 Planejamento

### 📌 Conteúdo Formativo
- Padrões de documentação de requisitos
- Estruturação formal de requisitos funcionais
- Estruturação formal de requisitos não funcionais
- Critérios de aceitação e métricas
- Priorização de requisitos (MoSCoW)
- Matriz de rastreabilidade
- Revisão e validação de documentação

### 🎯 Objetivo Geral
Estruturar e documentar formalmente todos os requisitos do projeto MeetStranger seguindo padrões profissionais de engenharia de software.

### 💡 Habilidades e Competências
✅ Ler, interpretar e elaborar documentos técnicos  
✅ Comunicar-se com clareza e objetividade de forma escrita  
✅ Trabalhar em equipe multi e interdisciplinar  
✅ Organizar materiais, ferramentas, instrumentos e documentos  

### 📌 Materiais Necessários
📌 Computadores com acesso à internet  
📌 Template de documentação de requisitos  
📌 Requisitos levantados nas aulas 3 e 4  
📌 Documento de requisitos do MeetStranger (referência)  
📌 Projetor para compartilhamento de telas  

---

## 🎓 Estratégias de Ensino e Aprendizagem

### Introdução e Contextualização (20min)
**Metodologia Ativa - Retomada e Organização:**  
- Revisão dos requisitos levantados nas aulas anteriores
- Apresentação do objetivo: transformar ideias em documentação profissional
- Explicação da importância da documentação no ciclo de desenvolvimento
- Formação de grupos de trabalho (mesmos da aula 4)
- Distribuição de materiais e acesso aos templates

---

### **Tópico 1: Padrões de Documentação de Requisitos (45min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Apresentação com Exemplos Reais:**  

**Por que documentar requisitos?**
- Comunicação clara entre equipe e stakeholders
- Base para desenvolvimento, testes e validação
- Rastreabilidade de mudanças
- Redução de retrabalho

**Estrutura Profissional de um Requisito Funcional:**
```
ID: RF001
Módulo: Autenticação
Título: Cadastro de Usuário
Prioridade: Alta (Must Have)

Descrição:
O sistema deve permitir que novos usuários criem uma conta 
informando email e senha.

Critérios de Aceitação:
✓ Usuário acessa tela de cadastro
✓ Usuário informa email válido (formato: xxx@xxx.xxx)
✓ Usuário informa senha com mínimo 6 caracteres
✓ Usuário confirma senha (deve ser igual)
✓ Sistema valida se email já existe
✓ Sistema criptografa senha (bcrypt)
✓ Sistema cria conta e retorna confirmação
✓ Sistema redireciona para tela de login

Fluxo Principal:
1. Usuário clica em "Criar Conta"
2. Sistema exibe formulário de cadastro
3. Usuário preenche email e senha
4. Usuário clica em "Cadastrar"
5. Sistema valida dados
6. Sistema cria conta
7. Sistema exibe mensagem de sucesso
8. Sistema redireciona para login

Fluxos Alternativos:
FA01: Email já cadastrado
- Sistema exibe erro: "Email já está em uso"
- Usuário pode tentar outro email ou fazer login

FA02: Senhas não conferem
- Sistema exibe erro: "As senhas não conferem"
- Usuário corrige e tenta novamente

Regras de Negócio:
RN01: Email deve ser único no sistema
RN02: Senha deve ter no mínimo 6 caracteres
RN03: Senha deve ser armazenada com hash bcrypt

Relacionado a:
- RNF07: Armazenamento seguro de senhas
- UC01: Fazer Cadastro
```

**Estrutura de um Requisito Não Funcional:**
```
ID: RNF01
Categoria: Desempenho
Título: Tempo de Resposta da API
Prioridade: Alta (Must Have)

Descrição:
As requisições à API devem ser processadas rapidamente 
para garantir boa experiência do usuário.

Métrica Mensurável:
- Requisições GET: < 500ms (95% dos casos)
- Requisições POST: < 1s (95% dos casos)
- Autenticação: < 800ms
- Conexão WebSocket: < 300ms

Como Testar:
- Usar ferramentas de performance testing (JMeter, Artillery)
- Medir tempo médio, mediano e percentil 95
- Testar com carga normal (10 usuários simultâneos)
- Testar em ambiente similar à produção

Impacto se não atendido:
- Usuários abandonam o app por lentidão
- Experiência ruim de chat em tempo real
- Avaliações negativas nas lojas de apps

Relacionado a:
- RF02: Login de Usuário
- RF08: Enviar Mensagem
```

#### 📌 Atividade Prática 1:
🎯 **Objetivo:** Compreender estrutura profissional de documentação  
📝 **Tarefa:**  
- **Metodologia Ativa - Análise Comparativa:**  

Cada grupo recebe 2 versões do mesmo requisito:
- Versão A: Mal documentada (vaga, incompleta)
- Versão B: Bem documentada (completa, clara)

**Tarefa (15min):**
1. Identificar diferenças entre as versões
2. Listar o que torna a Versão B melhor
3. Apresentar 3 principais diferenças

**Discussão (10min):**
- Cada grupo compartilha suas conclusões
- Docente consolida os pontos importantes

**Parte do Projeto Construída:** Compreensão de documentação profissional

---

### **Tópico 2: Estruturação de Requisitos Funcionais (70min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Demonstração ao Vivo:**  
- Docente pega um requisito levantado na aula 4
- Transforma em documentação profissional ao vivo
- Explica cada campo enquanto preenche
- Mostra onde buscar informações (briefing, casos de uso)
- Demonstra uso do template no Google Docs

**Método MoSCoW para Priorização:**
- **Must Have** (Deve ter): Essencial, sem isso o app não funciona
- **Should Have** (Deveria ter): Importante, mas não crítico
- **Could Have** (Poderia ter): Desejável, se houver tempo
- **Won't Have** (Não terá): Fora do escopo do MVP

Exemplos no MeetStranger:
- Must: Login, Chat, Seleção de tópicos
- Should: Indicador de digitação, Sobre o app
- Could: Dark mode, Mais tópicos
- Won't: Chamadas de voz, Compartilhar mídia

#### 📌 Atividade Prática 2:
🎯 **Objetivo:** Documentar requisitos funcionais do MeetStranger  
📝 **Tarefa:**  
- **Metodologia Ativa - Produção Orientada de Documentação:**  

**Organização do Trabalho:**
Cada grupo recebe um módulo do MeetStranger:
- **Grupo 1:** Autenticação (Cadastro, Login, Logout, Validação)
- **Grupo 2:** Tópicos (Listar, Selecionar)
- **Grupo 3:** Chat P2P (Conectar, Enviar, Receber, Trocar parceiro)
- **Grupo 4:** Interface e Navegação (Telas, Transições, Feedback)
- **Grupo 5:** Informações (Sobre, Política de privacidade)

**Passo 1 - Seleção (10min):**
- Revisar requisitos do seu módulo (aula 4)
- Selecionar os 5 mais importantes
- Priorizar usando MoSCoW

**Passo 2 - Documentação (40min):**
- Usar template fornecido
- Documentar cada requisito completamente:
  - ID, Módulo, Título, Prioridade
  - Descrição clara e objetiva
  - Critérios de aceitação (mínimo 5)
  - Fluxo principal (passo a passo)
  - Fluxos alternativos (mínimo 2)
  - Regras de negócio relacionadas

**Passo 3 - Revisão Interna (20min):**
- Revisar documentação do grupo
- Verificar completude de cada campo
- Corrigir erros de português
- Garantir clareza e objetividade

**Parte do Projeto Construída:** Requisitos funcionais formalmente documentados

---

### **Tópico 3: Estruturação de Requisitos Não Funcionais (50min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Apresentação com Métricas:**  

**Importância das Métricas:**
- RNF sem métrica = não testável
- Métrica deve ser objetiva e mensurável
- Exemplos ruins: "rápido", "seguro", "fácil de usar"
- Exemplos bons: "< 2s", "criptografia TLS 1.2+", "máximo 3 cliques"

**Categorias de RNF no MeetStranger:**
1. **Desempenho:** Tempo de resposta, latência, throughput
2. **Segurança:** Criptografia, autenticação, proteção de dados
3. **Usabilidade:** Facilidade de uso, acessibilidade, feedback
4. **Confiabilidade:** Disponibilidade, recuperação de falhas
5. **Manutenibilidade:** Qualidade de código, documentação
6. **Portabilidade:** iOS, Android, diferentes dispositivos

#### 📌 Atividade Prática 3:
🎯 **Objetivo:** Documentar requisitos não funcionais  
📝 **Tarefa:**  
- **Metodologia Ativa - Documentação por Categoria:**  

**Redistribuição de Grupos:**
Cada grupo foca em uma categoria de RNF:
- **Grupo 1:** Desempenho e Escalabilidade
- **Grupo 2:** Segurança e Privacidade
- **Grupo 3:** Usabilidade e Acessibilidade
- **Grupo 4:** Confiabilidade e Disponibilidade
- **Grupo 5:** Manutenibilidade e Portabilidade

**Tarefa (30min):**
1. Revisar RNF levantados na aula 4
2. Selecionar 5 RNF da sua categoria
3. Documentar cada um com:
   - ID, Categoria, Título, Prioridade
   - Descrição clara
   - Métrica mensurável (OBRIGATÓRIO)
   - Como testar
   - Impacto se não atendido
   - Relacionamentos com RF

**Exemplos de Métricas:**
- Desempenho: "< 2s para 95% das requisições"
- Segurança: "100% das senhas com hash bcrypt cost ≥ 10"
- Usabilidade: "Usuário completa cadastro em < 2 minutos"
- Confiabilidade: "95% de uptime mensal"

**Parte do Projeto Construída:** Requisitos não funcionais com métricas

---

### **Tópico 4: Revisão Coletiva e Matriz de Rastreabilidade (35min)**
#### 📌 Demonstração Prática:
**Metodologia Ativa - Revisão por Pares:**  

**O que é Matriz de Rastreabilidade?**
- Relaciona requisitos com outros artefatos
- Garante que nada foi esquecido
- Facilita gestão de mudanças
- Conecta RF com RNF, casos de uso, testes

**Exemplo de Matriz:**
| RF | RNF Relacionados | Caso de Uso | UC do Curso | Prioridade |
|----|------------------|-------------|-------------|------------|
| RF01 | RNF07, RNF10 | UC01 | UC 02-3, 02-4 | Must |
| RF02 | RNF01, RNF08 | UC02 | UC 02-3, 02-4 | Must |

#### 📌 Atividade Prática 4:
🎯 **Objetivo:** Validar e relacionar requisitos  
📝 **Tarefa:**  
- **Metodologia Ativa - Peer Review e Consolidação:**  

**Passo 1 - Troca de Documentos (5min):**
- Grupos trocam documentos entre si
- Grupo 1 ↔ Grupo 2
- Grupo 3 ↔ Grupo 4
- Grupo 5 revisa todos

**Passo 2 - Revisão (15min):**
Verificar no documento recebido:
- ✓ Todos os campos estão preenchidos?
- ✓ Descrições estão claras?
- ✓ Critérios de aceitação são testáveis?
- ✓ RNF têm métricas mensuráveis?
- ✓ Priorização faz sentido?
- ✓ Português está correto?

**Passo 3 - Feedback (10min):**
- Anotar melhorias sugeridas
- Devolver documento com comentários
- Grupo original faz ajustes

**Passo 4 - Matriz (5min):**
- Docente apresenta matriz consolidada
- Grupos identificam relacionamentos
- Discussão sobre dependências

**Parte do Projeto Construída:** Documentação revisada e validada

---

### Encerramento e Reflexão (20min)
#### 📌 Discussão em grupo:
**Metodologia Ativa - Galeria de Documentação:**  
- Cada grupo apresenta 1 requisito bem documentado (2min cada)
- Turma aplaude o melhor documentado
- Docente destaca pontos fortes de cada grupo
- Discussão: "Como essa documentação vai nos ajudar nas próximas UCs?"

#### 📌 Desafio para a próxima aula:
**Metodologia Ativa - Refinamento Contínuo:**  
Cada grupo deve:
1. Aplicar feedback recebido
2. Completar documentação de TODOS os requisitos do seu módulo
3. Revisar português e formatação
4. Preparar para apresentação final na próxima aula
5. Pensar em regras de negócio relacionadas

---

### 📌 Objetos de Aprendizagem
📝 **Materiais Didáticos Utilizados:**  
- Template de documentação de requisitos
- Exemplos de requisitos bem e mal documentados
- Documento de requisitos do MeetStranger (referência)
- Guia de priorização MoSCoW
- Template de matriz de rastreabilidade

---

## 🎯 Avaliação

### **Avaliação Formativa (Durante a aula):**
✅ Qualidade da documentação produzida  
✅ Completude dos campos obrigatórios  
✅ Clareza e objetividade das descrições  
✅ Presença de métricas nos RNF  
✅ Participação na revisão por pares  
✅ Aplicação do feedback recebido  

### **Avaliação Somativa (Entregáveis):**
✅ 5 Requisitos Funcionais documentados (em grupo)  
✅ 5 Requisitos Não Funcionais documentados (em grupo)  
✅ Documento revisado e validado  
✅ Feedback de revisão por pares  

### **Critérios de Qualidade:**
- **Excelente (9-10):** Documentação completa, profissional, todos os campos preenchidos corretamente, métricas claras, sem erros de português, priorização coerente  
- **Bom (7-8):** Documentação adequada, campos principais preenchidos, métricas presentes, poucos erros, priorização razoável  
- **Satisfatório (6-7):** Documentação básica, alguns campos faltando, métricas vagas, alguns erros, priorização simples  
- **Insatisfatório (<6):** Documentação incompleta, muitos campos vazios, sem métricas, muitos erros, sem priorização  

---

## 🎓 Conclusão

### **Aprendizado Esperado:**
🎯 **Conhecimento Técnico:**  
- Padrões profissionais de documentação de requisitos
- Estrutura completa de RF e RNF
- Método MoSCoW de priorização
- Conceito de matriz de rastreabilidade
- Importância de métricas mensuráveis

🎯 **Aplicação Prática:**  
- Documentação formal de requisitos do MeetStranger
- Uso de templates profissionais
- Revisão por pares
- Relacionamento entre requisitos
- Organização de documentação técnica

🎯 **Competências Profissionais:**  
- Documentação técnica profissional
- Trabalho colaborativo
- Revisão crítica
- Atenção a detalhes
- Comunicação escrita clara

### **Conexão com o Projeto:**  
Esta aula transforma os requisitos levantados em documentação profissional que será usada em TODAS as próximas UCs. Cada desenvolvedor, testador e designer usará este documento como guia.

### **Preparação para Próxima Aula:**  
Na próxima aula (com Mateus), continuaremos refinando a documentação, adicionaremos regras de negócio detalhadas e criaremos casos de uso. Os grupos devem finalizar a documentação dos requisitos do seu módulo.

---

## 📝 Observações para o Docente

### Preparação Prévia
- Preparar template de documentação no Google Docs
- Criar exemplos de requisitos bem e mal documentados
- Revisar documento de requisitos do MeetStranger
- Preparar matriz de rastreabilidade inicial
- Testar compartilhamento de documentos

### Durante a Aula
- Circular entre grupos auxiliando na documentação
- Dar exemplos práticos de cada campo
- Mostrar como buscar informações no briefing
- Garantir que todos os grupos estão progredindo
- Tirar prints dos documentos em progresso

### Após a Aula
- Consolidar todos os documentos em um único
- Revisar e dar feedback individual por grupo
- Identificar requisitos faltantes
- Preparar material para próxima aula
- Compartilhar versão consolidada com a turma

### Dicas Importantes
- Enfatizar que documentação é trabalho contínuo
- Mostrar que documentação economiza tempo depois
- Dar exemplos de problemas por falta de documentação
- Celebrar boa documentação produzida
- Ser paciente - documentar é difícil no início
