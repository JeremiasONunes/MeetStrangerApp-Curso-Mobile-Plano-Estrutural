# Aula 02 - Estrutura do Projeto e Componentização

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Organização de projeto e criação de componentes reutilizáveis

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Organizar projeto React Native em estrutura profissional
- ✅ Criar componentes reutilizáveis
- ✅ Entender e aplicar JSX corretamente
- ✅ Separar lógica de apresentação
- ✅ Aplicar boas práticas de componentização
- ✅ Criar componentes Header, Button e Card

---

## 📚 Conteúdo Programático

### 1. Estrutura de Pastas
- Organização por feature vs por tipo
- Separação de componentes, telas e serviços
- Assets e configurações

### 2. Conceito de Componentes
- Componentes funcionais
- Props (propriedades)
- Reutilização de código
- Composição de componentes

### 3. JSX
- Sintaxe e regras
- Expressões JavaScript em JSX
- Renderização condicional
- Listas

### 4. Boas Práticas
- Nomenclatura de componentes
- Componentes pequenos e focados
- Separação de responsabilidades

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Arquitetura MeetStranger
- Configuração do ambiente
- Primeiro app React Native

**Atividade de Aquecimento:**
```
Discussão:
- Por que organizar código em pastas?
- O que é um componente reutilizável?
- Qual a vantagem de separar Header em componente próprio?

Objetivo: Preparar para componentização
```

**Checkpoint:**
- Verificar se todos têm app rodando
- Revisar estrutura básica do App.js

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Estrutura de Pastas (15 min)

**Estrutura Proposta para MeetStranger:**

```
meetstranger-mobile/
├── src/
│   ├── components/       # Componentes reutilizáveis
│   │   ├── Header.js
│   │   ├── Button.js
│   │   └── Card.js
│   ├── screens/          # Telas do app
│   │   ├── HomeScreen.js
│   │   ├── LoginScreen.js
│   │   └── RegisterScreen.js
│   ├── services/         # Comunicação com API
│   │   └── api.js
│   ├── styles/           # Estilos globais
│   │   └── colors.js
│   └── utils/            # Funções auxiliares
│       └── validation.js
├── assets/               # Imagens, fontes
├── App.js                # Componente raiz
└── package.json
```

**Por que essa estrutura?**
- ✅ Fácil de encontrar arquivos
- ✅ Escalável
- ✅ Separação clara de responsabilidades
- ✅ Padrão da indústria

#### 📖 Parte 2: Componentes Funcionais (20 min)

**O que é um Componente?**
- Bloco de código reutilizável
- Recebe props (entrada)
- Retorna JSX (saída)
- Pode ter estado próprio

**Anatomia de um Componente:**

```jsx
import { View, Text, StyleSheet } from 'react-native';

// Componente funcional
function Header(props) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>{props.title}</Text>
    </View>
  );
}

// Estilos
const styles = StyleSheet.create({
  container: {
    padding: 20,
    backgroundColor: '#6C63FF',
  },
  title: {
    fontSize: 24,
    color: '#fff',
    fontWeight: 'bold',
  },
});

export default Header;
```

**Usando o Componente:**

```jsx
import Header from './components/Header';

function App() {
  return (
    <View>
      <Header title="MeetStranger" />
    </View>
  );
}
```

**Props (Propriedades):**
- Dados passados de pai para filho
- Imutáveis (não podem ser alterados pelo filho)
- Permitem reutilização

```jsx
// Diferentes usos do mesmo componente
<Header title="MeetStranger" />
<Header title="Perfil" />
<Header title="Configurações" />
```

#### 📖 Parte 3: JSX em Profundidade (15 min)

**Regras do JSX:**

1. **Um elemento raiz:**
```jsx
// ❌ Errado
return (
  <Text>Título</Text>
  <Text>Subtítulo</Text>
);

// ✅ Correto
return (
  <View>
    <Text>Título</Text>
    <Text>Subtítulo</Text>
  </View>
);
```

2. **Expressões JavaScript com {}:**
```jsx
const nome = "João";
const idade = 25;

<Text>Olá, {nome}!</Text>
<Text>Você tem {idade} anos</Text>
<Text>Ano que vem: {idade + 1}</Text>
```

3. **Atributos em camelCase:**
```jsx
// HTML: background-color
// JSX: backgroundColor

<View style={{ backgroundColor: '#fff' }} />
```

4. **className vira style:**
```jsx
// HTML: <div class="container">
// JSX: <View style={styles.container}>
```

**Renderização Condicional:**

```jsx
const isLoggedIn = true;

// Operador ternário
{isLoggedIn ? <Text>Bem-vindo!</Text> : <Text>Faça login</Text>}

// Operador &&
{isLoggedIn && <Text>Você está logado</Text>}
```

**Renderização de Listas:**

```jsx
const categorias = ['Filmes', 'Jogos', 'Séries'];

{categorias.map((cat, index) => (
  <Text key={index}>{cat}</Text>
))}
```

#### 📖 Parte 4: Boas Práticas (10 min)

**Nomenclatura:**
- Componentes: PascalCase (Header, Button, UserCard)
- Arquivos: PascalCase (Header.js, Button.js)
- Variáveis: camelCase (userName, isActive)
- Constantes: UPPER_CASE (API_URL, MAX_LENGTH)

**Componentes Pequenos:**
```jsx
// ❌ Componente muito grande
function HomeScreen() {
  return (
    <View>
      <View style={styles.header}>
        <Text>MeetStranger</Text>
        <TouchableOpacity><Text>Menu</Text></TouchableOpacity>
      </View>
      <View style={styles.content}>
        {/* 100 linhas de código */}
      </View>
      <View style={styles.footer}>
        <Text>© 2024</Text>
      </View>
    </View>
  );
}

// ✅ Componentes separados
function HomeScreen() {
  return (
    <View>
      <Header />
      <Content />
      <Footer />
    </View>
  );
}
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Criar Estrutura de Pastas (15 min)

**Criar pastas:**

```bash
cd meetstranger-mobile

mkdir src
mkdir src\components
mkdir src\screens
mkdir src\styles
mkdir src\services
```

**Criar arquivo de cores:** `src/styles/colors.js`

```javascript
export default {
  primary: '#6C63FF',
  secondary: '#FF6584',
  background: '#F5F5F5',
  white: '#FFFFFF',
  black: '#000000',
  gray: '#999999',
  success: '#4CAF50',
  error: '#F44336',
};
```

#### 💻 Exercício 2: Criar Componente Header (25 min)

**Arquivo:** `src/components/Header.js`

```jsx
import { View, Text, StyleSheet } from 'react-native';
import colors from '../styles/colors';

export default function Header({ title, subtitle }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>{title}</Text>
      {subtitle && <Text style={styles.subtitle}>{subtitle}</Text>}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: colors.primary,
    padding: 20,
    paddingTop: 50,
    alignItems: 'center',
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: colors.white,
  },
  subtitle: {
    fontSize: 14,
    color: colors.white,
    marginTop: 5,
  },
});
```

**Testar no App.js:**

```jsx
import { View, StyleSheet } from 'react-native';
import Header from './src/components/Header';

export default function App() {
  return (
    <View style={styles.container}>
      <Header title="MeetStranger" subtitle="Converse anonimamente" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
});
```

#### 💻 Exercício 3: Criar Componente Button (25 min)

**Arquivo:** `src/components/Button.js`

```jsx
import { TouchableOpacity, Text, StyleSheet } from 'react-native';
import colors from '../styles/colors';

export default function Button({ title, onPress, variant = 'primary' }) {
  return (
    <TouchableOpacity 
      style={[
        styles.button, 
        variant === 'secondary' && styles.buttonSecondary
      ]}
      onPress={onPress}
    >
      <Text style={[
        styles.text,
        variant === 'secondary' && styles.textSecondary
      ]}>
        {title}
      </Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: colors.primary,
    paddingVertical: 15,
    paddingHorizontal: 40,
    borderRadius: 25,
    alignItems: 'center',
  },
  buttonSecondary: {
    backgroundColor: colors.white,
    borderWidth: 2,
    borderColor: colors.primary,
  },
  text: {
    color: colors.white,
    fontSize: 16,
    fontWeight: 'bold',
  },
  textSecondary: {
    color: colors.primary,
  },
});
```

**Testar no App.js:**

```jsx
import { View, StyleSheet, Alert } from 'react-native';
import Header from './src/components/Header';
import Button from './src/components/Button';

export default function App() {
  return (
    <View style={styles.container}>
      <Header title="MeetStranger" subtitle="Converse anonimamente" />
      
      <View style={styles.content}>
        <Button 
          title="Entrar" 
          onPress={() => Alert.alert('Entrar clicado')}
        />
        
        <Button 
          title="Cadastrar" 
          variant="secondary"
          onPress={() => Alert.alert('Cadastrar clicado')}
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  content: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    gap: 15,
  },
});
```

#### 💻 Exercício 4: Criar Componente Card (25 min)

**Arquivo:** `src/components/Card.js`

```jsx
import { View, Text, StyleSheet } from 'react-native';
import colors from '../styles/colors';

export default function Card({ icon, title, description }) {
  return (
    <View style={styles.container}>
      <Text style={styles.icon}>{icon}</Text>
      <Text style={styles.title}>{title}</Text>
      <Text style={styles.description}>{description}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: colors.white,
    borderRadius: 15,
    padding: 20,
    margin: 10,
    alignItems: 'center',
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3,
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
});
```

**Testar com lista de categorias:**

```jsx
import { View, StyleSheet, ScrollView } from 'react-native';
import Header from './src/components/Header';
import Card from './src/components/Card';
import colors from './src/styles/colors';

export default function App() {
  const categorias = [
    { id: 1, icon: '🎬', title: 'Filmes', description: 'Converse sobre cinema' },
    { id: 2, icon: '🎮', title: 'Jogos', description: 'Converse sobre games' },
    { id: 3, icon: '📺', title: 'Séries', description: 'Converse sobre séries' },
  ];

  return (
    <View style={styles.container}>
      <Header title="Categorias" subtitle="Escolha um tema" />
      
      <ScrollView style={styles.content}>
        {categorias.map(cat => (
          <Card 
            key={cat.id}
            icon={cat.icon}
            title={cat.title}
            description={cat.description}
          />
        ))}
      </ScrollView>
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
});
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Criar Componente Input (30 min)

**Tarefa:** Criar componente de input reutilizável

**Arquivo:** `src/components/Input.js`

**Requisitos:**
- Receber props: placeholder, value, onChangeText, secureTextEntry
- Estilizar com borda arredondada
- Usar cores do colors.js
- Ícone opcional

**Exemplo de uso:**
```jsx
<Input 
  placeholder="Email"
  value={email}
  onChangeText={setEmail}
/>

<Input 
  placeholder="Senha"
  value={senha}
  onChangeText={setSenha}
  secureTextEntry
/>
```

**Dica:**
```jsx
import { TextInput, StyleSheet } from 'react-native';

export default function Input({ placeholder, value, onChangeText, secureTextEntry }) {
  return (
    <TextInput
      style={styles.input}
      placeholder={placeholder}
      value={value}
      onChangeText={onChangeText}
      secureTextEntry={secureTextEntry}
      placeholderTextColor="#999"
    />
  );
}

const styles = StyleSheet.create({
  input: {
    backgroundColor: '#fff',
    borderRadius: 10,
    padding: 15,
    fontSize: 16,
    borderWidth: 1,
    borderColor: '#ddd',
  },
});
```

#### 🎯 Desafio 2: Criar HomeScreen (30 min)

**Tarefa:** Criar primeira tela completa

**Arquivo:** `src/screens/HomeScreen.js`

**Requisitos:**
- Usar componente Header
- Usar componente Button
- Usar componente Card
- Exibir 3 categorias
- Botão "Entrar na Fila"

**Estrutura:**
```jsx
import { View, StyleSheet, ScrollView } from 'react-native';
import Header from '../components/Header';
import Card from '../components/Card';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function HomeScreen() {
  const categorias = [
    { id: 1, icon: '🎬', title: 'Filmes', description: 'Converse sobre cinema' },
    { id: 2, icon: '🎮', title: 'Jogos', description: 'Converse sobre games' },
    { id: 3, icon: '📺', title: 'Séries', description: 'Converse sobre séries' },
  ];

  return (
    <View style={styles.container}>
      <Header title="MeetStranger" subtitle="Escolha uma categoria" />
      
      <ScrollView style={styles.content}>
        {categorias.map(cat => (
          <Card 
            key={cat.id}
            icon={cat.icon}
            title={cat.title}
            description={cat.description}
          />
        ))}
      </ScrollView>

      <View style={styles.footer}>
        <Button title="Entrar na Fila" onPress={() => {}} />
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

**Atualizar App.js:**
```jsx
import HomeScreen from './src/screens/HomeScreen';

export default function App() {
  return <HomeScreen />;
}
```

**Checklist:**
- [ ] Input component criado
- [ ] HomeScreen criada
- [ ] Todos os componentes funcionando
- [ ] App.js usando HomeScreen

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **O que é um componente?**
   - Bloco de código reutilizável que retorna JSX

2. **O que são props?**
   - Dados passados de pai para filho

3. **Por que componentizar?**
   - Reutilização, organização, manutenção

4. **Qual a regra principal do JSX?**
   - Um elemento raiz

#### 🎯 Estrutura do Projeto

```
src/
├── components/    # Header, Button, Card, Input
├── screens/       # HomeScreen
├── styles/        # colors.js
└── services/      # (próxima aula)
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Organizar projeto em pastas
- [ ] Criar componentes funcionais
- [ ] Usar props
- [ ] Aplicar JSX corretamente
- [ ] Renderizar listas
- [ ] Estilizar componentes
- [ ] Reutilizar componentes

#### 📚 Para Casa

1. **Implementação:**
   - Criar componente Footer
   - Adicionar mais categorias
   - Criar componente Avatar

2. **Estudo:**
   - Ler sobre useState (próxima aula)
   - Explorar componentes do React Native

---

## 📊 Avaliação

### Critérios (Peso: 15% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Estrutura de Pastas** | 25% | Organização correta |
| **Componentes** | 40% | Header, Button, Card, Input |
| **Reutilização** | 20% | Props usadas corretamente |
| **HomeScreen** | 15% | Tela completa funcionando |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar todos os componentes
- [ ] Preparar exemplos de props
- [ ] Revisar JSX

### Pontos de Atenção
- ⚠️ Alunos esquecem export default
- ⚠️ Confusão entre props e state
- ⚠️ Esquecem key em listas
- ⚠️ Erros de importação de paths

### Troubleshooting

**Problema:** "Cannot find module './src/components/Header'"
**Solução:** Verificar path relativo

**Problema:** "Each child should have unique key"
**Solução:** Adicionar key={id} em map

---

## 📎 Recursos Adicionais

- [React Components](https://react.dev/learn/your-first-component)
- [React Native Components](https://reactnative.dev/docs/components-and-apis)

### Próxima Aula
**Aula 03 - Estado e Interatividade**
- useState hook
- Eventos e interações
- Formulários
- Navegação entre telas

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
