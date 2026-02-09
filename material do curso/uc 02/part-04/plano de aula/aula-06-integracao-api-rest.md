# Aula 06 - Integração com APIs REST (Backend MeetStranger)

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Integração frontend-backend via APIs REST

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Compreender comunicação cliente-servidor via HTTP
- ✅ Consumir APIs REST com fetch e axios
- ✅ Integrar frontend React Native com backend Node.js
- ✅ Implementar autenticação com JWT
- ✅ Armazenar token com AsyncStorage
- ✅ Fazer requisições autenticadas
- ✅ Tratar erros de API

---

## 📚 Conteúdo Programático

### 1. Conceito de APIs REST
- Cliente-servidor
- Requisições HTTP
- JSON como formato de dados
- Status codes

### 2. Métodos HTTP
- GET: Buscar dados
- POST: Criar dados
- PUT: Atualizar dados
- DELETE: Remover dados

### 3. Fetch vs Axios
- Fetch API nativa
- Axios (biblioteca)
- Configuração de headers
- Interceptors

### 4. Autenticação JWT
- Login e obtenção de token
- Armazenamento com AsyncStorage
- Envio de token em requisições
- Logout

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- FlatList e renderização de listas
- Manipulação de dados
- Estados loading/empty/error

**Atividade de Aquecimento:**
```
Discussão:
- Como o app Instagram busca posts do servidor?
- O que acontece quando você faz login?
- Como o app "lembra" que você está logado?

Objetivo: Preparar para integração com API
```

**Checkpoint:**
- Revisar backend criado na Part 03
- Verificar se backend está rodando (localhost:3000)
- Testar endpoints com Thunder Client

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Comunicação HTTP (15 min)

**Fluxo Cliente-Servidor:**

```
App Mobile (Frontend)
    ↓ HTTP Request
    ↓ GET /usuarios
API Backend
    ↓ SQL Query
Banco de Dados
    ↓ Retorna dados
API Backend
    ↓ HTTP Response (JSON)
App Mobile
    ↓ Exibe na tela
```

**Requisição HTTP:**
```
GET /usuarios HTTP/1.1
Host: localhost:3000
Authorization: Bearer eyJhbGc...
Content-Type: application/json
```

**Resposta HTTP:**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "username": "joao123",
  "email": "joao@email.com"
}
```

#### 📖 Parte 2: Fetch API (15 min)

**GET Request:**
```javascript
const response = await fetch('http://localhost:3000/usuarios');
const data = await response.json();
console.log(data);
```

**POST Request:**
```javascript
const response = await fetch('http://localhost:3000/usuarios', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    username: 'joao123',
    email: 'joao@email.com',
    senha: '123456'
  })
});

const data = await response.json();
```

**Com Autenticação:**
```javascript
const token = 'eyJhbGc...';

const response = await fetch('http://localhost:3000/usuarios', {
  headers: {
    'Authorization': `Bearer ${token}`
  }
});
```

#### 📖 Parte 3: Axios (15 min)

**Instalação:**
```bash
npm install axios
```

**Configuração:**
```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: 'http://localhost:3000',
  timeout: 5000,
});

// GET
const response = await api.get('/usuarios');
console.log(response.data);

// POST
const response = await api.post('/usuarios', {
  username: 'joao123',
  email: 'joao@email.com',
  senha: '123456'
});
```

**Interceptors:**
```javascript
// Adicionar token automaticamente
api.interceptors.request.use(config => {
  const token = getToken();
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```

#### 📖 Parte 4: AsyncStorage (15 min)

**Instalação:**
```bash
npm install @react-native-async-storage/async-storage
```

**Uso:**
```javascript
import AsyncStorage from '@react-native-async-storage/async-storage';

// Salvar
await AsyncStorage.setItem('token', 'eyJhbGc...');

// Buscar
const token = await AsyncStorage.getItem('token');

// Remover
await AsyncStorage.removeItem('token');

// Limpar tudo
await AsyncStorage.clear();
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Configurar API Service (20 min)

**Instalar dependências:**
```bash
npm install axios @react-native-async-storage/async-storage
```

**Criar:** `src/services/api.js`

```javascript
import axios from 'axios';
import AsyncStorage from '@react-native-async-storage/async-storage';

const api = axios.create({
  baseURL: 'http://localhost:3000',
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Interceptor para adicionar token
api.interceptors.request.use(
  async (config) => {
    const token = await AsyncStorage.getItem('token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

// Interceptor para tratar erros
api.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      await AsyncStorage.removeItem('token');
    }
    return Promise.reject(error);
  }
);

export default api;
```

#### 💻 Exercício 2: Implementar Login com API (30 min)

**Atualizar:** `src/screens/LoginScreen.js`

```javascript
import { useState } from 'react';
import { View, Text, StyleSheet, Alert, TouchableOpacity, ActivityIndicator } from 'react-native';
import AsyncStorage from '@react-native-async-storage/async-storage';
import Input from '../components/Input';
import Button from '../components/Button';
import api from '../services/api';
import colors from '../styles/colors';

export default function LoginScreen({ navigation }) {
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');
  const [loading, setLoading] = useState(false);

  const handleLogin = async () => {
    if (!email || !senha) {
      Alert.alert('Erro', 'Preencha todos os campos');
      return;
    }

    setLoading(true);

    try {
      const response = await api.post('/auth/login', {
        email,
        senha
      });

      const { token, usuario } = response.data;

      // Salvar token
      await AsyncStorage.setItem('token', token);
      await AsyncStorage.setItem('usuario', JSON.stringify(usuario));

      // Navegar para Home
      navigation.replace('Home');
    } catch (error) {
      console.error(error);
      
      if (error.response?.status === 401) {
        Alert.alert('Erro', 'Email ou senha inválidos');
      } else {
        Alert.alert('Erro', 'Não foi possível fazer login. Tente novamente.');
      }
    } finally {
      setLoading(false);
    }
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
          editable={!loading}
        />
        
        <Input
          placeholder="Senha"
          value={senha}
          onChangeText={setSenha}
          secureTextEntry
          editable={!loading}
        />
        
        {loading ? (
          <ActivityIndicator size="large" color={colors.primary} />
        ) : (
          <Button title="Entrar" onPress={handleLogin} />
        )}

        <TouchableOpacity 
          onPress={() => navigation.navigate('Register')}
          style={styles.link}
          disabled={loading}
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

#### 💻 Exercício 3: Implementar Cadastro com API (20 min)

**Atualizar:** `src/screens/RegisterScreen.js`

```javascript
import { useState } from 'react';
import { View, StyleSheet, Alert, TouchableOpacity, Text, ActivityIndicator } from 'react-native';
import Input from '../components/Input';
import Button from '../components/Button';
import api from '../services/api';
import colors from '../styles/colors';

export default function RegisterScreen({ navigation }) {
  const [username, setUsername] = useState('');
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');
  const [confirmarSenha, setConfirmarSenha] = useState('');
  const [loading, setLoading] = useState(false);

  const handleCadastro = async () => {
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

    setLoading(true);

    try {
      await api.post('/usuarios', {
        username,
        email,
        senha
      });

      Alert.alert('Sucesso', 'Cadastro realizado! Faça login.', [
        { text: 'OK', onPress: () => navigation.goBack() }
      ]);
    } catch (error) {
      console.error(error);
      
      if (error.response?.status === 409) {
        Alert.alert('Erro', 'Email ou username já cadastrado');
      } else if (error.response?.status === 400) {
        Alert.alert('Erro', error.response.data.erro || 'Dados inválidos');
      } else {
        Alert.alert('Erro', 'Não foi possível cadastrar. Tente novamente.');
      }
    } finally {
      setLoading(false);
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.content}>
        <Input
          placeholder="Username"
          value={username}
          onChangeText={setUsername}
          editable={!loading}
        />
        
        <Input
          placeholder="Email"
          value={email}
          onChangeText={setEmail}
          keyboardType="email-address"
          editable={!loading}
        />
        
        <Input
          placeholder="Senha"
          value={senha}
          onChangeText={setSenha}
          secureTextEntry
          editable={!loading}
        />
        
        <Input
          placeholder="Confirmar Senha"
          value={confirmarSenha}
          onChangeText={setConfirmarSenha}
          secureTextEntry
          editable={!loading}
        />
        
        {loading ? (
          <ActivityIndicator size="large" color={colors.primary} />
        ) : (
          <Button title="Cadastrar" onPress={handleCadastro} />
        )}

        <TouchableOpacity 
          onPress={() => navigation.goBack()}
          style={styles.link}
          disabled={loading}
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

#### 💻 Exercício 4: Buscar Categorias da API (20 min)

**Atualizar:** `src/screens/CategoryScreen.js`

```javascript
import { useState, useEffect } from 'react';
import { View, StyleSheet, FlatList, Alert, ActivityIndicator } from 'react-native';
import Header from '../components/Header';
import CategoryCard from '../components/CategoryCard';
import Button from '../components/Button';
import api from '../services/api';
import colors from '../styles/colors';

export default function CategoryScreen({ navigation }) {
  const [selectedId, setSelectedId] = useState(null);
  const [categorias, setCategorias] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    loadCategorias();
  }, []);

  const loadCategorias = async () => {
    try {
      const response = await api.get('/categorias');
      setCategorias(response.data);
    } catch (error) {
      console.error(error);
      Alert.alert('Erro', 'Não foi possível carregar categorias');
    } finally {
      setLoading(false);
    }
  };

  const handleEntrarFila = () => {
    if (!selectedId) {
      Alert.alert('Atenção', 'Selecione uma categoria');
      return;
    }

    const categoria = categorias.find(c => c.id === selectedId);
    navigation.navigate('Chat', {
      categoriaId: categoria.id,
      categoriaNome: categoria.nome,
      categoriaIcon: categoria.icone
    });
  };

  if (loading) {
    return (
      <View style={styles.container}>
        <Header title="Categorias" />
        <View style={styles.loading}>
          <ActivityIndicator size="large" color={colors.primary} />
        </View>
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <Header 
        title="Categorias" 
        subtitle="Escolha um tema para conversar" 
      />
      
      <FlatList
        data={categorias}
        renderItem={({ item }) => (
          <CategoryCard
            icon={item.icone}
            title={item.nome}
            description={item.descricao}
            selected={selectedId === item.id}
            onPress={() => setSelectedId(item.id)}
          />
        )}
        keyExtractor={(item) => item.id.toString()}
      />

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
  loading: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  footer: {
    padding: 20,
    backgroundColor: colors.white,
  },
});
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Implementar Logout (20 min)

**Tarefa:** Adicionar botão de logout no HomeScreen

**Requisitos:**
- Botão "Sair"
- Remover token do AsyncStorage
- Navegar para Login
- Confirmar ação com Alert

**Dica:**
```javascript
const handleLogout = async () => {
  Alert.alert(
    'Sair',
    'Deseja realmente sair?',
    [
      { text: 'Cancelar', style: 'cancel' },
      {
        text: 'Sair',
        onPress: async () => {
          await AsyncStorage.removeItem('token');
          await AsyncStorage.removeItem('usuario');
          navigation.replace('Login');
        }
      }
    ]
  );
};
```

#### 🎯 Desafio 2: Buscar Usuários Online da API (20 min)

**Tarefa:** Atualizar UsersOnlineScreen para buscar dados reais

**Arquivo:** `src/screens/UsersOnlineScreen.js`

**Requisitos:**
- useEffect para carregar ao montar
- GET /usuarios
- Loading state
- Error handling
- Pull-to-refresh

**Estrutura:**
```javascript
const [usuarios, setUsuarios] = useState([]);
const [loading, setLoading] = useState(true);
const [refreshing, setRefreshing] = useState(false);

useEffect(() => {
  loadUsuarios();
}, []);

const loadUsuarios = async () => {
  try {
    const response = await api.get('/usuarios');
    setUsuarios(response.data);
  } catch (error) {
    Alert.alert('Erro', 'Não foi possível carregar usuários');
  } finally {
    setLoading(false);
  }
};

const handleRefresh = async () => {
  setRefreshing(true);
  await loadUsuarios();
  setRefreshing(false);
};
```

#### 🎯 Desafio 3: Atualizar Perfil via API (20 min)

**Tarefa:** Implementar edição de perfil com API

**Arquivo:** `src/screens/ProfileScreen.js`

**Requisitos:**
- Carregar dados do usuário logado
- PUT /usuarios/:id para atualizar
- Validações
- Feedback de sucesso/erro

**Dica:**
```javascript
const handleSalvar = async () => {
  try {
    const usuarioStorage = await AsyncStorage.getItem('usuario');
    const usuario = JSON.parse(usuarioStorage);

    await api.put(`/usuarios/${usuario.id}`, {
      username: nome,
      email: email
    });

    Alert.alert('Sucesso', 'Perfil atualizado!');
    setEditando(false);
  } catch (error) {
    Alert.alert('Erro', 'Não foi possível atualizar perfil');
  }
};
```

**Checklist:**
- [ ] Logout funcionando
- [ ] UsersOnlineScreen com API
- [ ] ProfileScreen com edição
- [ ] Todas as requisições tratando erros

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **Diferença entre fetch e axios?**
   - fetch: nativo / axios: biblioteca com mais recursos

2. **Para que serve AsyncStorage?**
   - Armazenar dados localmente (token, preferências)

3. **Como enviar token em requisições?**
   - Header Authorization: Bearer {token}

4. **O que fazer quando API retorna 401?**
   - Remover token e redirecionar para login

#### 🎯 Fluxo de Autenticação

```
1. Login → POST /auth/login
2. Recebe token
3. Salva no AsyncStorage
4. Requisições usam token
5. Logout → Remove token
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Fazer requisições HTTP
- [ ] Usar axios
- [ ] Configurar interceptors
- [ ] Salvar/buscar token
- [ ] Tratar erros de API
- [ ] Implementar login/logout
- [ ] Consumir endpoints REST

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar loading em todas as telas
   - Implementar retry em caso de erro
   - Adicionar timeout nas requisições

2. **Estudo:**
   - Ler sobre useEffect
   - Explorar outros métodos do axios

---

## 📊 Avaliação

### Critérios (Peso: 20% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Configuração API** | 25% | api.js configurado corretamente |
| **Autenticação** | 30% | Login/logout funcionando |
| **Requisições** | 25% | GET/POST/PUT implementados |
| **Tratamento de Erros** | 20% | Erros tratados adequadamente |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Garantir backend rodando
- [ ] Testar endpoints com Thunder Client
- [ ] Preparar dados de teste no banco
- [ ] Verificar CORS configurado

### Pontos de Atenção
- ⚠️ Problemas de CORS
- ⚠️ Backend não rodando
- ⚠️ URL incorreta (localhost vs IP)
- ⚠️ Token não sendo enviado

### Troubleshooting

**Problema:** "Network request failed"
**Solução:** Verificar se backend está rodando e URL está correta

**Problema:** "CORS error"
**Solução:** Configurar CORS no backend

**Problema:** "401 Unauthorized"
**Solução:** Verificar se token está sendo enviado

---

## 📎 Recursos Adicionais

- [Axios Docs](https://axios-http.com/)
- [AsyncStorage](https://react-native-async-storage.github.io/async-storage/)

### Próxima Aula
**Aula 07 - Testes e Qualidade**
- Testes unitários
- Testes de integração
- Debugging
- Performance

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
