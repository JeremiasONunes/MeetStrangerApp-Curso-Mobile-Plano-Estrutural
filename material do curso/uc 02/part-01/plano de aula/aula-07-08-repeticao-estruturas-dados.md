# Aula 07-08 - Estruturas de Repetição e Introdução às Estruturas de Dados

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 01 - Lógica de Programação  
**Carga Horária:** 8 horas (2 aulas de 4h)  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final destas aulas, o estudante será capaz de:

1. **Repetir** instruções de forma controlada usando loops
2. **Aplicar** ENQUANTO, PARA e REPITA-ATÉ em algoritmos
3. **Compreender** o conceito de estruturas de dados
4. **Manipular** listas, pilhas e filas no contexto do MeetStranger

---

## 📚 Conteúdos Programáticos

### AULA 07 (4 horas)

#### 1. Estrutura ENQUANTO (WHILE) - 60 min
- Conceito de repetição
- Sintaxe e funcionamento
- Condição de parada
- Loops infinitos e como evitar

#### 2. Estrutura PARA (FOR) - 60 min
- Repetição com contador
- Sintaxe e aplicações
- Percorrer sequências

#### 3. Estrutura REPITA-ATÉ (DO-WHILE) - 45 min
- Diferença para ENQUANTO
- Execução garantida
- Casos de uso

#### 4. Prática com Loops - 75 min
- Exercícios progressivos
- Validações com repetição
- Aplicações no MeetStranger

### AULA 08 (4 horas)

#### 1. Conceito de Estruturas de Dados - 45 min
- O que são estruturas de dados
- Por que organizar dados
- Tipos básicos

#### 2. Listas (Arrays) - 90 min
- Conceito e sintaxe
- Adicionar, remover, buscar
- Percorrer com loops
- Aplicações práticas

#### 3. Pilhas e Filas - 60 min
- Conceito de LIFO (pilha)
- Conceito de FIFO (fila)
- Aplicações no MeetStranger

#### 4. Projeto Prático - 75 min
- Sistema de gerenciamento de usuários
- Fila de matching
- Trabalho em grupos

---

## 🎓 AULA 07 - Estratégias de Ensino

### Momento 1: Retomada e Motivação (30 min)

**Problema Motivador:**
```
Situação: Validar login com até 3 tentativas

Sem repetição (ruim):
- Tentar 1ª vez
- SE falhou, tentar 2ª vez
- SE falhou, tentar 3ª vez
- SE falhou, bloquear

Com repetição (melhor):
- ENQUANTO tentativas < 3 E não logou
  - Tentar login
  - Incrementar tentativas
```

### Momento 2: Estrutura ENQUANTO (60 min)

**Atividade 1:** Conceito e Sintaxe (20 min)
```
ENQUANTO condição FAÇA
  // comandos repetidos
FIM_ENQUANTO

Exemplo:
contador ← 1
ENQUANTO contador <= 5 FAÇA
  ESCREVER contador
  contador ← contador + 1
FIM_ENQUANTO
// Saída: 1 2 3 4 5
```

**Atividade 2:** Fluxograma (15 min)
```
     ┌─────────┐
     │ Início  │
     └────┬────┘
          │
     ┌────▼────┐
  ┌─►│Condição?│
  │  └─┬────┬──┘
  │    │Sim │Não
  │  ┌─▼──┐ │
  │  │Ação│ │
  │  └─┬──┘ │
  └────┘    │
            │
       ┌────▼────┐
       │   Fim   │
       └─────────┘
```

**Atividade 3:** Exercícios (25 min)
```
1. Contar de 1 a 10
2. Somar números de 1 a 100
3. Validar entrada até ser válida
4. Login com tentativas limitadas
```

### Momento 3: Estrutura PARA (60 min)

**Atividade 1:** Apresentação (20 min)
```
PARA variavel DE inicio ATÉ fim FAÇA
  // comandos
FIM_PARA

Exemplo:
PARA i DE 1 ATÉ 5 FAÇA
  ESCREVER i
FIM_PARA
// Saída: 1 2 3 4 5
```

**Atividade 2:** ENQUANTO vs PARA (15 min)
```
// ENQUANTO - quando não sabe quantas vezes
ENQUANTO usuario_nao_logado FAÇA
  TENTAR_LOGIN()
FIM_ENQUANTO

// PARA - quando sabe quantas vezes
PARA i DE 1 ATÉ 10 FAÇA
  PROCESSAR_USUARIO(i)
FIM_PARA
```

**Atividade 3:** Exercícios em Duplas (25 min)
```
1. Listar números de 1 a 20
2. Tabuada do 5
3. Percorrer lista de categorias
4. Processar 10 mensagens
```

### Momento 4: Estrutura REPITA-ATÉ (45 min + 10 min intervalo)

**Atividade 1:** Conceito (15 min)
```
REPITA
  // comandos (executam pelo menos 1 vez)
ATÉ condição

Exemplo:
REPITA
  LER opcao
  PROCESSAR(opcao)
ATÉ opcao = "sair"
```

**Atividade 2:** Diferenças (15 min)
```
ENQUANTO: testa antes, pode não executar
REPITA: testa depois, executa pelo menos 1 vez

Uso: menus, validações que precisam tentar
```

**Atividade 3:** Exercício Guiado (15 min)
```
Menu do MeetStranger:
REPITA
  ESCREVER "1-Login 2-Cadastro 3-Sair"
  LER opcao
  PROCESSAR_OPCAO(opcao)
ATÉ opcao = 3
```

### Momento 5: Prática Intensiva (75 min)

**Atividade 1:** Exercícios Progressivos (30 min)
- Nível 1: Loops simples
- Nível 2: Loops com condições
- Nível 3: Loops aninhados

**Atividade 2:** Aplicações MeetStranger (30 min)
```
1. Processar fila de matching
2. Validar múltiplos campos
3. Listar mensagens do chat
4. Buscar usuário por username
```

**Atividade 3:** Síntese (15 min)
- Quando usar cada estrutura
- Exercício para próxima aula

---

## 🎓 AULA 08 - Estratégias de Ensino

### Momento 1: Retomada e Introdução (30 min)

**Atividade:** Problema Motivador
```
Como armazenar múltiplos usuários?

Ruim:
usuario1 ← "João"
usuario2 ← "Maria"
usuario3 ← "Pedro"
...

Melhor:
usuarios ← ["João", "Maria", "Pedro", ...]
```

### Momento 2: Conceito de Estruturas de Dados (45 min)

**Atividade 1:** O que são? (15 min)
- Formas de organizar dados
- Coleções de valores
- Operações básicas

**Atividade 2:** Tipos Básicos (15 min)
```
LISTA: sequência ordenada [1, 2, 3]
PILHA: último a entrar, primeiro a sair
FILA: primeiro a entrar, primeiro a sair
```

**Atividade 3:** Por que usar? (15 min)
- Gerenciar múltiplos dados
- Facilitar operações
- Organização lógica

### Momento 3: Listas (Arrays) (90 min + 10 min intervalo)

**Atividade 1:** Conceito e Sintaxe (25 min)
```
// Declaração
DECLARAR usuarios: LISTA DE TEXT
DECLARAR idades: LISTA DE INTEGER

// Inicialização
usuarios ← ["João", "Maria", "Pedro"]
idades ← [25, 30, 22]

// Acesso por índice (começa em 0)
usuarios[0] = "João"
usuarios[1] = "Maria"
usuarios[2] = "Pedro"
```

**Atividade 2:** Operações Básicas (30 min)
```
// Adicionar
ADICIONAR(usuarios, "Ana")

// Remover
REMOVER(usuarios, 1)  // remove "Maria"

// Buscar
posicao ← BUSCAR(usuarios, "Pedro")

// Tamanho
total ← TAMANHO(usuarios)

// Verificar existência
existe ← CONTEM(usuarios, "João")
```

**Atividade 3:** Percorrer Listas (25 min)
```
// Com PARA
PARA i DE 0 ATÉ TAMANHO(usuarios)-1 FAÇA
  ESCREVER usuarios[i]
FIM_PARA

// Com PARA CADA
PARA CADA usuario EM usuarios FAÇA
  ESCREVER usuario
FIM_PARA
```

**Atividade 4:** Exercícios Práticos (10 min)
```
1. Criar lista de categorias
2. Adicionar nova categoria
3. Listar todas
4. Buscar categoria específica
```

### Momento 4: Pilhas e Filas (60 min)

**Atividade 1:** Pilhas - LIFO (25 min)
```
Conceito: Last In, First Out
Como uma pilha de pratos

Operações:
EMPILHAR(item)  // push
DESEMPILHAR()   // pop
TOPO()          // peek

Exemplo:
pilha ← []
EMPILHAR(pilha, "A")  // [A]
EMPILHAR(pilha, "B")  // [A, B]
EMPILHAR(pilha, "C")  // [A, B, C]
DESEMPILHAR(pilha)    // [A, B] (remove C)

Aplicação: histórico de navegação
```

**Atividade 2:** Filas - FIFO (25 min)
```
Conceito: First In, First Out
Como fila de banco

Operações:
ENFILEIRAR(item)  // enqueue
DESENFILEIRAR()   // dequeue
PRIMEIRO()        // front

Exemplo:
fila ← []
ENFILEIRAR(fila, "João")   // [João]
ENFILEIRAR(fila, "Maria")  // [João, Maria]
ENFILEIRAR(fila, "Pedro")  // [João, Maria, Pedro]
DESENFILEIRAR(fila)        // [Maria, Pedro] (remove João)

Aplicação: fila de matching do MeetStranger
```

**Atividade 3:** Comparação (10 min)
```
LISTA: acesso aleatório, qualquer posição
PILHA: acesso apenas no topo
FILA: acesso apenas no início e fim
```

### Momento 5: Projeto Prático (75 min)

**Atividade:** Sistema de Gerenciamento
- Dividir turma em 4 grupos
- Cada grupo implementa um módulo

**Grupo 1: Lista de Usuários**
```
- Adicionar usuário
- Remover usuário
- Listar todos
- Buscar por username
```

**Grupo 2: Fila de Matching (Filmes)**
```
- Adicionar usuário à fila
- Remover da fila (match encontrado)
- Mostrar posição na fila
- Listar todos na fila
```

**Grupo 3: Fila de Matching (Jogos)**
```
- Mesmas operações do Grupo 2
- Para categoria Jogos
```

**Grupo 4: Histórico de Salas (Pilha)**
```
- Adicionar sala ao histórico
- Remover última sala
- Mostrar sala atual
- Listar histórico
```

**Estrutura:**
- Planejamento: 15 min
- Implementação: 40 min
- Apresentação: 20 min (5 min cada)

---

## 📝 Atividades Práticas

### AULA 07 - Atividade 1: Login com Tentativas

```
ALGORITMO Login_Com_Tentativas
INÍCIO
  DECLARAR email, senha: TEXT
  DECLARAR tentativas, max_tentativas: INTEGER
  DECLARAR logado: BOOLEAN
  
  max_tentativas ← 3
  tentativas ← 0
  logado ← FALSO
  
  ENQUANTO tentativas < max_tentativas E NÃO logado FAÇA
    ESCREVER "Tentativa " + (tentativas + 1) + " de " + max_tentativas
    LER email, senha
    
    SE VERIFICAR_CREDENCIAIS(email, senha) ENTÃO
      ESCREVER "Login realizado!"
      logado ← VERDADEIRO
    SENÃO
      tentativas ← tentativas + 1
      SE tentativas < max_tentativas ENTÃO
        ESCREVER "Credenciais incorretas. Tente novamente."
      FIM_SE
    FIM_SE
  FIM_ENQUANTO
  
  SE NÃO logado ENTÃO
    ESCREVER "Máximo de tentativas atingido. Conta bloqueada."
    BLOQUEAR_CONTA(email)
  FIM_SE
FIM
```

### AULA 07 - Atividade 2: Processar Fila

```
ALGORITMO Processar_Fila_Matching
INÍCIO
  DECLARAR fila_tamanho, i: INTEGER
  DECLARAR categoria: TEXT
  
  categoria ← "Filmes"
  fila_tamanho ← OBTER_TAMANHO_FILA(categoria)
  
  ESCREVER "Processando fila de " + categoria
  ESCREVER "Total de usuários: " + fila_tamanho
  
  PARA i DE 1 ATÉ fila_tamanho FAÇA
    ESCREVER "Posição " + i + ": " + OBTER_USUARIO_FILA(categoria, i)
  FIM_PARA
  
  // Tentar fazer matches
  ENQUANTO fila_tamanho >= 2 FAÇA
    usuario1 ← DESENFILEIRAR(categoria)
    usuario2 ← DESENFILEIRAR(categoria)
    CRIAR_SALA(usuario1, usuario2, categoria)
    ESCREVER "Match criado: " + usuario1 + " <-> " + usuario2
    fila_tamanho ← fila_tamanho - 2
  FIM_ENQUANTO
  
  SE fila_tamanho = 1 ENTÃO
    ESCREVER "1 usuário aguardando na fila"
  FIM_SE
FIM
```

### AULA 07 - Atividade 3: Menu Interativo

```
ALGORITMO Menu_Principal
INÍCIO
  DECLARAR opcao: INTEGER
  
  REPITA
    ESCREVER "=== MEETSTRANGER ==="
    ESCREVER "1 - Login"
    ESCREVER "2 - Cadastro"
    ESCREVER "3 - Sobre"
    ESCREVER "4 - Sair"
    ESCREVER "Escolha uma opção:"
    LER opcao
    
    SE opcao = 1 ENTÃO
      EXECUTAR_LOGIN()
    SENÃO SE opcao = 2 ENTÃO
      EXECUTAR_CADASTRO()
    SENÃO SE opcao = 3 ENTÃO
      MOSTRAR_SOBRE()
    SENÃO SE opcao = 4 ENTÃO
      ESCREVER "Até logo!"
    SENÃO
      ESCREVER "Opção inválida!"
    FIM_SE
  ATÉ opcao = 4
FIM
```

### AULA 08 - Atividade 1: Gerenciar Lista de Usuários

```
ALGORITMO Gerenciar_Usuarios
INÍCIO
  DECLARAR usuarios: LISTA DE TEXT
  DECLARAR opcao: INTEGER
  DECLARAR username: TEXT
  DECLARAR posicao, i: INTEGER
  
  usuarios ← []
  
  REPITA
    ESCREVER "=== GERENCIAR USUÁRIOS ==="
    ESCREVER "1 - Adicionar"
    ESCREVER "2 - Remover"
    ESCREVER "3 - Listar"
    ESCREVER "4 - Buscar"
    ESCREVER "5 - Voltar"
    LER opcao
    
    SE opcao = 1 ENTÃO
      ESCREVER "Username:"
      LER username
      ADICIONAR(usuarios, username)
      ESCREVER "Usuário adicionado!"
      
    SENÃO SE opcao = 2 ENTÃO
      ESCREVER "Username a remover:"
      LER username
      posicao ← BUSCAR(usuarios, username)
      SE posicao >= 0 ENTÃO
        REMOVER(usuarios, posicao)
        ESCREVER "Usuário removido!"
      SENÃO
        ESCREVER "Usuário não encontrado"
      FIM_SE
      
    SENÃO SE opcao = 3 ENTÃO
      ESCREVER "Total: " + TAMANHO(usuarios)
      PARA i DE 0 ATÉ TAMANHO(usuarios)-1 FAÇA
        ESCREVER (i+1) + ". " + usuarios[i]
      FIM_PARA
      
    SENÃO SE opcao = 4 ENTÃO
      ESCREVER "Username a buscar:"
      LER username
      posicao ← BUSCAR(usuarios, username)
      SE posicao >= 0 ENTÃO
        ESCREVER "Encontrado na posição " + (posicao+1)
      SENÃO
        ESCREVER "Não encontrado"
      FIM_SE
    FIM_SE
  ATÉ opcao = 5
FIM
```

### AULA 08 - Atividade 2: Fila de Matching

```
ALGORITMO Fila_Matching
INÍCIO
  DECLARAR fila_filmes: LISTA DE TEXT
  DECLARAR usuario: TEXT
  DECLARAR opcao, posicao: INTEGER
  
  fila_filmes ← []
  
  REPITA
    ESCREVER "=== FILA DE MATCHING - FILMES ==="
    ESCREVER "1 - Entrar na fila"
    ESCREVER "2 - Sair da fila"
    ESCREVER "3 - Ver posição"
    ESCREVER "4 - Listar fila"
    ESCREVER "5 - Processar matches"
    ESCREVER "6 - Voltar"
    LER opcao
    
    SE opcao = 1 ENTÃO
      ESCREVER "Seu username:"
      LER usuario
      ENFILEIRAR(fila_filmes, usuario)
      posicao ← TAMANHO(fila_filmes)
      ESCREVER "Você está na posição " + posicao
      
    SENÃO SE opcao = 2 ENTÃO
      ESCREVER "Seu username:"
      LER usuario
      posicao ← BUSCAR(fila_filmes, usuario)
      SE posicao >= 0 ENTÃO
        REMOVER(fila_filmes, posicao)
        ESCREVER "Você saiu da fila"
      SENÃO
        ESCREVER "Você não está na fila"
      FIM_SE
      
    SENÃO SE opcao = 3 ENTÃO
      ESCREVER "Seu username:"
      LER usuario
      posicao ← BUSCAR(fila_filmes, usuario)
      SE posicao >= 0 ENTÃO
        ESCREVER "Sua posição: " + (posicao+1)
      SENÃO
        ESCREVER "Você não está na fila"
      FIM_SE
      
    SENÃO SE opcao = 4 ENTÃO
      ESCREVER "Total na fila: " + TAMANHO(fila_filmes)
      PARA i DE 0 ATÉ TAMANHO(fila_filmes)-1 FAÇA
        ESCREVER (i+1) + ". " + fila_filmes[i]
      FIM_PARA
      
    SENÃO SE opcao = 5 ENTÃO
      ENQUANTO TAMANHO(fila_filmes) >= 2 FAÇA
        usuario1 ← DESENFILEIRAR(fila_filmes)
        usuario2 ← DESENFILEIRAR(fila_filmes)
        ESCREVER "Match: " + usuario1 + " <-> " + usuario2
      FIM_ENQUANTO
      SE TAMANHO(fila_filmes) = 1 ENTÃO
        ESCREVER "1 usuário aguardando"
      SENÃO
        ESCREVER "Fila vazia"
      FIM_SE
    FIM_SE
  ATÉ opcao = 6
FIM
```

### Exercício para Casa (Aula 07)

**Criar algoritmo: Validar Múltiplos Campos**

Usar ENQUANTO para validar até entrada ser válida:
- Username (3-20 caracteres)
- Email (formato válido)
- Senha (6+ caracteres)
- Idade (13+ anos)

Não permitir prosseguir até todos estarem corretos.

### Exercício para Casa (Aula 08)

**Criar sistema: Gerenciar Categorias**

Usar lista para armazenar categorias do MeetStranger:
- Adicionar categoria
- Remover categoria
- Listar todas
- Buscar categoria
- Contar usuários por categoria (usar outra lista)

---

## 📊 Avaliação

### Avaliação Diagnóstica (Aula 07)
- Compreensão de condições
- Capacidade de identificar repetições

### Avaliação Formativa

**Critérios:**
- ✅ Usa ENQUANTO corretamente
- ✅ Aplica PARA adequadamente
- ✅ Implementa REPITA-ATÉ quando apropriado
- ✅ Cria e manipula listas
- ✅ Compreende pilhas e filas
- ✅ Combina loops com estruturas de dados

**Instrumentos:**
- Exercícios práticos
- Projeto em grupo
- Participação
- Exercícios para casa

### Avaliação Somativa

**Aula 07:**
- Exercícios em aula: 40%
- Exercício para casa: 60%

**Aula 08:**
- Projeto em grupo: 50%
- Exercício para casa: 50%

**Peso das Aulas:** 25% da nota da Parte 1

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Identifica quando usar loops  
✅ Implementa ENQUANTO, PARA e REPITA corretamente  
✅ Evita loops infinitos  
✅ Cria e manipula listas  
✅ Compreende diferença entre pilha e fila  
✅ Combina loops com estruturas de dados  
✅ Aplica conceitos no MeetStranger  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Projetor/TV
- [ ] Slides com fluxogramas
- [ ] Quadro branco
- [ ] Cartões para simular pilha/fila
- [ ] Folhas de exercício
- [ ] Documentação do MeetStranger

### Analogias Visuais

**Pilha (LIFO):**
```
Pilha de pratos:
┌─────┐
│  C  │ ← Topo (último a entrar, primeiro a sair)
├─────┤
│  B  │
├─────┤
│  A  │ ← Base
└─────┘
```

**Fila (FIFO):**
```
Fila de banco:
Entrada → [João] [Maria] [Pedro] → Saída
          ↑                        ↑
       Último                  Primeiro
```

### Referências
- FORBELLONE, A. L. V. **Lógica de Programação**. Cap. 6-7.
- MANZANO, J. A. N. G. **Algoritmos**. Cap. 5-6.

---

## 🔄 Conexão com Outras Aulas

### Revisão das Aulas 01-06
- Algoritmos e pseudocódigo
- Variáveis e operadores
- Estruturas condicionais

### Preparação para Aula 09
- Integração de todos os conceitos
- Projeto final da Parte 1
- Avaliação somativa

---

## 💡 Dicas para o Docente

### Gestão do Tempo

**Aula 07:**
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 60 min
- ⏰ Momento 4: 55 min (com intervalo)
- ⏰ Momento 5: 75 min

**Aula 08:**
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 45 min
- ⏰ Momento 3: 100 min (com intervalo)
- ⏰ Momento 4: 60 min
- ⏰ Momento 5: 75 min

### Pontos de Atenção
1. **Loops Infinitos**: Sempre verificar condição de parada
2. **Índices**: Listas começam em 0
3. **ENQUANTO vs REPITA**: Diferença crucial
4. **Pilha vs Fila**: Use analogias físicas
5. **Performance**: Loops aninhados podem ser lentos

### Estratégias
- Use objetos físicos (cartas, blocos)
- Simule execução passo a passo
- Desenhe estruturas no quadro
- Peça estudantes para "serem" a estrutura
- Mostre código real em JavaScript

### Adaptações
- **Turma iniciante**: Foque em PARA e listas
- **Turma avançada**: Introduza recursão
- **EAD**: Use animações online

---

## 📋 Checklist do Docente

### Antes das Aulas
- [ ] Preparar slides com animações
- [ ] Criar exercícios progressivos
- [ ] Preparar materiais físicos (cartões)
- [ ] Revisar conceitos de estruturas
- [ ] Organizar grupos

### Durante Aula 07
- [ ] Ensinar ENQUANTO
- [ ] Apresentar PARA
- [ ] Explicar REPITA-ATÉ
- [ ] Conduzir práticas
- [ ] Entregar exercício

### Durante Aula 08
- [ ] Revisar exercício
- [ ] Ensinar listas
- [ ] Apresentar pilhas e filas
- [ ] Conduzir projeto
- [ ] Avaliar aprendizado

### Após as Aulas
- [ ] Registrar frequência
- [ ] Avaliar projetos
- [ ] Dar feedback
- [ ] Preparar aula final

---

## 📝 Observações e Ajustes

```
AULA 07
Data: ___/___/______

Compreensão:
- ENQUANTO: ___/10
- PARA: ___/10
- REPITA: ___/10

Dificuldades:
- 

Tempo real: _____ min

---

AULA 08
Data: ___/___/______

Compreensão:
- Listas: ___/10
- Pilhas: ___/10
- Filas: ___/10

Projeto:
- Qualidade: ___/10

Ajustes:
- 
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
