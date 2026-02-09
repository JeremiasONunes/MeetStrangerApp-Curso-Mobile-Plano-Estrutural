# Aula 04 - Navegação entre Telas

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Implementação de navegação e fluxo de telas

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Instalar e configurar React Navigation
- ✅ Criar Stack Navigator
- ✅ Navegar entre telas (push, navigate, goBack)
- ✅ Passar parâmetros entre telas
- ✅ Estruturar fluxo de autenticação
- ✅ Implementar navegação completa do MeetStranger

---

## 📚 Conteúdo Programático

### 1. Conceito de Navegação Mobile
- Stack (pilha de telas)
- Tabs (abas)
- Drawer (menu lateral)
- Fluxo de navegação

### 2. React Navigation
- Instalação e configuração
- NavigationContainer
- Stack Navigator
- Navegação programática

### 3. Passagem de Parâmetros
- route.params
- navigation.navigate com params
- Atualização de tela com parâmetros

### 4. Fluxo do MeetStranger
- Telas de autenticação (Login, Register)
- Telas principais (Home, Categories, Chat)
- Telas de perfil

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Props e State
- useState hook
- Formulários controlados
- Componentes interativos

**Atividade de Aquecimento:**
```
Discussão:
- Como apps como Instagram navegam entre telas?
- O que acontece quando você clica "Voltar"?
- Como passar dados de uma tela para outra?

Objetivo: Preparar para conceito de navegação
```

**Checkpoint:**
- Revisar telas criadas (Login, Register, Category, Profile)
- Demonstrar necessidade de navegação

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Conceito de Navegação (15 min)

**Stack Navigator (Pilha):**

```
Tela 3 (Chat)         ← Topo da pilha
Tela 2 (Categories)
Tela 1 (Home)         ← Base da pilha
```

**Operações:**
- `push`: Adiciona tela no topo
- `pop/goBack`: Remove tela do topo
- `navigate`: Navega para tela específica
- `replace`: Substitui tela atual

**Fluxo MeetStranger:**

```
Login → Register
  ↓
Home → Categories → Chat → Profile
```

#### 📖 Parte 2: React Navigation (20 min)

**Instalação:**

```bash
npm install @react-navigation/native
npm install react-native-screens react-native-safe-area-context
npm install @react-navigation/native-stack
```

**Estrutura Básica:**

```jsx
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

**Navegação:**

```jsx
// Em qualquer tela
function HomeScreen({ navigation }) {
  return (
    <Button 
      title="Ir para Details"
      onPress={() => navigation.navigate('Details')}
    />
  );
}
```

#### 📖 Parte 3: Passagem de Parâmetros (15 min)

**Enviar Parâmetros:**

```jsx
navigation.navigate('Details', {
  userId: 123,
  userName: 'João'
});
```

**Receber Parâmetros:**

```jsx
function DetailsScreen({ route }) {
  const { userId, userName } = route.params;
  
  return <Text>Usuário: {userName} (ID: {userId})</Text>;
}
```

**Exemplo MeetStranger:**

```jsx
// CategoryScreen
navigation.navigate('Chat', {
  categoriaId: 1,
  categoriaNome: 'Filmes'
});

// ChatScreen
function ChatScreen({ route }) {
  const { categoriaId, categoriaNome } = route.params;
  return <Text>Chat de {categoriaNome}</Text>;
}
```

#### 📖 Parte 4: Configuração de Header (10 min)

**Opções de Tela:**

```jsx
<Stack.Screen 
  name="Home" 
  component={HomeScreen}
  options={{
    title: 'Início',
    headerStyle: { backgroundColor: '#6C63FF' },
    headerTintColor: '#fff',
    headerTitleStyle: { fontWeight: 'bold' }
  }}
/>
```

**Ocultar Header:**

```jsx
<Stack.Screen 
  name="Login" 
  component={LoginScreen}
  options={{ headerShown: false }}
/>
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Instalar React Navigation (15 min)

**Instalar dependências:**

```bash
cd meetstranger-mobile

npm install @react-navigation/native
npm install react-native-screens react-native-safe-area-context
npm install @react-navigation/native-stack
```

**Verificar instalação:**
- Verificar package.json
- Reiniciar Expo: `expo start --clear`

#### 💻 Exercício 2: Configurar Navegação Básica (25 min)

**Atualizar:** `App.js`

```jsx
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import LoginScreen from './src/screens/LoginScreen';
import RegisterScreen from './src/screens/RegisterScreen';
import HomeScreen from './src/screens/HomeScreen';

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator 
        initialRouteName="Login"
        screenOptions={{
          headerStyle: { backgroundColor: '#6C63FF' },
          headerTintColor: '#fff',
          headerTitleStyle: { fontWeight: 'bold' }
        }}
      >
        <Stack.Screen 
          name="Login" 
          component={LoginScreen}
          options={{ headerShown: false }}
        />
        <Stack.Screen 
          name="Register" 
          component={RegisterScreen}
          options={{ title: 'Cadastro' }}
        />
        <Stack.Screen 
          name="Home" 
          component={HomeScreen}
          options={{ 
            title: 'MeetStranger',
            headerLeft: () => null // Remove botão voltar
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

#### 💻 Exercício 3: Atualizar LoginScreen com Navegação (25 min)

**Atualizar:** `src/screens/LoginScreen.js`

```jsx
import { useState } from 'react';
import { View, Text, StyleSheet, Alert, TouchableOpacity } from 'react-native';
import Input from '../components/Input';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function LoginScreen({ navigation }) {
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');

  const handleLogin = () => {
    if (!email || !senha) {
      Alert.alert('Erro', 'Preencha todos os campos');
      return;
    }

    // Simular login bem-sucedido
    navigation.replace('Home');
  };

  return (
    <View style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.logo}>🎭</Text>
        <Text style={styles.title}>MeetStranger</Text>
        <Text style={styles.subtitle}>Converse anonimamente</Text>
      </View>
      
      <View style={styles.form}>
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

        <TouchableOpacity 
          onPress={() => navigation.navigate('Register')}
          style={styles.link}
        >
          <Text style={styles.linkText}>
            Não tem conta? Cadastre-se
          </Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.primary,
  },
  header: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  logo: {
    fontSize: 80,
    marginBottom: 20,
  },
  title: {
    fontSize: 32,
    fontWeight: 'bold',
    color: colors.white,
    marginBottom: 10,
  },
  subtitle: {
    fontSize: 16,
    color: colors.white,
  },
  form: {
    backgroundColor: colors.white,
    borderTopLeftRadius: 30,
    borderTopRightRadius: 30,
    padding: 30,
    gap: 15,
  },
  link: {
    marginTop: 15,
    alignItems: 'center',
  },
  linkText: {
    color: colors.primary,
    fontSize: 14,
  },
});
```

#### 💻 Exercício 4: Atualizar RegisterScreen (25 min)

**Atualizar:** `src/screens/RegisterScreen.js`

```jsx
import { useState } from 'react';
import { View, StyleSheet, Alert, TouchableOpacity, Text } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function RegisterScreen({ navigation }) {
  const [username, setUsername] = useState('');
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');
  const [confirmarSenha, setConfirmarSenha] = useState('');

  const handleCadastro = () => {
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

    Alert.alert('Sucesso', 'Cadastro realizado!', [
      { text: 'OK', onPress: () => navigation.replace('Home') }
    ]);
  };

  return (
    <View style={styles.container}>
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

        <TouchableOpacity 
          onPress={() => navigation.goBack()}
          style={styles.link}
        >
          <Text style={styles.linkText}>
            Já tem conta? Faça login
          </Text>
        </TouchableOpacity>
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
  link: {
    marginTop: 15,
    alignItems: 'center',
  },
  linkText: {
    color: colors.primary,
    fontSize: 14,
  },
});
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Adicionar Mais Telas ao Stack (30 min)

**Tarefa:** Adicionar CategoryScreen e ChatScreen à navegação

**Atualizar:** `App.js`

```jsx
import CategoryScreen from './src/screens/CategoryScreen';
import ChatScreen from './src/screens/ChatScreen';
import ProfileScreen from './src/screens/ProfileScreen';

// Adicionar no Stack.Navigator
<Stack.Screen 
  name="Category" 
  component={CategoryScreen}
  options={{ title: 'Categorias' }}
/>
<Stack.Screen 
  name="Chat" 
  component={ChatScreen}
  options={{ title: 'Chat' }}
/>
<Stack.Screen 
  name="Profile" 
  component={ProfileScreen}
  options={{ title: 'Perfil' }}
/>
```

**Atualizar:** `src/screens/HomeScreen.js`

```jsx
import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <View style={styles.content}>
        <Text style={styles.welcome}>Bem-vindo ao MeetStranger!</Text>
        <Text style={styles.description}>
          Converse anonimamente com pessoas que compartilham seus interesses
        </Text>

        <Button 
          title="Escolher Categoria"
          onPress={() => navigation.navigate('Category')}
        />

        <Button 
          title="Meu Perfil"
          variant="secondary"
          onPress={() => navigation.navigate('Profile')}
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
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    gap: 20,
  },
  welcome: {
    fontSize: 24,
    fontWeight: 'bold',
    color: colors.primary,
    textAlign: 'center',
  },
  description: {
    fontSize: 16,
    color: colors.gray,
    textAlign: 'center',
    marginBottom: 20,
  },
});
```

#### 🎯 Desafio 2: Implementar Navegação com Parâmetros (30 min)

**Tarefa:** Passar categoria selecionada para ChatScreen

**Atualizar:** `src/screens/CategoryScreen.js`

```jsx
const handleEntrarFila = () => {
  if (!selectedId) {
    Alert.alert('Atenção', 'Selecione uma categoria');
    return;
  }

  const categoria = categorias.find(c => c.id === selectedId);
  
  navigation.navigate('Chat', {
    categoriaId: categoria.id,
    categoriaNome: categoria.title,
    categoriaIcon: categoria.icon
  });
};
```

**Criar:** `src/screens/ChatScreen.js`

```jsx
import { View, Text, StyleSheet, ScrollView } from 'react-native';
import Button from '../components/Button';
import colors from '../styles/colors';

export default function ChatScreen({ route, navigation }) {
  const { categoriaId, categoriaNome, categoriaIcon } = route.params;

  const mensagens = [
    { id: 1, texto: 'Olá!', autor: 'outro' },
    { id: 2, texto: 'Oi! Tudo bem?', autor: 'eu' },
    { id: 3, texto: 'Você gosta de que tipo de filme?', autor: 'outro' },
  ];

  return (
    <View style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.icon}>{categoriaIcon}</Text>
        <Text style={styles.categoria}>{categoriaNome}</Text>
        <Text style={styles.status}>● Online</Text>
      </View>

      <ScrollView style={styles.messages}>
        {mensagens.map(msg => (
          <View 
            key={msg.id}
            style={[
              styles.message,
              msg.autor === 'eu' && styles.messageMe
            ]}
          >
            <Text style={styles.messageText}>{msg.texto}</Text>
          </View>
        ))}
      </ScrollView>

      <View style={styles.footer}>
        <Button 
          title="Encerrar Chat"
          variant="secondary"
          onPress={() => navigation.navigate('Home')}
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
  header: {
    backgroundColor: colors.white,
    padding: 15,
    alignItems: 'center',
    borderBottomWidth: 1,
    borderBottomColor: '#ddd',
  },
  icon: {
    fontSize: 32,
  },
  categoria: {
    fontSize: 18,
    fontWeight: 'bold',
    color: colors.black,
    marginTop: 5,
  },
  status: {
    fontSize: 12,
    color: colors.success,
    marginTop: 5,
  },
  messages: {
    flex: 1,
    padding: 15,
  },
  message: {
    backgroundColor: colors.white,
    padding: 15,
    borderRadius: 15,
    marginBottom: 10,
    maxWidth: '80%',
  },
  messageMe: {
    backgroundColor: colors.primary,
    alignSelf: 'flex-end',
  },
  messageText: {
    fontSize: 16,
    color: colors.black,
  },
  footer: {
    padding: 15,
    backgroundColor: colors.white,
  },
});
```

**Checklist:**
- [ ] Todas as telas no Stack
- [ ] Navegação funcionando
- [ ] Parâmetros sendo passados
- [ ] ChatScreen exibindo categoria

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **O que é Stack Navigator?**
   - Pilha de telas, última entra primeira sai

2. **Diferença entre navigate e replace?**
   - navigate: adiciona na pilha / replace: substitui tela atual

3. **Como passar dados entre telas?**
   - navigation.navigate('Tela', { param: valor })

4. **Como receber parâmetros?**
   - route.params.param

#### 🎯 Fluxo de Navegação MeetStranger

```
Login ──→ Register
  ↓
Home ──→ Category ──→ Chat
  ↓
Profile
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Instalar React Navigation
- [ ] Criar Stack Navigator
- [ ] Navegar entre telas
- [ ] Passar parâmetros
- [ ] Configurar header
- [ ] Usar navigation.goBack()
- [ ] Usar navigation.replace()

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar botão "Sair" que volta para Login
   - Criar tela de Estatísticas
   - Adicionar navegação para Estatísticas

2. **Estudo:**
   - Ler sobre Tab Navigator
   - Explorar outras opções de navegação

---

## 📊 Avaliação

### Critérios (Peso: 20% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Configuração** | 25% | React Navigation instalado |
| **Stack Navigator** | 30% | Todas as telas configuradas |
| **Navegação** | 25% | Fluxo funcionando |
| **Parâmetros** | 20% | Dados passados corretamente |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar instalação do React Navigation
- [ ] Preparar exemplos de navegação
- [ ] Revisar conceito de Stack

### Pontos de Atenção
- ⚠️ Erros de instalação de dependências
- ⚠️ Confusão entre navigate e replace
- ⚠️ Esquecem NavigationContainer
- ⚠️ Problemas com route.params undefined

### Troubleshooting

**Problema:** "Cannot read property 'navigate' of undefined"
**Solução:** Verificar se tela está no Stack Navigator

**Problema:** "route.params is undefined"
**Solução:** Verificar se parâmetros foram passados

**Problema:** "Invariant Violation: requireNativeComponent"
**Solução:** Reiniciar Expo: `expo start --clear`

---

## 📎 Recursos Adicionais

- [React Navigation Docs](https://reactnavigation.org/)
- [Stack Navigator](https://reactnavigation.org/docs/stack-navigator/)

### Próxima Aula
**Aula 05 - Integração com API Backend**
- Fetch e Axios
- Consumir endpoints do backend
- Autenticação com JWT
- AsyncStorage

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
