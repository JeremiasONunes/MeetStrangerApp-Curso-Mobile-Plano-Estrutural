# Aula 01 - Contexto do Projeto e Fundamentos da Lógica de Programação

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 01 - Lógica de Programação  
**Carga Horária:** 4 horas  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Retomar** o planejamento realizado na UC 1 e conectá-lo com a fase de desenvolvimento
2. **Compreender** o papel fundamental da lógica de programação no desenvolvimento mobile
3. **Identificar** e aplicar o conceito de algoritmo no contexto do projeto MeetStranger
4. **Relacionar** sequências lógicas com funcionalidades reais do sistema

---

## 📚 Conteúdos Programáticos

### 1. Apresentação da Parte 1 da UC 2 (30 min)
- Visão geral da UC 02 e suas 4 partes
- Objetivos da Parte 1: Lógica de Programação
- Cronograma das 9 aulas
- Metodologia de trabalho e avaliação

### 2. Revisão do Contexto do Projeto MeetStranger (45 min)
- Retomada do briefing e requisitos da UC 1
- Funcionalidades principais do sistema
- Regras de negócio essenciais
- Fluxos de usuário planejados

### 3. Conceito de Algoritmo (60 min)
- Definição formal e informal de algoritmo
- Características de um bom algoritmo
- Algoritmos no cotidiano vs. algoritmos computacionais
- Formas de representação (linguagem natural, fluxograma, pseudocódigo)

### 4. Sequência Lógica de Instruções (45 min)
- Conceito de sequência lógica
- Importância da ordem das instruções
- Entrada → Processamento → Saída
- Aplicação prática no MeetStranger

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Acolhimento e Contextualização (30 min)

**Atividade:** Dinâmica de Retomada
- Apresentação dos objetivos da aula
- Discussão em grupo: "O que vocês lembram do planejamento da UC 1?"
- Mapeamento coletivo das funcionalidades do MeetStranger no quadro

**Recursos:**
- Projetor/TV
- Quadro branco
- Documentação da UC 1

### Momento 2: Revisão do Projeto MeetStranger (45 min)

**Atividade:** Análise Colaborativa
- Apresentação em slides do projeto completo
- Discussão orientada sobre cada funcionalidade
- Identificação dos principais fluxos do sistema

**Perguntas Norteadoras:**
- Quais são as funcionalidades principais do MeetStranger?
- Como um usuário se cadastra no sistema?
- Quais validações são necessárias?
- Como funciona o matching entre usuários?

**Recursos:**
- Slides do projeto
- Documentação de requisitos
- Protótipos (se disponíveis)

### Momento 3: Conceito de Algoritmo (60 min)

**Atividade 1:** Algoritmos do Cotidiano (20 min)
- Dividir turma em grupos de 3-4 pessoas
- Cada grupo descreve um algoritmo do dia a dia:
  - Fazer um café
  - Trocar uma lâmpada
  - Fazer login em um app
- Apresentação e discussão das soluções

**Atividade 2:** Formalização do Conceito (20 min)
- Exposição dialogada sobre algoritmos
- Características essenciais:
  - Finitude
  - Definição clara
  - Entrada e saída
  - Efetividade
- Formas de representação

**Atividade 3:** Primeiro Algoritmo Computacional (20 min)
- Exemplo prático: "Validar se um email é válido"
- Representação em linguagem natural
- Discussão sobre precisão e clareza

**Recursos:**
- Slides explicativos
- Exemplos práticos
- Quadro para construção coletiva

### Momento 4: Sequência Lógica de Instruções (45 min)

**Atividade 1:** Exercício Prático Individual (15 min)
- Descrever em linguagem natural o algoritmo:
  - "Cadastrar um novo usuário no MeetStranger"
- Identificar entrada, processamento e saída

**Atividade 2:** Análise Coletiva (20 min)
- Voluntários apresentam suas soluções
- Discussão sobre diferentes abordagens
- Identificação de problemas comuns:
  - Falta de validações
  - Ordem incorreta de passos
  - Instruções ambíguas

**Atividade 3:** Refinamento (10 min)
- Construção coletiva do algoritmo correto
- Registro no quadro
- Comparação com requisitos da UC 1

**Recursos:**
- Folhas de exercício
- Quadro branco
- Documentação de requisitos

### Momento 5: Fechamento e Avaliação (30 min)

**Atividade:** Síntese e Reflexão
- Recapitulação dos conceitos principais
- Conexão com a próxima aula
- Exercício para casa

**Perguntas de Reflexão:**
- O que é um algoritmo?
- Por que a ordem das instruções é importante?
- Como a lógica se relaciona com o desenvolvimento mobile?

---

## 📝 Atividades Práticas

### Atividade em Aula: Algoritmo de Cadastro

**Objetivo:** Aplicar conceitos de algoritmo e sequência lógica

**Enunciado:**
Descreva em linguagem natural (passo a passo) o algoritmo completo para cadastrar um novo usuário no MeetStranger, considerando:
- Dados necessários: username, email, senha
- Validações: email válido, senha forte (mínimo 6 caracteres)
- Verificação: email já cadastrado
- Resultado: sucesso ou erro com mensagem

**Exemplo de Solução:**
```
ALGORITMO: Cadastrar Usuário

ENTRADA:
- username (texto)
- email (texto)
- senha (texto)

PROCESSAMENTO:
1. Receber username, email e senha do usuário
2. Verificar se username está vazio
   - Se SIM: exibir erro "Username obrigatório" e PARAR
3. Verificar se email está vazio
   - Se SIM: exibir erro "Email obrigatório" e PARAR
4. Verificar se email contém "@" e "."
   - Se NÃO: exibir erro "Email inválido" e PARAR
5. Verificar se senha tem pelo menos 6 caracteres
   - Se NÃO: exibir erro "Senha deve ter no mínimo 6 caracteres" e PARAR
6. Consultar banco de dados para verificar se email já existe
   - Se SIM: exibir erro "Email já cadastrado" e PARAR
7. Criptografar a senha
8. Salvar usuário no banco de dados
9. Gerar token de autenticação
10. Exibir mensagem "Cadastro realizado com sucesso!"

SAÍDA:
- Mensagem de sucesso ou erro
- Token de autenticação (se sucesso)
```

### Exercício para Casa

**Título:** Algoritmos do MeetStranger

**Instruções:**
Escolha UMA das funcionalidades abaixo e descreva o algoritmo completo em linguagem natural:

1. **Login de Usuário**
   - Entrada: email e senha
   - Validações necessárias
   - Verificação de credenciais
   - Resultado: acesso permitido ou negado

2. **Selecionar Tópico de Conversa**
   - Entrada: categoria escolhida (Filmes, Jogos ou Séries)
   - Processamento: entrar na fila de matching
   - Resultado: aguardar conexão

3. **Enviar Mensagem no Chat**
   - Entrada: texto da mensagem
   - Validações: mensagem não vazia, usuário conectado
   - Processamento: enviar para o parceiro
   - Resultado: mensagem entregue

**Formato de Entrega:**
- Documento de texto (.txt, .doc ou .pdf)
- Estrutura: ENTRADA → PROCESSAMENTO → SAÍDA
- Mínimo 10 passos detalhados
- Incluir validações e tratamento de erros

**Prazo:** Trazer na próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica (Início da Aula)
- Discussão sobre conhecimentos prévios
- Identificação do nível de compreensão sobre lógica

### Avaliação Formativa (Durante a Aula)
- Observação da participação nas atividades
- Qualidade das soluções propostas nos exercícios
- Capacidade de trabalhar em grupo

**Critérios:**
- Compreensão do conceito de algoritmo
- Clareza na descrição de sequências lógicas
- Identificação de entrada, processamento e saída
- Participação ativa nas discussões

### Avaliação Somativa (Exercício para Casa)
- Algoritmo completo e bem estruturado
- Presença de validações
- Sequência lógica correta
- Clareza na descrição

**Peso:** 10% da nota da Parte 1

---

## 🎯 Indicadores de Desempenho

O estudante demonstra compreensão quando:

✅ Explica com clareza o que é um algoritmo  
✅ Identifica entrada, processamento e saída em um problema  
✅ Descreve sequências lógicas de forma ordenada  
✅ Relaciona lógica de programação com funcionalidades do MeetStranger  
✅ Identifica a necessidade de validações em algoritmos  
✅ Participa ativamente das discussões e atividades  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Computador com projetor/TV
- [ ] Slides da aula
- [ ] Quadro branco e marcadores
- [ ] Documentação do projeto MeetStranger (UC 1)
- [ ] Folhas de exercício impressas
- [ ] Acesso à internet

### Materiais de Apoio
- Documentação de requisitos do MeetStranger
- Exemplos de algoritmos do cotidiano
- Diagramas de fluxo simples
- Glossário de termos técnicos

### Referências Bibliográficas
- FORBELLONE, A. L. V.; EBERSPÄCHER, H. F. **Lógica de Programação**. 3ª ed. Pearson, 2005.
- MANZANO, J. A. N. G.; OLIVEIRA, J. F. **Algoritmos: Lógica para Desenvolvimento de Programação de Computadores**. 28ª ed. Érica, 2016.
- CORMEN, T. H. et al. **Algoritmos: Teoria e Prática**. 3ª ed. Campus, 2012.

### Links Úteis
- Documentação do projeto: `/material do curso/documentacao-projeto/`
- Visualizador de algoritmos: https://visualgo.net/
- Exercícios online: https://www.beecrowd.com.br/

---

## 🔄 Conexão com Outras Aulas

### Pré-requisitos
- UC 01 completa (Planejamento)
- Conhecimento básico de informática
- Familiaridade com o projeto MeetStranger

### Preparação para Próxima Aula
A Aula 02 aprofundará:
- Estruturação de algoritmos mais complexos
- Representação em pseudocódigo
- Resolução de problemas computacionais aplicados ao MeetStranger

**Dica para o Docente:** Revisar os exercícios para casa antes da Aula 02 para identificar dificuldades comuns e ajustar o conteúdo.

---

## 💡 Dicas para o Docente

### Antes da Aula
1. Revisar toda a documentação da UC 1
2. Preparar exemplos práticos do MeetStranger
3. Testar equipamentos (projetor, computador)
4. Imprimir folhas de exercício
5. Preparar ambiente colaborativo

### Durante a Aula
1. Manter clima acolhedor e participativo
2. Usar exemplos do cotidiano antes de conceitos técnicos
3. Incentivar perguntas e discussões
4. Circular pela sala durante atividades em grupo
5. Fazer conexões constantes com o projeto real

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 45 min
- ⏰ Momento 3: 60 min (incluir intervalo de 10 min)
- ⏰ Momento 4: 45 min
- ⏰ Momento 5: 30 min
- **Total:** 4 horas (240 min)

### Adaptações Possíveis
- Se a turma tiver dificuldade: reduzir complexidade dos exemplos
- Se a turma avançar rápido: incluir exercícios extras
- Para turmas grandes: usar ferramentas colaborativas online
- Para EAD: adaptar atividades para fóruns e videoconferência

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Slides preparados e testados
- [ ] Documentação da UC 1 revisada
- [ ] Exercícios impressos
- [ ] Equipamentos testados
- [ ] Ambiente organizado

### Durante a Aula
- [ ] Apresentar objetivos claramente
- [ ] Realizar todas as atividades planejadas
- [ ] Observar participação dos estudantes
- [ ] Fazer anotações sobre dificuldades
- [ ] Entregar exercício para casa

### Após a Aula
- [ ] Registrar frequência
- [ ] Anotar observações sobre a turma
- [ ] Preparar feedback para próxima aula
- [ ] Revisar exercícios entregues
- [ ] Ajustar planejamento se necessário

---

## 📝 Observações e Ajustes

**Espaço para anotações do docente:**

```
Data da aplicação: ___/___/______

Pontos positivos:
- 
- 

Dificuldades encontradas:
- 
- 

Ajustes necessários para próxima turma:
- 
- 

Tempo real gasto por atividade:
- Momento 1: _____ min
- Momento 2: _____ min
- Momento 3: _____ min
- Momento 4: _____ min
- Momento 5: _____ min
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
