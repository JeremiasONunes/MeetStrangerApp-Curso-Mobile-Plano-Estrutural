# Aula 02 - Algoritmos e Resolução de Problemas Computacionais

**Curso:** Programador Mobile  
**UC:** 02 - Programação de Dispositivos Móveis  
**Parte:** 01 - Lógica de Programação  
**Carga Horária:** 4 horas  
**Docente:** Jeremias O Nunes

---

## 🎯 Objetivos de Aprendizagem

Ao final desta aula, o estudante será capaz de:

1. **Desenvolver** raciocínio lógico para solução de problemas computacionais
2. **Estruturar** algoritmos completos e bem organizados
3. **Representar** algoritmos em linguagem natural e pseudocódigo
4. **Aplicar** técnicas de resolução de problemas no contexto do MeetStranger

---

## 📚 Conteúdos Programáticos

### 1. Estruturação de Algoritmos (60 min)
- Componentes de um algoritmo bem estruturado
- Padrão: Entrada → Processamento → Saída
- Decomposição de problemas complexos
- Boas práticas na escrita de algoritmos

### 2. Representação em Linguagem Natural (45 min)
- Características da linguagem natural
- Vantagens e limitações
- Técnicas para clareza e precisão
- Exemplos práticos do MeetStranger

### 3. Introdução ao Pseudocódigo (60 min)
- O que é pseudocódigo
- Estrutura básica e sintaxe
- Palavras-chave comuns
- Conversão de linguagem natural para pseudocódigo

### 4. Resolução de Problemas Computacionais (45 min)
- Metodologia de resolução de problemas
- Análise do problema
- Planejamento da solução
- Implementação e validação

---

## 🎓 Estratégias de Ensino-Aprendizagem

### Momento 1: Retomada e Correção (30 min)

**Atividade:** Revisão do Exercício para Casa
- Voluntários apresentam seus algoritmos
- Discussão sobre diferentes abordagens
- Identificação de pontos fortes e melhorias

**Perguntas Norteadoras:**
- Quais validações foram incluídas?
- A sequência está lógica?
- Faltou algum passo importante?

### Momento 2: Estruturação de Algoritmos (60 min)

**Atividade 1:** Análise de Algoritmo Mal Estruturado (20 min)
```
Exemplo propositalmente confuso:
"Pegar email e senha, ver se tá certo, se não tiver @ no email 
dá erro, aí salva no banco, mas antes vê se já tem, 
se tiver dá erro, senão cadastra e pronto"
```
- Identificar problemas
- Discutir importância da estrutura

**Atividade 2:** Componentes Essenciais (20 min)
- Exposição dialogada sobre estrutura
- Modelo padrão de algoritmo
- Importância de cada seção

**Atividade 3:** Reestruturação Coletiva (20 min)
- Reescrever o exemplo de forma estruturada
- Aplicar padrão Entrada → Processamento → Saída
- Comparar versões

### Momento 3: Pseudocódigo (60 min + 10 min intervalo)

**Atividade 1:** Introdução ao Pseudocódigo (20 min)
- Apresentação do conceito
- Palavras-chave básicas: INÍCIO, FIM, SE, SENÃO, ENQUANTO
- Comparação com linguagem natural

**Atividade 2:** Conversão Prática (30 min)
- Converter algoritmo de "Login de Usuário" para pseudocódigo
- Trabalho em duplas
- Apresentação de soluções

**Atividade 3:** Exercício Guiado (10 min)
- Pseudocódigo de "Validar Email"
- Construção coletiva no quadro

### Momento 4: Resolução de Problemas (60 min)

**Atividade 1:** Metodologia de Resolução (15 min)
- Apresentar os 4 passos:
  1. Entender o problema
  2. Planejar a solução
  3. Executar o plano
  4. Revisar e validar

**Atividade 2:** Problema Prático em Grupo (35 min)
- Dividir turma em grupos de 3-4
- Cada grupo resolve um problema diferente:
  - Grupo 1: Validar senha forte
  - Grupo 2: Verificar disponibilidade de username
  - Grupo 3: Entrar na fila de matching
  - Grupo 4: Sair do chat e reconectar
- Criar algoritmo em pseudocódigo

**Atividade 3:** Apresentação e Feedback (10 min)
- Cada grupo apresenta rapidamente
- Turma sugere melhorias

### Momento 5: Análise Coletiva e Fechamento (30 min)

**Atividade:** Refinamento de Soluções
- Escolher 2 algoritmos apresentados
- Análise detalhada em conjunto
- Identificar melhorias possíveis
- Síntese dos aprendizados

---

## 📝 Atividades Práticas

### Atividade em Aula: Algoritmo de Login

**Problema:**
Criar algoritmo completo para login de usuário no MeetStranger.

**Requisitos:**
- Entrada: email e senha
- Validações: campos obrigatórios, formato de email
- Verificação: credenciais no banco de dados
- Saída: token de autenticação ou mensagem de erro

**Solução em Pseudocódigo:**
```
ALGORITMO Login_Usuario

INÍCIO
  // ENTRADA
  DECLARAR email: TEXTO
  DECLARAR senha: TEXTO
  
  ESCREVER "Digite seu email:"
  LER email
  
  ESCREVER "Digite sua senha:"
  LER senha
  
  // PROCESSAMENTO
  SE email VAZIO ENTÃO
    ESCREVER "Erro: Email obrigatório"
    FIM
  FIM_SE
  
  SE senha VAZIO ENTÃO
    ESCREVER "Erro: Senha obrigatória"
    FIM
  FIM_SE
  
  SE NÃO CONTEM(email, "@") OU NÃO CONTEM(email, ".") ENTÃO
    ESCREVER "Erro: Email inválido"
    FIM
  FIM_SE
  
  usuario ← BUSCAR_NO_BANCO(email)
  
  SE usuario NÃO EXISTE ENTÃO
    ESCREVER "Erro: Usuário não encontrado"
    FIM
  FIM_SE
  
  SE NÃO VERIFICAR_SENHA(senha, usuario.senha_hash) ENTÃO
    ESCREVER "Erro: Senha incorreta"
    FIM
  FIM_SE
  
  token ← GERAR_TOKEN(usuario.id)
  ATUALIZAR_STATUS_ONLINE(usuario.id, VERDADEIRO)
  
  // SAÍDA
  ESCREVER "Login realizado com sucesso!"
  RETORNAR token
FIM
```

### Exercício em Grupo: Problemas do MeetStranger

**Grupo 1: Validar Senha Forte**
```
Requisitos:
- Mínimo 6 caracteres
- Pelo menos 1 letra
- Pelo menos 1 número
Criar algoritmo em pseudocódigo
```

**Grupo 2: Verificar Username Disponível**
```
Requisitos:
- Username não pode estar vazio
- Mínimo 3 caracteres
- Verificar se já existe no banco
Criar algoritmo em pseudocódigo
```

**Grupo 3: Entrar na Fila de Matching**
```
Requisitos:
- Usuário deve estar autenticado
- Escolher categoria (Filmes, Jogos, Séries)
- Adicionar à fila da categoria
- Retornar posição na fila
Criar algoritmo em pseudocódigo
```

**Grupo 4: Sair do Chat**
```
Requisitos:
- Verificar se está em uma sala
- Notificar parceiro
- Remover da sala
- Oferecer opção de reconectar
Criar algoritmo em pseudocódigo
```

### Exercício para Casa

**Título:** Algoritmos Completos do MeetStranger

**Parte 1:** Escolha 2 funcionalidades e crie algoritmos em pseudocódigo:
1. Enviar mensagem no chat
2. Trocar de parceiro ("Próximo")
3. Atualizar perfil de usuário
4. Logout do sistema

**Parte 2:** Para cada algoritmo, identifique:
- Entradas necessárias
- Validações obrigatórias
- Processamento principal
- Saídas possíveis (sucesso e erro)

**Formato:**
```
ALGORITMO Nome_Da_Funcionalidade
INÍCIO
  // Seu código aqui
FIM

ANÁLISE:
Entradas: ...
Validações: ...
Processamento: ...
Saídas: ...
```

**Prazo:** Próxima aula

---

## 📊 Avaliação

### Avaliação Diagnóstica
- Correção do exercício da aula anterior
- Identificação de dificuldades comuns

### Avaliação Formativa
**Critérios de Observação:**
- Participação nas atividades em grupo
- Qualidade dos algoritmos criados
- Capacidade de converter linguagem natural para pseudocódigo
- Colaboração e comunicação

**Indicadores:**
- ✅ Estrutura algoritmos corretamente
- ✅ Usa pseudocódigo adequadamente
- ✅ Identifica validações necessárias
- ✅ Trabalha bem em equipe

### Avaliação Somativa
- Exercício em grupo (30% da nota da aula)
- Exercício para casa (70% da nota da aula)

**Peso da Aula:** 15% da nota da Parte 1

---

## 🎯 Indicadores de Desempenho

O estudante demonstra competência quando:

✅ Estrutura algoritmos com início, meio e fim claros  
✅ Converte linguagem natural para pseudocódigo  
✅ Identifica entradas, processamento e saídas  
✅ Inclui validações e tratamento de erros  
✅ Usa palavras-chave do pseudocódigo corretamente  
✅ Resolve problemas de forma lógica e organizada  
✅ Analisa criticamente soluções propostas  

---

## 📚 Recursos Didáticos

### Materiais Necessários
- [ ] Projetor/TV
- [ ] Slides da aula
- [ ] Quadro branco
- [ ] Folhas para exercícios em grupo
- [ ] Exemplos de algoritmos impressos
- [ ] Documentação do MeetStranger

### Materiais de Apoio
- Tabela de palavras-chave do pseudocódigo
- Exemplos de algoritmos bem estruturados
- Checklist de validações comuns
- Guia rápido de pseudocódigo

### Referências
- FORBELLONE, A. L. V. **Lógica de Programação**. Cap. 2-3.
- MANZANO, J. A. N. G. **Algoritmos**. Cap. 1-2.
- Material da aula anterior

---

## 🔄 Conexão com Outras Aulas

### Revisão da Aula 01
- Conceito de algoritmo
- Sequência lógica
- Entrada → Processamento → Saída

### Preparação para Aula 03
- Tipos de dados (próximo tema)
- Variáveis e constantes
- Aplicação em pseudocódigo

---

## 💡 Dicas para o Docente

### Gestão do Tempo
- ⏰ Momento 1: 30 min
- ⏰ Momento 2: 60 min
- ⏰ Momento 3: 70 min (com intervalo)
- ⏰ Momento 4: 60 min
- ⏰ Momento 5: 30 min

### Pontos de Atenção
1. **Pseudocódigo**: Não existe padrão único, deixe claro que é uma ferramenta
2. **Grupos**: Misture níveis de conhecimento
3. **Tempo**: Atividades em grupo podem estender, seja flexível
4. **Exemplos**: Use sempre o MeetStranger para manter contexto

### Adaptações
- **Turma com dificuldade**: Foque mais em linguagem natural, menos em pseudocódigo
- **Turma avançada**: Introduza fluxogramas como representação alternativa
- **EAD**: Use breakout rooms para atividades em grupo

---

## 📋 Checklist do Docente

### Antes da Aula
- [ ] Corrigir exercícios da aula anterior
- [ ] Preparar exemplos de algoritmos
- [ ] Criar folhas de exercício para grupos
- [ ] Testar equipamentos
- [ ] Revisar pseudocódigo

### Durante a Aula
- [ ] Corrigir exercício anterior
- [ ] Apresentar estruturação de algoritmos
- [ ] Ensinar pseudocódigo
- [ ] Conduzir atividades em grupo
- [ ] Fazer análise coletiva
- [ ] Entregar novo exercício

### Após a Aula
- [ ] Registrar frequência
- [ ] Anotar dificuldades observadas
- [ ] Avaliar exercícios em grupo
- [ ] Preparar feedback
- [ ] Ajustar próxima aula se necessário

---

## 📝 Gabarito - Exercícios em Grupo

### Grupo 1: Validar Senha Forte
```
ALGORITMO Validar_Senha_Forte
INÍCIO
  DECLARAR senha: TEXTO
  DECLARAR temLetra, temNumero: LÓGICO
  
  LER senha
  
  SE TAMANHO(senha) < 6 ENTÃO
    RETORNAR FALSO, "Senha deve ter no mínimo 6 caracteres"
  FIM_SE
  
  temLetra ← FALSO
  temNumero ← FALSO
  
  PARA cada caractere EM senha FAÇA
    SE caractere É_LETRA ENTÃO
      temLetra ← VERDADEIRO
    FIM_SE
    SE caractere É_NÚMERO ENTÃO
      temNumero ← VERDADEIRO
    FIM_SE
  FIM_PARA
  
  SE NÃO temLetra ENTÃO
    RETORNAR FALSO, "Senha deve conter pelo menos uma letra"
  FIM_SE
  
  SE NÃO temNumero ENTÃO
    RETORNAR FALSO, "Senha deve conter pelo menos um número"
  FIM_SE
  
  RETORNAR VERDADEIRO, "Senha válida"
FIM
```

### Grupo 2: Verificar Username Disponível
```
ALGORITMO Verificar_Username_Disponivel
INÍCIO
  DECLARAR username: TEXTO
  
  LER username
  
  SE username VAZIO ENTÃO
    RETORNAR FALSO, "Username obrigatório"
  FIM_SE
  
  SE TAMANHO(username) < 3 ENTÃO
    RETORNAR FALSO, "Username deve ter no mínimo 3 caracteres"
  FIM_SE
  
  existe ← BUSCAR_NO_BANCO("users", "username", username)
  
  SE existe ENTÃO
    RETORNAR FALSO, "Username já está em uso"
  FIM_SE
  
  RETORNAR VERDADEIRO, "Username disponível"
FIM
```

---

## 📝 Observações e Ajustes

```
Data: ___/___/______

Participação da turma:
- 

Dificuldades principais:
- 

Ajustes realizados:
- 

Tempo real:
- Momento 1: _____ min
- Momento 2: _____ min
- Momento 3: _____ min
- Momento 4: _____ min
- Momento 5: _____ min

Próxima aula - ajustes:
- 
```

---

**Elaborado por:** Jeremias O Nunes  
**Data:** 2024  
**Versão:** 1.0  
**Status:** ✅ Pronto para aplicação
