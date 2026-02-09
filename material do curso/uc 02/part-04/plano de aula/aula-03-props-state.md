# Aula 03 - Propriedades (Props) e Estados (State)

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Gerenciamento de estado e comunicação entre componentes

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Diferenciar props de state
- ✅ Usar useState hook para gerenciar estado
- ✅ Criar componentes dinâmicos e interativos
- ✅ Passar dados entre componentes (pai → filho)
- ✅ Manipular eventos de usuário
- ✅ Implementar formulários controlados
- ✅ Entender ciclo de atualização de componentes

---

## 📚 Conteúdo Programático

### 1. Props (Propriedades)
- Passagem de dados pai → filho
- Props são imutáveis
- Desestruturação de props
- Props padrão

### 2. State (Estado)
- useState hook
- Estado local do componente
- Atualização de estado
- Estado é mutável

### 3. Ciclo de Atualização
- Renderização inicial
- Re-renderização ao mudar estado
- Performance e otimização

### 4. Componentes Dinâmicos
- Formulários controlados
- Listas dinâmicas
- Interatividade

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Estrutura de pastas
- Componentes reutilizáveis
- JSX e props básicas

**Atividade de Aquecimento:**
```
Discussão:
- Como um botão "sabe" que foi clicado?
- Como armazenar dados temporários no app?
- Qual a diferença entre dado fixo e dado que muda?

Objetivo: Preparar para conceito de estado
```

**Checkpoint:**
- Revisar componentes criados (Header, Button, Card)
- Demonstrar props em ação

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Props vs State (15 min)

**Comparação:**

| Aspecto | Props | State |
|---------|-------|-------|
| **Origem** | Vem do componente pai | Criado no próprio componente |
| **Mutabilidade** | Imutável (read-only) | Mutável (pode ser alterado) |
| **Uso** | Passar dados entre componentes | Armazenar dados locais |
| **Atualização** | Pai atualiza e passa novo valor | Componente atualiza com setState |

**Exemplo Visual:**

```
ComponentePai (state: nome = "João")
    ↓ props
ComponenteFilho (recebe props.nome)
    → Exibe: "Olá, João"
```

**Props - Dados de Entrada:**
```jsx
// Pai passa dados
<Button title="Entrar" color="blue" />

// Filho recebe dados
function Button({ title, color }) {
  return <Text style={{ color }}>{title}</Text>;
}
```

**State - Dados Internos:**
```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <View>
      <Text>{count}</Text>
      <Button title="+" onPress={() => setCount(count + 1)} />
    </View>
  );
}
```

#### 📖 Parte 2: useState Hook (20 min)

**Sintaxe:**
```jsx
const [valor, setValor] = useState(valorInicial);
```

- `valor`: variável que armazena o estado
- `setValor`: função para atualizar o estado
- `valorInicial`: valor inicial do estado

**Exemplos:**

```jsx
// Estado simples
const [nome, setNome] = useState('');
const [idade, setIdade] = useState(0);
const [ativo, setAtivo] = useState(false);

// Estado objeto
const [usuario, setUsuario] = useState({
  nome: '',
  email: '',
  senha: ''
});

// Estado array
const [categorias, setCategorias] = useState([]);
```

**Atualizar Estado:**

```jsx
// Valor simples
setNome('João');
setIdade(25);
setAtivo(true);

// Baseado no valor anterior
setCount(count + 1);
setCount(prevCount => prevCount + 1); // Mais seguro

// Objeto (spread operator)
setUsuario({ ...usuario, nome: 'João' });

// Array
setCategorias([...categorias, novaCategoria]);
```

**Regras Importantes:**
1. ❌ Nunca modificar estado diretamente: `count = count + 1`
2. ✅ Sempre usar função set: `setCount(count + 1)`
3. ❌ Não usar estado imediatamente após set (assíncrono)
4. ✅ Estado atualiza na próxima renderização

#### 📖 Parte 3: Formulários Controlados (15 min)

**Input Controlado:**

```jsx
import { useState } from 'react';
import { TextInput } from 'react-native';

function LoginForm() {
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');

  return (
    <View>
      <TextInput
        value={email}
        onChangeText={setEmail}
        placeholder="Email"
      />
      
      <TextInput
        value={senha}
        onChangeText={setSenha}
        placeholder="Senha"
        secureTextEntry
      />
      
      <Button 
        title="Entrar"
        onPress={() => console.log(email, senha)}
      />
    </View>
  );
}
```

**Por que "Controlado"?**
- React controla o valor do input
- Valor sempre sincronizado com estado
- Facilita validação e manipulação

#### 📖 Parte 4: Ciclo de Atualização (10 min)

**Fluxo:**

```
1. Componente renderiza (primeira vez)
   ↓
2. Usuário interage (clica, digita)
   ↓
3. Estado é atualizado (setState)
   ↓
4. Componente re-renderiza
   ↓
5. UI atualiza na tela
```

**Exemplo:**

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  
  console.log('Renderizou! Count:', count);
  
  return (
    <View>
      <Text>{count}</Text>
      <Button onPress={() => setCount(count + 1)} />
    </View>
  );
}

// Saída no console:
// Renderizou! Count: 0
// (usuário clica)
// Renderizou! Count: 1
// (usuário clica)
// Renderizou! Count: 2
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Contador Simples (20 min)

**Arquivo:** `src/screens/CounterScreen.js`

```jsx
import { useState } from 'react';
import { View, Text, StyleSheet } from 'react-native';
import Button from '../components/Button';
import Header from '../components/Header';
import colors from '../styles/colors';

export default function CounterScreen() {
  const [count, setCount] = useState(0);

  return (
    <View style={styles.container}>
      <Header title="Contador" />
      
      <View style={styles.content}>
        <Text style={styles.count}>{count}</Text>
        
        <View style={styles.buttons}>
          <Button 
            title="-" 
            onPress={() => setCount(count - 1)}
          />
          
          <Button 
            title="Reset" 
            variant="secondary"
            onPress={() => setCount(0)}
          />
          
          <Button 
            title="+" 
            onPress={() => setCount(count + 1)}
          />
        </View>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  content: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  count: {
    fontSize: 72,
    fontWeight: 'bold',
    color: colors.primary,
    marginBottom: 40,
  },
  buttons: {
    flexDirection: 'row',
    gap: 15,
  },
});
```

**Testar no App.js:**
```jsx
import CounterScreen from './src/screens/CounterScreen';

export default function App() {
  return <CounterScreen />;
}
```

#### 💻 Exercício 2: Formulário de Login (30 min)

**Atualizar:** `src/components/Input.js`

```jsx
import { TextInput, StyleSheet } from 'react-native';
import colors from '../styles/colors';

export default function Input({ 
  placeholder, 
  value, 
  onChangeText, 
  secureTextEntry,
  keyboardType = 'default'
}) {
  return (
    <TextInput
      style={styles.input}
      placeholder={placeholder}
      value={value}
      onChangeText={onChangeText}
      secureTextEntry={secureTextEntry}
      keyboardType={keyboardType}
      placeholderTextColor={colors.gray}
    />
  );
}

const styles = StyleSheet.create({
  input: {
    backgroundColor: colors.white,
    borderRadius: 10,
    padding: 15,
    fontSize: 16,
    borderWidth: 1,
    borderColor: '#ddd',
    width: '100%',
  },
});
```

**Criar:** `src/screens/LoginScreen.js`

```jsx
import { useState } from 'react';
import { View, Text, StyleSheet, Alert } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function LoginScreen() {
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');

  const handleLogin = () => {
    if (!email || !senha) {
      Alert.alert('Erro', 'Preencha todos os campos');
      return;
    }

    Alert.alert('Login', `Email: ${email}\nSenha: ${senha}`);
  };

  return (
    <View style={styles.container}>
      <Header title="Login" subtitle="Entre na sua conta" />
      
      <View style={styles.content}>
        <Input
          placeholder="Email"
          value={email}
          onChangeText={setEmail}
          keyboardType="email-address"
        />
        
        <Input
          placeholder="Senha"
          value={senha}
          onChangeText={setSenha}
          secureTextEntry
        />
        
        <Button 
          title="Entrar" 
          onPress={handleLogin}
        />
        
        <Text style={styles.debug}>
          Email: {email}{'\n'}
          Senha: {senha}
        </Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  content: {
    flex: 1,
    padding: 20,
    gap: 15,
  },
  debug: {
    marginTop: 20,
    color: colors.gray,
    fontSize: 12,
  },
});
```

#### 💻 Exercício 3: Lista de Categorias Selecionável (40 min)

**Criar:** `src/components/CategoryCard.js`

```jsx
import { TouchableOpacity, Text, StyleSheet } from 'react-native';
import colors from '../styles/colors';

export default function CategoryCard({ 
  icon, 
  title, 
  description, 
  selected,
  onPress 
}) {
  return (
    <TouchableOpacity 
      style={[
        styles.container,
        selected && styles.selected
      ]}
      onPress={onPress}
    >
      <Text style={styles.icon}>{icon}</Text>
      <Text style={styles.title}>{title}</Text>
      <Text style={styles.description}>{description}</Text>
      {selected && <Text style={styles.check}>✓</Text>}
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: colors.white,
    borderRadius: 15,
    padding: 20,
    margin: 10,
    alignItems: 'center',
    borderWidth: 2,
    borderColor: 'transparent',
  },
  selected: {
    borderColor: colors.primary,
    backgroundColor: '#F0EFFF',
  },
  icon: {
    fontSize: 48,
    marginBottom: 10,
  },
  title: {
    fontSize: 18,
    fontWeight: 'bold',
    color: colors.black,
    marginBottom: 5,
  },
  description: {
    fontSize: 14,
    color: colors.gray,
    textAlign: 'center',
  },
  check: {
    position: 'absolute',
    top: 10,
    right: 10,
    fontSize: 24,
    color: colors.primary,
  },
});
```

**Criar:** `src/screens/CategoryScreen.js`

```jsx
import { useState } from 'react';
import { View, StyleSheet, ScrollView, Alert } from 'react-native';
import Header from '../components/Header';
import CategoryCard from '../components/CategoryCard';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function CategoryScreen() {
  const [selectedId, setSelectedId] = useState(null);

  const categorias = [
    { id: 1, icon: '🎬', title: 'Filmes', description: 'Converse sobre cinema' },
    { id: 2, icon: '🎮', title: 'Jogos', description: 'Converse sobre games' },
    { id: 3, icon: '📺', title: 'Séries', description: 'Converse sobre séries' },
    { id: 4, icon: '🎵', title: 'Música', description: 'Converse sobre música' },
  ];

  const handleEntrarFila = () => {
    if (!selectedId) {
      Alert.alert('Atenção', 'Selecione uma categoria');
      return;
    }

    const categoria = categorias.find(c => c.id === selectedId);
    Alert.alert('Fila', `Entrando na fila de ${categoria.title}`);
  };

  return (
    <View style={styles.container}>
      <Header 
        title="Categorias" 
        subtitle="Escolha um tema para conversar" 
      />
      
      <ScrollView style={styles.content}>
        {categorias.map(cat => (
          <CategoryCard
            key={cat.id}
            icon={cat.icon}
            title={cat.title}
            description={cat.description}
            selected={selectedId === cat.id}
            onPress={() => setSelectedId(cat.id)}
          />
        ))}
      </ScrollView>

      <View style={styles.footer}>
        <Button 
          title="Entrar na Fila" 
          onPress={handleEntrarFila}
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  content: {
    flex: 1,
  },
  footer: {
    padding: 20,
    backgroundColor: colors.white,
  },
});
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Formulário de Cadastro (30 min)

**Tarefa:** Criar tela de cadastro completa

**Arquivo:** `src/screens/RegisterScreen.js`

**Requisitos:**
- Campos: username, email, senha, confirmar senha
- Validações:
  - Todos os campos obrigatórios
  - Email deve conter @
  - Senha mínimo 6 caracteres
  - Senhas devem ser iguais
- Mostrar mensagens de erro
- Botão "Cadastrar"

**Estrutura:**
```jsx
import { useState } from 'react';
import { View, StyleSheet, Alert } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function RegisterScreen() {
  const [username, setUsername] = useState('');
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');
  const [confirmarSenha, setConfirmarSenha] = useState('');

  const handleCadastro = () => {
    // Validações
    if (!username || !email || !senha || !confirmarSenha) {
      Alert.alert('Erro', 'Preencha todos os campos');
      return;
    }

    if (!email.includes('@')) {
      Alert.alert('Erro', 'Email inválido');
      return;
    }

    if (senha.length < 6) {
      Alert.alert('Erro', 'Senha deve ter no mínimo 6 caracteres');
      return;
    }

    if (senha !== confirmarSenha) {
      Alert.alert('Erro', 'Senhas não conferem');
      return;
    }

    Alert.alert('Sucesso', 'Cadastro realizado!');
  };

  return (
    <View style={styles.container}>
      <Header title="Cadastro" subtitle="Crie sua conta" />
      
      <View style={styles.content}>
        <Input
          placeholder="Username"
          value={username}
          onChangeText={setUsername}
        />
        
        <Input
          placeholder="Email"
          value={email}
          onChangeText={setEmail}
          keyboardType="email-address"
        />
        
        <Input
          placeholder="Senha"
          value={senha}
          onChangeText={setSenha}
          secureTextEntry
        />
        
        <Input
          placeholder="Confirmar Senha"
          value={confirmarSenha}
          onChangeText={setConfirmarSenha}
          secureTextEntry
        />
        
        <Button 
          title="Cadastrar" 
          onPress={handleCadastro}
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  content: {
    flex: 1,
    padding: 20,
    gap: 15,
  },
});
```

#### 🎯 Desafio 2: Perfil de Usuário (30 min)

**Tarefa:** Criar tela de perfil com dados editáveis

**Arquivo:** `src/screens/ProfileScreen.js`

**Requisitos:**
- Exibir dados do usuário (nome, email, bio)
- Botão "Editar" que habilita campos
- Botão "Salvar" que salva alterações
- Contador de conversas (mock)
- Categoria favorita

**Estrutura:**
```jsx
import { useState } from 'react';
import { View, Text, StyleSheet, Alert } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function ProfileScreen() {
  const [editando, setEditando] = useState(false);
  const [nome, setNome] = useState('João Silva');
  const [email, setEmail] = useState('joao@email.com');
  const [bio, setBio] = useState('Adoro conversar sobre filmes!');

  const handleSalvar = () => {
    Alert.alert('Sucesso', 'Perfil atualizado!');
    setEditando(false);
  };

  return (
    <View style={styles.container}>
      <Header title="Perfil" />
      
      <View style={styles.content}>
        <Text style={styles.avatar}>👤</Text>
        
        <View style={styles.stats}>
          <View style={styles.stat}>
            <Text style={styles.statNumber}>42</Text>
            <Text style={styles.statLabel}>Conversas</Text>
          </View>
          <View style={styles.stat}>
            <Text style={styles.statNumber}>🎬</Text>
            <Text style={styles.statLabel}>Favorita</Text>
          </View>
        </View>

        <Input
          placeholder="Nome"
          value={nome}
          onChangeText={setNome}
          editable={editando}
        />
        
        <Input
          placeholder="Email"
          value={email}
          onChangeText={setEmail}
          editable={editando}
        />
        
        <Input
          placeholder="Bio"
          value={bio}
          onChangeText={setBio}
          editable={editando}
        />
        
        {editando ? (
          <Button title="Salvar" onPress={handleSalvar} />
        ) : (
          <Button 
            title="Editar" 
            variant="secondary"
            onPress={() => setEditando(true)} 
          />
        )}
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  content: {
    flex: 1,
    padding: 20,
    gap: 15,
  },
  avatar: {
    fontSize: 80,
    textAlign: 'center',
    marginVertical: 20,
  },
  stats: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 20,
  },
  stat: {
    alignItems: 'center',
  },
  statNumber: {
    fontSize: 32,
    fontWeight: 'bold',
    color: colors.primary,
  },
  statLabel: {
    fontSize: 14,
    color: colors.gray,
  },
});
```

**Checklist:**
- [ ] RegisterScreen com validações
- [ ] ProfileScreen com modo edição
- [ ] Todos os estados funcionando
- [ ] Validações implementadas

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **Qual a diferença entre props e state?**
   - Props: dados de entrada (imutáveis) / State: dados internos (mutáveis)

2. **Como atualizar estado?**
   - Usar função set: setCount(count + 1)

3. **O que é formulário controlado?**
   - Input cujo valor é controlado pelo estado React

4. **Quando o componente re-renderiza?**
   - Quando o estado é atualizado

#### 🎯 Fluxo de Estado

```
Usuário digita no Input
    ↓
onChangeText dispara
    ↓
setEmail(novoValor)
    ↓
Estado atualiza
    ↓
Componente re-renderiza
    ↓
Input mostra novo valor
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Diferenciar props de state
- [ ] Usar useState
- [ ] Criar formulários controlados
- [ ] Atualizar estado corretamente
- [ ] Validar dados de entrada
- [ ] Criar componentes interativos

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar mais validações
   - Criar tela de configurações
   - Implementar toggle (switch)

2. **Estudo:**
   - Ler sobre useEffect (próxima aula)
   - Explorar outros hooks

---

## 📊 Avaliação

### Critérios (Peso: 20% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **useState** | 30% | Uso correto do hook |
| **Formulários** | 30% | Inputs controlados |
| **Validações** | 25% | Regras implementadas |
| **Interatividade** | 15% | Seleção de categorias |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar todos os exemplos
- [ ] Preparar demonstração de re-renderização
- [ ] Revisar useState

### Pontos de Atenção
- ⚠️ Alunos modificam estado diretamente
- ⚠️ Confusão entre props e state
- ⚠️ Esquecem que setState é assíncrono
- ⚠️ Não entendem re-renderização

### Troubleshooting

**Problema:** "Estado não atualiza"
**Solução:** Verificar se está usando função set

**Problema:** "Input não digita"
**Solução:** Verificar value e onChangeText

---

## 📎 Recursos Adicionais

- [React useState](https://react.dev/reference/react/useState)
- [React Native TextInput](https://reactnative.dev/docs/textinput)

### Próxima Aula
**Aula 04 - Navegação entre Telas**
- React Navigation
- Stack Navigator
- Passar dados entre telas
- Tab Navigator

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
