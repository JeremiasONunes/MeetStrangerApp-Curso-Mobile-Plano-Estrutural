# Aula 04 - Operadores e Expressões Lógicas

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 01 - Lógica de Programação  
**Carga Horária:** 4 horas  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Aplicar** operadores aritméticos, relacionais e lógicos corretamente
2. **Construir** expressões lógicas coerentes e eficientes
3. **Combinar** diferentes tipos de operadores em expressões complexas
4. **Validar** dados usando expressões lógicas no contexto do MeetStranger

---

## 📚 Conteúdos Programáticos

### 1. Operadores Aritméticos (45 min)
- Adição, subtração, multiplicação, divisão
- Módulo (resto da divisão)
- Precedência de operadores
- Aplicações práticas

### 2. Operadores Relacionais (45 min)
- Igual, diferente
- Maior, menor, maior ou igual, menor ou igual
- Comparação entre tipos
- Resultado booleano

### 3. Operadores Lógicos (60 min)
- E (AND)
- OU (OR)
- NÃO (NOT)
- Tabelas verdade
- Combinação de condições

### 4. Expressões Complexas (60 min)
- Combinação de operadores
- Precedência e parênteses
- Validações compostas
- Aplicação em validações do MeetStranger

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Retomada e Introdução (30 min)

**Atividade:** Revisão + Problema Motivador
- Correção breve dos exercícios
- Apresentar situação: "Como validar se senha tem 6+ caracteres E contém número?"
- Discussão sobre necessidade de operadores

**Problema:**
```
Validar cadastro:
- Username tem 3+ caracteres
- Email contém @ e .
- Senha tem 6+ caracteres
- Idade >= 13

Como combinar todas essas condições?
```

### Momento 2: Operadores Aritméticos (45 min)

**Atividade 1:** Apresentação dos Operadores (15 min)
```
+ (Adição)        5 + 3 = 8
- (Subtração)     5 - 3 = 2
* (Multiplicação) 5 * 3 = 15
/ (Divisão)       5 / 2 = 2.5
% (Módulo)        5 % 2 = 1
```

**Atividade 2:** Precedência (10 min)
```
2 + 3 * 4 = ?
(2 + 3) * 4 = ?

Ordem: ( ) → * / % → + -
```

**Atividade 3:** Exercícios Práticos (20 min)
- Calcular tempo médio de conversa
- Calcular posição na fila
- Verificar se número é par (módulo)

**Exemplos do MeetStranger:**
```
// Calcular tempo total online em horas
tempo_minutos ← 150
tempo_horas ← tempo_minutos / 60  // 2.5

// Verificar se posição na fila é par
posicao ← 7
eh_par ← (posicao % 2) = 0  // FALSO

// Calcular média de mensagens por conversa
total_mensagens ← 45
total_conversas ← 9
media ← total_mensagens / total_conversas  // 5
```

### Momento 3: Operadores Relacionais (45 min)

**Atividade 1:** Apresentação (15 min)
```
=  (Igual)              idade = 18
<> (Diferente)          status <> "offline"
>  (Maior)              idade > 13
<  (Menor)              tentativas < 3
>= (Maior ou igual)     tamanho >= 6
<= (Menor ou igual)     posicao <= 10
```

**Atividade 2:** Comparações Práticas (15 min)
- Trabalho em duplas
- Criar 5 comparações para validações do sistema
- Apresentar soluções

**Atividade 3:** Exercício Guiado (15 min)
```
ALGORITMO Validar_Idade
  DECLARAR idade: INTEGER
  DECLARAR idade_valida: BOOLEAN
  
  LER idade
  
  idade_valida ← idade >= 13
  
  SE idade_valida ENTÃO
    ESCREVER "Idade válida"
  SENÃO
    ESCREVER "Idade mínima: 13 anos"
  FIM_SE
FIM
```

### Momento 4: Operadores Lógicos (60 min + 10 min intervalo)

**Atividade 1:** Conceito e Tabelas Verdade (20 min)

**Operador E (AND):**
```
VERDADEIRO E VERDADEIRO = VERDADEIRO
VERDADEIRO E FALSO = FALSO
FALSO E VERDADEIRO = FALSO
FALSO E FALSO = FALSO

Exemplo: usuario_existe E senha_correta
```

**Operador OU (OR):**
```
VERDADEIRO OU VERDADEIRO = VERDADEIRO
VERDADEIRO OU FALSO = VERDADEIRO
FALSO OU VERDADEIRO = VERDADEIRO
FALSO OU FALSO = FALSO

Exemplo: campo_vazio OU formato_invalido
```

**Operador NÃO (NOT):**
```
NÃO VERDADEIRO = FALSO
NÃO FALSO = VERDADEIRO

Exemplo: NÃO autenticado
```

**Atividade 2:** Exercícios com Tabelas Verdade (15 min)
- Resolver expressões lógicas
- Prever resultados
- Verificar respostas

**Atividade 3:** Aplicação Prática (25 min)
```
// Validar email
email_valido ← CONTEM(email, "@") E CONTEM(email, ".")

// Verificar se pode enviar mensagem
pode_enviar ← autenticado E em_sala E NÃO bloqueado

// Validar senha forte
senha_forte ← (tamanho >= 6) E (tem_letra E tem_numero)

// Verificar erro no cadastro
tem_erro ← username_vazio OU email_invalido OU senha_fraca
```

### Momento 5: Expressões Complexas e Validações (60 min)

**Atividade 1:** Precedência de Operadores (15 min)
```
Ordem de avaliação:
1. ( )
2. NÃO
3. E
4. OU

Exemplo:
A OU B E C = A OU (B E C)
(A OU B) E C = diferente!
```

**Atividade 2:** Validação Completa de Cadastro (25 min)
- Trabalho em grupos
- Criar expressão completa para validar cadastro
- Incluir todas as regras de negócio

**Atividade 3:** Apresentação e Refinamento (20 min)
- Grupos apresentam soluções
- Análise coletiva
- Identificar melhorias

---

## 📝 Atividades Práticas

### Atividade 1: Operadores Aritméticos

**Exercícios:**

1. Calcular tempo médio de conversa:
```
total_minutos ← 180
numero_conversas ← 6
media ← ?
```

2. Verificar se usuário está na primeira metade da fila:
```
posicao_usuario ← 5
tamanho_fila ← 12
primeira_metade ← posicao_usuario <= (tamanho_fila / 2)
```

3. Calcular quantas conversas completas de 10 minutos cabem:
```
tempo_disponivel ← 47
conversas_possiveis ← tempo_disponivel / 10  // 4
tempo_restante ← tempo_disponivel % 10       // 7
```

### Atividade 2: Validação de Email

```
ALGORITMO Validar_Email
INÍCIO
  DECLARAR email: TEXT
  DECLARAR tem_arroba: BOOLEAN
  DECLARAR tem_ponto: BOOLEAN
  DECLARAR tamanho_valido: BOOLEAN
  DECLARAR email_valido: BOOLEAN
  
  LER email
  
  tem_arroba ← CONTEM(email, "@")
  tem_ponto ← CONTEM(email, ".")
  tamanho_valido ← TAMANHO(email) >= 5
  
  email_valido ← tem_arroba E tem_ponto E tamanho_valido
  
  SE email_valido ENTÃO
    ESCREVER "Email válido"
  SENÃO
    SE NÃO tem_arroba ENTÃO
      ESCREVER "Email deve conter @"
    FIM_SE
    SE NÃO tem_ponto ENTÃO
      ESCREVER "Email deve conter ."
    FIM_SE
    SE NÃO tamanho_valido ENTÃO
      ESCREVER "Email muito curto"
    FIM_SE
  FIM_SE
FIM
```

### Atividade 3: Validação Completa de Cadastro

```
ALGORITMO Validar_Cadastro_Completo
INÍCIO
  // VARIÁVEIS
  DECLARAR username, email, senha: TEXT
  DECLARAR idade: INTEGER
  DECLARAR username_valido, email_valido, senha_valida, idade_valida: BOOLEAN
  DECLARAR cadastro_valido: BOOLEAN
  
  // CONSTANTES
  CONSTANTE MIN_USERNAME: INTEGER = 3
  CONSTANTE MIN_SENHA: INTEGER = 6
  CONSTANTE MIN_IDADE: INTEGER = 13
  
  // ENTRADA
  LER username, email, senha, idade
  
  // VALIDAÇÕES INDIVIDUAIS
  username_valido ← (TAMANHO(username) >= MIN_USERNAME) E (username <> "")
  
  email_valido ← CONTEM(email, "@") E CONTEM(email, ".") E (TAMANHO(email) >= 5)
  
  senha_valida ← (TAMANHO(senha) >= MIN_SENHA) E 
                 (CONTEM_LETRA(senha)) E 
                 (CONTEM_NUMERO(senha))
  
  idade_valida ← idade >= MIN_IDADE
  
  // VALIDAÇÃO GERAL
  cadastro_valido ← username_valido E email_valido E senha_valida E idade_valida
  
  // SAÍDA
  SE cadastro_valido ENTÃO
    ESCREVER "Cadastro válido! Processando..."
  SENÃO
    ESCREVER "Erros encontrados:"
    SE NÃO username_valido ENTÃO
      ESCREVER "- Username inválido (mínimo 3 caracteres)"
    FIM_SE
    SE NÃO email_valido ENTÃO
      ESCREVER "- Email inválido"
    FIM_SE
    SE NÃO senha_valida ENTÃO
      ESCREVER "- Senha fraca (mínimo 6 caracteres, letra e número)"
    FIM_SE
    SE NÃO idade_valida ENTÃO
      ESCREVER "- Idade mínima: 13 anos"
    FIM_SE
  FIM_SE
FIM
```

### Exercício para Casa

**Parte 1: Expressões Lógicas**

Resolva as expressões (V = Verdadeiro, F = Falso):

1. `V E F OU V` = ?
2. `(V E F) OU V` = ?
3. `V E (F OU V)` = ?
4. `NÃO (V E F)` = ?
5. `NÃO V OU NÃO F` = ?

**Parte 2: Validações do MeetStranger**

Crie expressões lógicas completas para:

1. **Validar Login:**
   - Email não vazio E formato válido
   - Senha não vazia E tamanho >= 6

2. **Verificar se pode enviar mensagem:**
   - Usuário autenticado
   - Está em uma sala
   - Sala está ativa
   - Não está bloqueado

3. **Validar entrada na fila:**
   - Usuário autenticado
   - Não está em outra sala
   - Categoria é válida (Filmes OU Jogos OU Séries)

**Parte 3: Algoritmo Completo**

Crie algoritmo de **Validar Senha Forte** usando:
- Operadores relacionais (>=, <=)
- Operadores lógicos (E, OU, NÃO)
- Validações: tamanho, letra, número, caractere especial

**Formato:**
```
ALGORITMO Validar_Senha_Forte
INÍCIO
  // Seu código aqui
FIM
```

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Conhecimento sobre operações matemáticas
- Compreensão de comparações

### Avaliação Formativa

**Critérios:**
- ✅ Usa operadores aritméticos corretamente
- ✅ Aplica operadores relacionais adequadamente
- ✅ Constrói expressões lógicas coerentes
- ✅ Combina operadores respeitando precedência
- ✅ Cria validações completas

**Instrumentos:**
- Exercícios práticos individuais
- Atividades em grupo
- Participação nas discussões

### Avaliação Somativa
- Exercícios em aula: 40%
- Exercício para casa: 60%

**Peso da Aula:** 15% da nota da Parte 1

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Aplica operadores aritméticos em cálculos  
✅ Usa operadores relacionais em comparações  
✅ Constrói expressões lógicas com E, OU, NÃO  
✅ Respeita precedência de operadores  
✅ Usa parênteses para clareza  
✅ Cria validações compostas eficientes  
✅ Resolve tabelas verdade corretamente  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Projetor/TV
- [ ] Slides com tabelas verdade
- [ ] Quadro branco
- [ ] Tabela de operadores impressa
- [ ] Exercícios práticos
- [ ] Calculadora (opcional)

### Tabela de Referência Rápida

```
┌─────────────────┬──────────┬──────────────────────┐
│ Tipo            │ Operador │ Exemplo              │
├─────────────────┼──────────┼──────────────────────┤
│ ARITMÉTICOS     │          │                      │
│                 │ +        │ 5 + 3 = 8            │
│                 │ -        │ 5 - 3 = 2            │
│                 │ *        │ 5 * 3 = 15           │
│                 │ /        │ 5 / 2 = 2.5          │
│                 │ %        │ 5 % 2 = 1            │
├─────────────────┼──────────┼──────────────────────┤
│ RELACIONAIS     │          │                      │
│                 │ =        │ idade = 18           │
│                 │ <>       │ status <> "off"      │
│                 │ >        │ idade > 13           │
│                 │ <        │ tentativas < 3       │
│                 │ >=       │ tamanho >= 6         │
│                 │ <=       │ posicao <= 10        │
├─────────────────┼──────────┼──────────────────────┤
│ LÓGICOS         │          │                      │
│                 │ E        │ V E V = V            │
│                 │ OU       │ F OU V = V           │
│                 │ NÃO      │ NÃO V = F            │
└─────────────────┴──────────┴──────────────────────┘

PRECEDÊNCIA: ( ) → NÃO → E → OU
```

### Referências
- FORBELLONE, A. L. V. **Lógica de Programação**. Cap. 4.
- MANZANO, J. A. N. G. **Algoritmos**. Cap. 3.

---

## 🔄 Conexão com Outras Aulas

### Revisão das Aulas 01-03
- Algoritmos e pseudocódigo
- Tipos de dados
- Variáveis e constantes

### Preparação para Aula 05
- Estruturas condicionais (próximo tema)
- Uso de expressões lógicas em SE/SENÃO
- Tomada de decisões

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 45 min
- ⏰ Momento 3: 45 min
- ⏰ Momento 4: 70 min (com intervalo)
- ⏰ Momento 5: 60 min

### Pontos de Atenção
1. **Precedência**: Enfatize uso de parênteses para clareza
2. **Tabelas Verdade**: Use exemplos visuais e práticos
3. **Operador E**: Ambos devem ser verdadeiros
4. **Operador OU**: Pelo menos um deve ser verdadeiro
5. **Validações**: Sempre relacione com o MeetStranger

### Estratégias
- Desenhe tabelas verdade no quadro
- Use cores diferentes para cada operador
- Faça exercícios passo a passo
- Peça para estudantes explicarem raciocínio
- Mostre erros comuns

### Adaptações
- **Turma iniciante**: Mais tempo em tabelas verdade
- **Turma avançada**: Introduza operador XOR
- **EAD**: Use ferramentas interativas online

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Preparar slides com tabelas verdade
- [ ] Imprimir tabela de operadores
- [ ] Criar exercícios práticos
- [ ] Revisar precedência de operadores
- [ ] Preparar exemplos do MeetStranger

### Durante a Aula
- [ ] Revisar exercício anterior
- [ ] Ensinar operadores aritméticos
- [ ] Apresentar operadores relacionais
- [ ] Explicar operadores lógicos
- [ ] Praticar expressões complexas
- [ ] Entregar exercício para casa

### Após a Aula
- [ ] Registrar frequência
- [ ] Avaliar exercícios práticos
- [ ] Anotar dificuldades comuns
- [ ] Preparar feedback
- [ ] Ajustar próxima aula

---

## 📝 Gabarito - Exercício para Casa

### Parte 1: Expressões Lógicas

1. `V E F OU V` = `(V E F) OU V` = `F OU V` = **V**
2. `(V E F) OU V` = `F OU V` = **V**
3. `V E (F OU V)` = `V E V` = **V**
4. `NÃO (V E F)` = `NÃO F` = **V**
5. `NÃO V OU NÃO F` = `F OU V` = **V**

### Parte 2: Validações

**1. Validar Login:**
```
login_valido ← (email <> "") E CONTEM(email, "@") E 
               (senha <> "") E (TAMANHO(senha) >= 6)
```

**2. Pode enviar mensagem:**
```
pode_enviar ← autenticado E em_sala E sala_ativa E (NÃO bloqueado)
```

**3. Validar entrada na fila:**
```
pode_entrar ← autenticado E (NÃO em_sala) E 
              (categoria = "Filmes" OU categoria = "Jogos" OU categoria = "Séries")
```

### Parte 3: Algoritmo Completo

```
ALGORITMO Validar_Senha_Forte
INÍCIO
  DECLARAR senha: TEXT
  DECLARAR tamanho_ok, tem_letra, tem_numero, tem_especial: BOOLEAN
  DECLARAR senha_forte: BOOLEAN
  
  CONSTANTE MIN_TAMANHO: INTEGER = 8
  
  LER senha
  
  tamanho_ok ← TAMANHO(senha) >= MIN_TAMANHO
  tem_letra ← CONTEM_LETRA(senha)
  tem_numero ← CONTEM_NUMERO(senha)
  tem_especial ← CONTEM_ESPECIAL(senha)
  
  senha_forte ← tamanho_ok E tem_letra E tem_numero E tem_especial
  
  SE senha_forte ENTÃO
    ESCREVER "Senha forte!"
  SENÃO
    ESCREVER "Senha fraca. Requisitos:"
    SE NÃO tamanho_ok ENTÃO
      ESCREVER "- Mínimo 8 caracteres"
    FIM_SE
    SE NÃO tem_letra ENTÃO
      ESCREVER "- Pelo menos uma letra"
    FIM_SE
    SE NÃO tem_numero ENTÃO
      ESCREVER "- Pelo menos um número"
    FIM_SE
    SE NÃO tem_especial ENTÃO
      ESCREVER "- Pelo menos um caractere especial"
    FIM_SE
  FIM_SE
FIM
```

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Compreensão por tipo de operador:
- Aritméticos: ___/10
- Relacionais: ___/10
- Lógicos: ___/10

Dificuldades principais:
- 

Exercícios que funcionaram bem:
- 

Ajustes necessários:
- 

Tempo real:
1. _____ min
2. _____ min
3. _____ min
4. _____ min
5. _____ min
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
