# Aula 03 - Tipos de Dados, Variáveis e Constantes

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 01 - Lógica de Programação  
**Carga Horária:** 4 horas  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Compreender** como os dados são representados e armazenados em algoritmos
2. **Diferenciar** tipos de dados primitivos e suas aplicações
3. **Utilizar** variáveis e constantes corretamente em algoritmos
4. **Aplicar** boas práticas na manipulação e nomenclatura de dados

---

## 📚 Conteúdos Programáticos

### 1. Tipos de Dados Primitivos (60 min)
- Conceito de tipo de dado
- Inteiro (INTEGER)
- Real/Decimal (REAL)
- Texto/String (TEXT)
- Lógico/Booleano (BOOLEAN)
- Escolha do tipo adequado

### 2. Variáveis (60 min)
- Conceito e função das variáveis
- Declaração de variáveis
- Atribuição de valores
- Nomenclatura e boas práticas
- Escopo de variáveis

### 3. Constantes (30 min)
- Diferença entre variável e constante
- Quando usar constantes
- Declaração e uso
- Exemplos práticos

### 4. Manipulação de Dados (60 min)
- Operações com diferentes tipos
- Conversão entre tipos
- Validação de dados
- Aplicação no MeetStranger

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Retomada e Motivação (30 min)

**Atividade:** Revisão Rápida + Problema Motivador
- Correção breve dos exercícios
- Apresentar problema: "Como o computador sabe que '25' é diferente de 25?"
- Discussão sobre necessidade de tipos de dados

**Problema Motivador:**
```
email = "usuario@email.com"
idade = 25
ativo = verdadeiro

Por que precisamos diferenciar esses dados?
```

### Momento 2: Tipos de Dados Primitivos (60 min)

**Atividade 1:** Classificação de Dados (15 min)
- Apresentar lista de dados do MeetStranger
- Turma classifica cada um:
  - username → ?
  - idade → ?
  - email → ?
  - senha → ?
  - online → ?
  - mensagem → ?

**Atividade 2:** Exposição Dialogada (25 min)
- Apresentar cada tipo primitivo
- Características e limitações
- Exemplos práticos

**Tipos de Dados:**
```
INTEGER (Inteiro)
- Números sem casas decimais
- Exemplos: idade, quantidade_mensagens, posicao_fila
- Faixa: -2147483648 a 2147483647

REAL (Decimal)
- Números com casas decimais
- Exemplos: avaliacao (4.5), tempo_resposta (1.25)
- Precisão limitada

TEXT (Texto/String)
- Sequência de caracteres
- Exemplos: username, email, mensagem
- Entre aspas: "texto"

BOOLEAN (Lógico)
- Apenas dois valores: VERDADEIRO ou FALSO
- Exemplos: online, autenticado, senha_forte
- Usado em condições
```

**Atividade 3:** Exercício Prático (20 min)
- Identificar tipo adequado para 10 dados do sistema
- Justificar escolhas
- Discussão coletiva

### Momento 3: Variáveis (60 min + 10 min intervalo)

**Atividade 1:** Conceito de Variável (15 min)
- Analogia: variável como "caixa com etiqueta"
- Demonstração visual no quadro
- Declaração vs. Atribuição

**Atividade 2:** Sintaxe e Declaração (20 min)
```
DECLARAR nome_variavel: TIPO

Exemplos:
DECLARAR username: TEXT
DECLARAR idade: INTEGER
DECLARAR online: BOOLEAN
DECLARAR avaliacao: REAL

Atribuição:
username ← "joao123"
idade ← 25
online ← VERDADEIRO
avaliacao ← 4.5
```

**Atividade 3:** Boas Práticas de Nomenclatura (15 min)
- Regras de nomenclatura
- Padrões: camelCase, snake_case
- Nomes descritivos vs. abreviações

**Boas Práticas:**
```
✅ BOM:
- username
- email_usuario
- senha_forte
- esta_online

❌ RUIM:
- x
- var1
- a
- dados
```

**Atividade 4:** Exercício em Duplas (10 min)
- Declarar variáveis para cadastro de usuário
- Atribuir valores de exemplo
- Apresentar soluções

### Momento 4: Constantes (30 min)

**Atividade 1:** Diferença Variável vs. Constante (10 min)
- Conceito de valor imutável
- Quando usar constantes
- Vantagens

**Atividade 2:** Exemplos do MeetStranger (10 min)
```
CONSTANTE CATEGORIAS: TEXT[] = ["Filmes", "Jogos", "Séries"]
CONSTANTE TAMANHO_MIN_SENHA: INTEGER = 6
CONSTANTE TAMANHO_MIN_USERNAME: INTEGER = 3
CONSTANTE TEMPO_TIMEOUT: INTEGER = 300
CONSTANTE VERSAO_APP: TEXT = "1.0.0"
```

**Atividade 3:** Identificar Constantes (10 min)
- Lista de dados do sistema
- Identificar quais devem ser constantes
- Justificar

### Momento 5: Manipulação e Prática (60 min)

**Atividade 1:** Algoritmo Completo com Variáveis (20 min)
- Criar algoritmo de cadastro usando variáveis
- Incluir declarações e atribuições
- Trabalho individual

**Atividade 2:** Simulação de Dados de Usuário (30 min)
- Dividir turma em grupos
- Cada grupo cria estrutura de dados para:
  - Grupo 1: Perfil de usuário
  - Grupo 2: Mensagem de chat
  - Grupo 3: Sala de conversa
  - Grupo 4: Fila de matching
- Apresentação rápida

**Atividade 3:** Síntese e Fechamento (10 min)
- Recapitulação dos conceitos
- Conexão com próxima aula
- Exercício para casa

---

## 📝 Atividades Práticas

### Atividade 1: Classificação de Dados

**Classifique cada dado com o tipo adequado:**

| Dado | Tipo | Justificativa |
|------|------|---------------|
| username | TEXT | Sequência de caracteres |
| idade | INTEGER | Número inteiro |
| email | TEXT | Sequência de caracteres |
| senha | TEXT | Sequência de caracteres |
| online | BOOLEAN | Verdadeiro ou Falso |
| quantidade_mensagens | INTEGER | Número inteiro |
| tempo_conexao | REAL | Pode ter decimais (minutos) |
| categoria_escolhida | TEXT | Nome da categoria |
| posicao_fila | INTEGER | Número inteiro |
| autenticado | BOOLEAN | Verdadeiro ou Falso |

### Atividade 2: Algoritmo de Cadastro com Variáveis

```
ALGORITMO Cadastrar_Usuario_Com_Variaveis

INÍCIO
  // DECLARAÇÃO DE VARIÁVEIS
  DECLARAR username: TEXT
  DECLARAR email: TEXT
  DECLARAR senha: TEXT
  DECLARAR idade: INTEGER
  DECLARAR email_valido: BOOLEAN
  DECLARAR senha_forte: BOOLEAN
  DECLARAR usuario_existe: BOOLEAN
  
  // DECLARAÇÃO DE CONSTANTES
  CONSTANTE TAMANHO_MIN_SENHA: INTEGER = 6
  CONSTANTE TAMANHO_MIN_USERNAME: INTEGER = 3
  
  // ENTRADA
  ESCREVER "Digite seu username:"
  LER username
  
  ESCREVER "Digite seu email:"
  LER email
  
  ESCREVER "Digite sua senha:"
  LER senha
  
  ESCREVER "Digite sua idade:"
  LER idade
  
  // PROCESSAMENTO - Validações
  SE TAMANHO(username) < TAMANHO_MIN_USERNAME ENTÃO
    ESCREVER "Erro: Username deve ter no mínimo 3 caracteres"
    FIM
  FIM_SE
  
  email_valido ← CONTEM(email, "@") E CONTEM(email, ".")
  SE NÃO email_valido ENTÃO
    ESCREVER "Erro: Email inválido"
    FIM
  FIM_SE
  
  senha_forte ← TAMANHO(senha) >= TAMANHO_MIN_SENHA
  SE NÃO senha_forte ENTÃO
    ESCREVER "Erro: Senha deve ter no mínimo 6 caracteres"
    FIM
  FIM_SE
  
  SE idade < 13 ENTÃO
    ESCREVER "Erro: Idade mínima é 13 anos"
    FIM
  FIM_SE
  
  usuario_existe ← BUSCAR_NO_BANCO("users", "email", email)
  SE usuario_existe ENTÃO
    ESCREVER "Erro: Email já cadastrado"
    FIM
  FIM_SE
  
  // PROCESSAMENTO - Cadastro
  SALVAR_NO_BANCO(username, email, senha, idade)
  
  // SAÍDA
  ESCREVER "Cadastro realizado com sucesso!"
  ESCREVER "Bem-vindo, " + username + "!"
FIM
```

### Atividade 3: Estrutura de Dados - Perfil de Usuário

```
ESTRUTURA Perfil_Usuario
  // Dados básicos
  DECLARAR id: INTEGER
  DECLARAR username: TEXT
  DECLARAR email: TEXT
  DECLARAR senha_hash: TEXT
  DECLARAR idade: INTEGER
  
  // Status
  DECLARAR online: BOOLEAN
  DECLARAR autenticado: BOOLEAN
  DECLARAR em_chat: BOOLEAN
  
  // Estatísticas
  DECLARAR total_conversas: INTEGER
  DECLARAR tempo_total_online: REAL
  DECLARAR categoria_favorita: TEXT
  
  // Datas
  DECLARAR data_cadastro: TEXT
  DECLARAR ultimo_login: TEXT
  
  // Constantes do sistema
  CONSTANTE VERSAO_PERFIL: TEXT = "1.0"
  CONSTANTE TIPO_CONTA: TEXT = "FREE"
FIM_ESTRUTURA
```

### Exercício para Casa

**Parte 1: Declaração de Variáveis**

Para cada funcionalidade, declare todas as variáveis necessárias com tipos adequados:

1. **Login de Usuário**
   - Quais dados são necessários?
   - Quais variáveis auxiliares?
   - Quais constantes?

2. **Enviar Mensagem**
   - Dados da mensagem
   - Validações necessárias
   - Constantes do sistema

3. **Entrar na Fila de Matching**
   - Dados do usuário
   - Categoria escolhida
   - Informações da fila

**Parte 2: Algoritmo Completo**

Escolha UMA funcionalidade e crie algoritmo completo incluindo:
- Declaração de todas as variáveis
- Declaração de constantes
- Atribuições
- Processamento
- Uso correto dos tipos

**Formato:**
```
ALGORITMO Nome_Funcionalidade
INÍCIO
  // VARIÁVEIS
  DECLARAR ...
  
  // CONSTANTES
  CONSTANTE ...
  
  // LÓGICA
  ...
FIM
```

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Conhecimento prévio sobre tipos de dados
- Experiência com variáveis

### Avaliação Formativa

**Critérios:**
- ✅ Identifica tipos de dados corretamente
- ✅ Declara variáveis com sintaxe adequada
- ✅ Usa nomenclatura descritiva
- ✅ Diferencia variável de constante
- ✅ Aplica boas práticas

**Instrumentos:**
- Observação durante atividades
- Exercícios práticos
- Participação nas discussões

### Avaliação Somativa
- Atividades em aula: 40%
- Exercício para casa: 60%

**Peso da Aula:** 15% da nota da Parte 1

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Escolhe o tipo de dado adequado para cada situação  
✅ Declara variáveis com sintaxe correta  
✅ Usa nomes descritivos e significativos  
✅ Diferencia quando usar variável ou constante  
✅ Atribui valores compatíveis com o tipo declarado  
✅ Aplica boas práticas de nomenclatura  
✅ Organiza declarações no início do algoritmo  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Projetor/TV
- [ ] Slides com exemplos
- [ ] Quadro branco
- [ ] Tabela de tipos de dados impressa
- [ ] Exercícios práticos
- [ ] Cartões com dados para classificação

### Materiais de Apoio

**Tabela de Referência Rápida:**
```
┌──────────┬─────────────┬──────────────────┬─────────────────┐
│ Tipo     │ Descrição   │ Exemplos         │ Uso no Sistema  │
├──────────┼─────────────┼──────────────────┼─────────────────┤
│ INTEGER  │ Inteiro     │ 25, -10, 0       │ idade, id       │
│ REAL     │ Decimal     │ 4.5, -2.3, 0.0   │ avaliacao       │
│ TEXT     │ Texto       │ "João", "abc"    │ username, email │
│ BOOLEAN  │ Lógico      │ VERDADEIRO/FALSO │ online, ativo   │
└──────────┴─────────────┴──────────────────┴─────────────────┘
```

### Referências
- FORBELLONE, A. L. V. **Lógica de Programação**. Cap. 3.
- MANZANO, J. A. N. G. **Algoritmos**. Cap. 2-3.

---

## 🔄 Conexão com Outras Aulas

### Revisão das Aulas 01-02
- Algoritmos estruturados
- Pseudocódigo
- Entrada → Processamento → Saída

### Preparação para Aula 04
- Operadores (próximo tema)
- Expressões com variáveis
- Operações entre tipos

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 70 min (com intervalo)
- ⏰ Momento 4: 30 min
- ⏰ Momento 5: 60 min

### Pontos de Atenção
1. **Tipos de Dados**: Relacione sempre com exemplos práticos do MeetStranger
2. **Nomenclatura**: Enfatize importância de nomes descritivos
3. **Constantes**: Deixe claro que são valores que não mudam
4. **Prática**: Foque mais em exercícios que em teoria

### Estratégias
- Use analogias visuais (caixas para variáveis)
- Desenhe no quadro a memória do computador
- Mostre erros comuns e como evitá-los
- Conecte sempre com JavaScript/TypeScript (futuro)

### Adaptações
- **Turma iniciante**: Mais exemplos, menos teoria
- **Turma avançada**: Introduza arrays e objetos brevemente
- **EAD**: Use ferramentas de quadro colaborativo online

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Preparar slides com exemplos
- [ ] Imprimir tabela de tipos de dados
- [ ] Criar cartões para atividade de classificação
- [ ] Revisar exercícios da aula anterior
- [ ] Preparar exemplos do MeetStranger

### Durante a Aula
- [ ] Fazer retomada da aula anterior
- [ ] Apresentar tipos de dados primitivos
- [ ] Ensinar declaração de variáveis
- [ ] Explicar constantes
- [ ] Conduzir atividades práticas
- [ ] Entregar exercício para casa

### Após a Aula
- [ ] Registrar frequência
- [ ] Avaliar exercícios práticos
- [ ] Anotar dificuldades da turma
- [ ] Preparar feedback
- [ ] Ajustar próxima aula

---

## 📝 Gabarito - Exercício para Casa

### Parte 1: Login de Usuário

```
ALGORITMO Login_Usuario
INÍCIO
  // VARIÁVEIS
  DECLARAR email: TEXT
  DECLARAR senha: TEXT
  DECLARAR usuario_encontrado: BOOLEAN
  DECLARAR senha_correta: BOOLEAN
  DECLARAR token: TEXT
  DECLARAR id_usuario: INTEGER
  
  // CONSTANTES
  CONSTANTE TEMPO_EXPIRACAO_TOKEN: INTEGER = 86400
  CONSTANTE MAX_TENTATIVAS: INTEGER = 3
  
  // LÓGICA
  LER email, senha
  
  usuario_encontrado ← BUSCAR_NO_BANCO("users", "email", email)
  
  SE usuario_encontrado ENTÃO
    senha_correta ← VERIFICAR_SENHA(senha)
    SE senha_correta ENTÃO
      token ← GERAR_TOKEN(id_usuario, TEMPO_EXPIRACAO_TOKEN)
      ESCREVER "Login realizado!"
      RETORNAR token
    SENÃO
      ESCREVER "Senha incorreta"
    FIM_SE
  SENÃO
    ESCREVER "Usuário não encontrado"
  FIM_SE
FIM
```

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Compreensão da turma:
- Tipos de dados: ___/10
- Variáveis: ___/10
- Constantes: ___/10

Dificuldades:
- 

Destaques positivos:
- 

Ajustes para próxima turma:
- 

Tempo real por momento:
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
