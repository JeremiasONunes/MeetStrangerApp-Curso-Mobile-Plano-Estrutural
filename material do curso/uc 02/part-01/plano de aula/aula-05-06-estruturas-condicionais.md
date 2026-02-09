# Aula 05-06 - Estruturas Condicionais e Controle de Decisão

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 01 - Lógica de Programação  
**Carga Horária:** 8 horas (2 aulas de 4h)  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final destas aulas, o estudante será capaz de:

1. **Controlar** o fluxo de execução usando estruturas condicionais
2. **Aplicar** SE, SENÃO e SENÃO SE em algoritmos
3. **Implementar** regras de negócio do MeetStranger
4. **Criar** validações complexas com condições aninhadas

---

## 📚 Conteúdos Programáticos

### AULA 05 (4 horas)

#### 1. Estrutura SE (IF) - 60 min
- Conceito de decisão em algoritmos
- Sintaxe básica do SE
- Condições simples
- Bloco de comandos

#### 2. Estrutura SE-SENÃO (IF-ELSE) - 60 min
- Decisões binárias
- Fluxo alternativo
- Aplicações práticas

#### 3. Estrutura SE-SENÃO SE (IF-ELSE IF) - 60 min
- Múltiplas condições
- Encadeamento de decisões
- Ordem de avaliação

#### 4. Prática Guiada - 60 min
- Validações do MeetStranger
- Exercícios orientados

### AULA 06 (4 horas)

#### 1. Condições Aninhadas - 60 min
- SE dentro de SE
- Níveis de profundidade
- Boas práticas

#### 2. Regras de Negócio - 90 min
- Análise de requisitos
- Tradução para algoritmos
- Implementação completa

#### 3. Projeto Prático - 90 min
- Sistema de validação completo
- Trabalho em grupos
- Apresentação

---

## 🎓 AULA 05 - Estratégias de Ensino

### Momento 1: Retomada e Introdução (30 min)

**Atividade:** Problema Motivador
```
Situação: Usuário tenta fazer login
- Se credenciais corretas → permitir acesso
- Se credenciais incorretas → negar acesso

Como implementar essa decisão?
```

**Discussão:**
- Até agora: algoritmos lineares
- Agora: algoritmos com decisões

### Momento 2: Estrutura SE (60 min)

**Atividade 1:** Conceito e Sintaxe (20 min)
```
SE condição ENTÃO
  // comandos executados se condição for VERDADEIRA
FIM_SE

Exemplo:
SE idade >= 13 ENTÃO
  ESCREVER "Idade válida"
FIM_SE
```

**Atividade 2:** Fluxograma Visual (15 min)
- Desenhar fluxo de decisão no quadro
- Mostrar caminho VERDADEIRO
- Mostrar caminho quando FALSO (nada acontece)

**Atividade 3:** Exercícios Práticos (25 min)
```
1. Verificar se username tem 3+ caracteres
2. Verificar se email contém @
3. Verificar se usuário está online
4. Verificar se sala está cheia
```

### Momento 3: Estrutura SE-SENÃO (60 min)

**Atividade 1:** Apresentação (20 min)
```
SE condição ENTÃO
  // comandos se VERDADEIRO
SENÃO
  // comandos se FALSO
FIM_SE

Exemplo:
SE senha_correta ENTÃO
  ESCREVER "Login realizado"
  GERAR_TOKEN()
SENÃO
  ESCREVER "Senha incorreta"
  INCREMENTAR_TENTATIVAS()
FIM_SE
```

**Atividade 2:** Comparação SE vs SE-SENÃO (15 min)
- Quando usar cada um
- Vantagens do SENÃO
- Exemplos práticos

**Atividade 3:** Exercício em Duplas (25 min)
```
Criar algoritmo: Verificar disponibilidade de username
- Se disponível: permitir cadastro
- Se indisponível: sugerir alternativas
```

### Momento 4: Estrutura SE-SENÃO SE (60 min + 10 min intervalo)

**Atividade 1:** Múltiplas Condições (25 min)
```
SE condição1 ENTÃO
  // comandos 1
SENÃO SE condição2 ENTÃO
  // comandos 2
SENÃO SE condição3 ENTÃO
  // comandos 3
SENÃO
  // comandos padrão
FIM_SE

Exemplo: Classificar força da senha
SE tamanho < 6 ENTÃO
  ESCREVER "Senha fraca"
SENÃO SE tamanho < 10 ENTÃO
  ESCREVER "Senha média"
SENÃO
  ESCREVER "Senha forte"
FIM_SE
```

**Atividade 2:** Ordem de Avaliação (15 min)
- Primeira condição verdadeira executa
- Demais são ignoradas
- Importância da ordem

**Atividade 3:** Exercício Guiado (20 min)
```
Categorizar usuário por atividade:
- 0 conversas: "Novo"
- 1-5 conversas: "Iniciante"
- 6-20 conversas: "Ativo"
- 21+ conversas: "Veterano"
```

### Momento 5: Prática e Fechamento (60 min)

**Atividade 1:** Validação de Cadastro (30 min)
- Implementar validação completa
- Usar todas as estruturas aprendidas
- Trabalho individual

**Atividade 2:** Análise Coletiva (20 min)
- Voluntários apresentam soluções
- Discussão sobre diferentes abordagens
- Identificar melhorias

**Atividade 3:** Síntese (10 min)
- Recapitular estruturas
- Exercício para próxima aula

---

## 🎓 AULA 06 - Estratégias de Ensino

### Momento 1: Retomada e Correção (30 min)

**Atividade:** Revisão do Exercício
- Correção coletiva
- Discussão de dúvidas
- Preparação para condições aninhadas

### Momento 2: Condições Aninhadas (60 min)

**Atividade 1:** Conceito de Aninhamento (20 min)
```
SE usuario_autenticado ENTÃO
  SE em_sala ENTÃO
    SE sala_ativa ENTÃO
      PERMITIR_ENVIAR_MENSAGEM()
    SENÃO
      ESCREVER "Sala inativa"
    FIM_SE
  SENÃO
    ESCREVER "Entre em uma sala primeiro"
  FIM_SE
SENÃO
  ESCREVER "Faça login primeiro"
FIM_SE
```

**Atividade 2:** Boas Práticas (15 min)
- Evitar aninhamento excessivo (máx 3 níveis)
- Usar operadores lógicos quando possível
- Clareza vs. complexidade

**Atividade 3:** Refatoração (25 min)
```
// Aninhado (ruim)
SE A ENTÃO
  SE B ENTÃO
    SE C ENTÃO
      EXECUTAR()
    FIM_SE
  FIM_SE
FIM_SE

// Refatorado (melhor)
SE A E B E C ENTÃO
  EXECUTAR()
FIM_SE
```

### Momento 3: Regras de Negócio (90 min + 10 min intervalo)

**Atividade 1:** Análise de Requisitos (30 min)
- Apresentar requisitos do MeetStranger
- Identificar regras de negócio
- Traduzir para condições

**Regras do MeetStranger:**
```
1. Cadastro:
   - Username: 3-20 caracteres, único
   - Email: formato válido, único
   - Senha: 6+ caracteres, letra + número
   - Idade: 13+ anos

2. Login:
   - Credenciais corretas
   - Máximo 3 tentativas
   - Bloquear após 3 falhas

3. Matching:
   - Usuário autenticado
   - Não estar em outra sala
   - Categoria válida
   - Fila não vazia

4. Chat:
   - Estar em sala ativa
   - Mensagem não vazia
   - Não estar bloqueado
```

**Atividade 2:** Implementação em Grupos (40 min)
- Grupo 1: Sistema de cadastro completo
- Grupo 2: Sistema de login com tentativas
- Grupo 3: Sistema de matching
- Grupo 4: Sistema de envio de mensagens

**Atividade 3:** Apresentação (20 min)
- Cada grupo apresenta (5 min cada)
- Feedback da turma

### Momento 4: Projeto Prático (90 min)

**Atividade:** Sistema de Validação Completo
- Criar módulo de validação do MeetStranger
- Incluir todas as regras de negócio
- Testar com diferentes cenários
- Documentar decisões

**Estrutura:**
```
1. Análise (20 min)
2. Planejamento (20 min)
3. Implementação (40 min)
4. Apresentação (10 min)
```

### Momento 5: Fechamento e Avaliação (30 min)

**Atividade:** Síntese Final
- Recapitular todas as estruturas
- Discussão sobre aprendizados
- Exercício final para casa

---

## 📝 Atividades Práticas

### AULA 05 - Atividade 1: Validação Simples

```
ALGORITMO Validar_Username
INÍCIO
  DECLARAR username: TEXT
  DECLARAR tamanho: INTEGER
  
  CONSTANTE MIN_TAMANHO: INTEGER = 3
  
  LER username
  tamanho ← TAMANHO(username)
  
  SE tamanho >= MIN_TAMANHO ENTÃO
    ESCREVER "Username válido"
  FIM_SE
FIM
```

### AULA 05 - Atividade 2: Login com SE-SENÃO

```
ALGORITMO Login_Usuario
INÍCIO
  DECLARAR email, senha: TEXT
  DECLARAR usuario_existe, senha_correta: BOOLEAN
  
  LER email, senha
  
  usuario_existe ← BUSCAR_NO_BANCO(email)
  
  SE usuario_existe ENTÃO
    senha_correta ← VERIFICAR_SENHA(senha)
    
    SE senha_correta ENTÃO
      ESCREVER "Login realizado com sucesso!"
      GERAR_TOKEN()
      REDIRECIONAR_HOME()
    SENÃO
      ESCREVER "Senha incorreta"
    FIM_SE
  SENÃO
    ESCREVER "Usuário não encontrado"
  FIM_SE
FIM
```

### AULA 05 - Atividade 3: Classificação com SE-SENÃO SE

```
ALGORITMO Classificar_Senha
INÍCIO
  DECLARAR senha: TEXT
  DECLARAR tamanho: INTEGER
  DECLARAR tem_letra, tem_numero, tem_especial: BOOLEAN
  
  LER senha
  tamanho ← TAMANHO(senha)
  tem_letra ← CONTEM_LETRA(senha)
  tem_numero ← CONTEM_NUMERO(senha)
  tem_especial ← CONTEM_ESPECIAL(senha)
  
  SE tamanho < 6 ENTÃO
    ESCREVER "Senha muito fraca - mínimo 6 caracteres"
  SENÃO SE NÃO tem_letra OU NÃO tem_numero ENTÃO
    ESCREVER "Senha fraca - adicione letras e números"
  SENÃO SE NÃO tem_especial ENTÃO
    ESCREVER "Senha média - adicione caractere especial"
  SENÃO
    ESCREVER "Senha forte!"
  FIM_SE
FIM
```

### AULA 06 - Atividade 1: Sistema de Cadastro Completo

```
ALGORITMO Cadastro_Completo
INÍCIO
  // VARIÁVEIS
  DECLARAR username, email, senha: TEXT
  DECLARAR idade: INTEGER
  DECLARAR erros: INTEGER
  
  // CONSTANTES
  CONSTANTE MIN_USERNAME: INTEGER = 3
  CONSTANTE MAX_USERNAME: INTEGER = 20
  CONSTANTE MIN_SENHA: INTEGER = 6
  CONSTANTE MIN_IDADE: INTEGER = 13
  
  // ENTRADA
  LER username, email, senha, idade
  erros ← 0
  
  // VALIDAÇÃO USERNAME
  SE TAMANHO(username) < MIN_USERNAME ENTÃO
    ESCREVER "Erro: Username muito curto (mínimo 3)"
    erros ← erros + 1
  SENÃO SE TAMANHO(username) > MAX_USERNAME ENTÃO
    ESCREVER "Erro: Username muito longo (máximo 20)"
    erros ← erros + 1
  SENÃO SE BUSCAR_NO_BANCO("users", "username", username) ENTÃO
    ESCREVER "Erro: Username já existe"
    erros ← erros + 1
  FIM_SE
  
  // VALIDAÇÃO EMAIL
  SE NÃO CONTEM(email, "@") OU NÃO CONTEM(email, ".") ENTÃO
    ESCREVER "Erro: Email inválido"
    erros ← erros + 1
  SENÃO SE BUSCAR_NO_BANCO("users", "email", email) ENTÃO
    ESCREVER "Erro: Email já cadastrado"
    erros ← erros + 1
  FIM_SE
  
  // VALIDAÇÃO SENHA
  SE TAMANHO(senha) < MIN_SENHA ENTÃO
    ESCREVER "Erro: Senha muito curta (mínimo 6)"
    erros ← erros + 1
  SENÃO SE NÃO CONTEM_LETRA(senha) ENTÃO
    ESCREVER "Erro: Senha deve conter letras"
    erros ← erros + 1
  SENÃO SE NÃO CONTEM_NUMERO(senha) ENTÃO
    ESCREVER "Erro: Senha deve conter números"
    erros ← erros + 1
  FIM_SE
  
  // VALIDAÇÃO IDADE
  SE idade < MIN_IDADE ENTÃO
    ESCREVER "Erro: Idade mínima é 13 anos"
    erros ← erros + 1
  FIM_SE
  
  // RESULTADO
  SE erros = 0 ENTÃO
    SALVAR_NO_BANCO(username, email, senha, idade)
    ESCREVER "Cadastro realizado com sucesso!"
    ESCREVER "Bem-vindo, " + username + "!"
  SENÃO
    ESCREVER "Cadastro não realizado. Corrija os erros acima."
  FIM_SE
FIM
```

### AULA 06 - Atividade 2: Sistema de Login com Tentativas

```
ALGORITMO Login_Com_Tentativas
INÍCIO
  DECLARAR email, senha: TEXT
  DECLARAR tentativas, max_tentativas: INTEGER
  DECLARAR bloqueado, login_sucesso: BOOLEAN
  
  max_tentativas ← 3
  tentativas ← 0
  bloqueado ← VERIFICAR_BLOQUEIO(email)
  
  SE bloqueado ENTÃO
    ESCREVER "Conta bloqueada. Contate o suporte."
    FIM
  FIM_SE
  
  ENQUANTO tentativas < max_tentativas FAÇA
    LER email, senha
    tentativas ← tentativas + 1
    
    SE VERIFICAR_CREDENCIAIS(email, senha) ENTÃO
      ESCREVER "Login realizado com sucesso!"
      RESETAR_TENTATIVAS(email)
      GERAR_TOKEN()
      login_sucesso ← VERDADEIRO
      PARAR
    SENÃO
      SE tentativas < max_tentativas ENTÃO
        ESCREVER "Credenciais incorretas. Tentativa " + tentativas + " de " + max_tentativas
      SENÃO
        ESCREVER "Máximo de tentativas atingido. Conta bloqueada."
        BLOQUEAR_CONTA(email)
      FIM_SE
    FIM_SE
  FIM_ENQUANTO
FIM
```

### Exercício para Casa (Aula 05)

**Criar algoritmo: Validar Entrada na Fila de Matching**

Regras:
- Usuário deve estar autenticado
- Não pode estar em outra sala
- Categoria deve ser válida (Filmes, Jogos ou Séries)
- Se tudo OK, adicionar à fila e retornar posição

### Exercício para Casa (Aula 06)

**Criar sistema completo: Enviar Mensagem no Chat**

Regras:
- Usuário autenticado
- Estar em sala ativa
- Mensagem não vazia
- Mensagem <= 500 caracteres
- Não estar bloqueado
- Sala não estar pausada

Incluir todas as validações e mensagens de erro apropriadas.

---

## 📊 Avaliação

### Avaliação Diagnóstica (Aula 05)
- Compreensão de expressões lógicas
- Capacidade de identificar decisões

### Avaliação Formativa

**Critérios:**
- ✅ Usa SE corretamente
- ✅ Aplica SE-SENÃO adequadamente
- ✅ Implementa SE-SENÃO SE
- ✅ Cria condições aninhadas quando necessário
- ✅ Traduz regras de negócio em código
- ✅ Escreve código claro e organizado

**Instrumentos:**
- Exercícios práticos individuais
- Atividades em grupo
- Projeto prático
- Participação

### Avaliação Somativa

**Aula 05:**
- Exercícios em aula: 40%
- Exercício para casa: 60%

**Aula 06:**
- Projeto em grupo: 50%
- Exercício para casa: 50%

**Peso das Aulas:** 25% da nota da Parte 1

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Identifica quando usar estruturas condicionais  
✅ Implementa SE, SENÃO e SENÃO SE corretamente  
✅ Cria condições aninhadas de forma organizada  
✅ Traduz regras de negócio em algoritmos  
✅ Valida dados usando condições  
✅ Escreve código legível e bem estruturado  
✅ Testa diferentes cenários  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Projetor/TV
- [ ] Slides com fluxogramas
- [ ] Quadro branco
- [ ] Folhas para exercícios
- [ ] Documentação de requisitos
- [ ] Cartões com cenários de teste

### Fluxogramas de Referência

```
SE simples:
┌─────────┐
│ Início  │
└────┬────┘
     │
┌────▼────┐
│Condição?│
└─┬────┬──┘
  │Sim │Não
  │    └──────┐
┌─▼──┐        │
│Ação│        │
└─┬──┘        │
  └────┬──────┘
       │
  ┌────▼────┐
  │   Fim   │
  └─────────┘

SE-SENÃO:
┌─────────┐
│ Início  │
└────┬────┘
     │
┌────▼────┐
│Condição?│
└─┬────┬──┘
  │Sim │Não
┌─▼──┐ │
│Ação│ │
│ 1  │ │
└─┬──┘ │
  │  ┌─▼──┐
  │  │Ação│
  │  │ 2  │
  │  └─┬──┘
  └────┼───┘
       │
  ┌────▼────┐
  │   Fim   │
  └─────────┘
```

### Referências
- FORBELLONE, A. L. V. **Lógica de Programação**. Cap. 5.
- MANZANO, J. A. N. G. **Algoritmos**. Cap. 4-5.

---

## 🔄 Conexão com Outras Aulas

### Revisão das Aulas 01-04
- Algoritmos e pseudocódigo
- Variáveis e tipos
- Operadores e expressões lógicas

### Preparação para Aulas 07-08
- Estruturas de repetição (próximo tema)
- Loops com condições
- Validações iterativas

---

## 💡 Dicas para o Docente

### Gestão do Tempo

**Aula 05:**
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 60 min
- ⏰ Momento 4: 70 min (com intervalo)
- ⏰ Momento 5: 60 min

**Aula 06:**
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 100 min (com intervalo)
- ⏰ Momento 4: 90 min
- ⏰ Momento 5: 30 min

### Pontos de Atenção
1. **Indentação**: Enfatize importância visual
2. **FIM_SE**: Sempre fechar estruturas
3. **Aninhamento**: Máximo 3 níveis
4. **Ordem**: SE-SENÃO SE avalia em sequência
5. **Testes**: Sempre testar todos os caminhos

### Estratégias
- Use fluxogramas visuais
- Desenhe árvores de decisão
- Simule execução passo a passo
- Peça estudantes para "serem o computador"
- Mostre código real em JavaScript/TypeScript

### Adaptações
- **Turma iniciante**: Mais exemplos simples
- **Turma avançada**: Introduza switch/case
- **EAD**: Use ferramentas de visualização online

---

## 📋 Checklist do Docente

### Antes das Aulas
- [ ] Preparar slides com fluxogramas
- [ ] Criar exercícios práticos
- [ ] Revisar regras de negócio do MeetStranger
- [ ] Preparar cenários de teste
- [ ] Organizar grupos

### Durante Aula 05
- [ ] Ensinar SE
- [ ] Apresentar SE-SENÃO
- [ ] Explicar SE-SENÃO SE
- [ ] Conduzir práticas
- [ ] Entregar exercício

### Durante Aula 06
- [ ] Revisar exercício anterior
- [ ] Ensinar condições aninhadas
- [ ] Trabalhar regras de negócio
- [ ] Conduzir projeto prático
- [ ] Avaliar aprendizado

### Após as Aulas
- [ ] Registrar frequência
- [ ] Avaliar projetos
- [ ] Dar feedback individual
- [ ] Preparar próxima aula

---

## 📝 Observações e Ajustes

```
AULA 05
Data: ___/___/______

Compreensão:
- SE: ___/10
- SE-SENÃO: ___/10
- SE-SENÃO SE: ___/10

Dificuldades:
- 

Tempo real: _____ min

---

AULA 06
Data: ___/___/______

Compreensão:
- Aninhamento: ___/10
- Regras de negócio: ___/10
- Projeto prático: ___/10

Destaques:
- 

Ajustes:
- 
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
