# Aula 07 - CRUD Completo no Frontend

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Implementação completa de CRUD integrado frontend-backend

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Implementar CRUD completo (Create, Read, Update, Delete)
- ✅ Integrar todas as operações com backend
- ✅ Validar dados antes de enviar para API
- ✅ Atualizar interface após operações
- ✅ Implementar confirmações de ações destrutivas
- ✅ Gerenciar estados de loading/success/error
- ✅ Testar fluxo completo da aplicação

---

## 📚 Conteúdo Programático

### 1. CRUD Completo
- CREATE: Cadastro de dados
- READ: Listagem e detalhes
- UPDATE: Edição de dados
- DELETE: Remoção de dados

### 2. Validações
- Validação no frontend
- Validação no backend
- Feedback ao usuário

### 3. Estados da UI
- Loading (carregando)
- Success (sucesso)
- Error (erro)
- Empty (vazio)

### 4. Boas Práticas
- Confirmação antes de deletar
- Feedback visual
- Atualização otimista
- Tratamento de erros

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Integração com API REST
- Axios e interceptors
- AsyncStorage
- Login/Logout

**Atividade de Aquecimento:**
```
Discussão:
- O que acontece quando você deleta um post no Instagram?
- Como o app confirma que você quer deletar?
- Por que pedir confirmação?

Objetivo: Preparar para operações CRUD completas
```

**Checkpoint:**
- Verificar backend rodando
- Testar login funcionando
- Revisar endpoints disponíveis

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: CRUD - Visão Geral (15 min)

**Operações CRUD:**

| Operação | Método HTTP | Endpoint | Ação |
|----------|-------------|----------|------|
| **Create** | POST | /usuarios | Criar novo usuário |
| **Read** | GET | /usuarios | Listar todos |
| **Read** | GET | /usuarios/:id | Buscar um |
| **Update** | PUT | /usuarios/:id | Atualizar |
| **Delete** | DELETE | /usuarios/:id | Remover |

**Fluxo Completo:**

```
1. CREATE
   Usuário preenche formulário
   → Validação frontend
   → POST /usuarios
   → Validação backend
   → Salva no banco
   → Retorna sucesso
   → Atualiza lista

2. READ
   Tela carrega
   → GET /usuarios
   → Busca no banco
   → Retorna lista
   → Exibe na tela

3. UPDATE
   Usuário edita dados
   → Validação frontend
   → PUT /usuarios/:id
   → Validação backend
   → Atualiza no banco
   → Retorna sucesso
   → Atualiza tela

4. DELETE
   Usuário clica deletar
   → Confirmação
   → DELETE /usuarios/:id
   → Remove do banco
   → Retorna sucesso
   → Remove da lista
```

#### 📖 Parte 2: Estados da UI (15 min)

**Estados Possíveis:**

```javascript
const [loading, setLoading] = useState(false);
const [error, setError] = useState(null);
const [success, setSuccess] = useState(false);
const [data, setData] = useState([]);

// Loading
if (loading) return <ActivityIndicator />;

// Error
if (error) return <Text>Erro: {error}</Text>;

// Empty
if (data.length === 0) return <Text>Nenhum dado</Text>;

// Success
return <FlatList data={data} />;
```

**Feedback Visual:**

```javascript
// Sucesso
Alert.alert('Sucesso', 'Usuário criado!');

// Erro
Alert.alert('Erro', 'Não foi possível criar usuário');

// Confirmação
Alert.alert(
  'Confirmar',
  'Deseja realmente deletar?',
  [
    { text: 'Cancelar', style: 'cancel' },
    { text: 'Deletar', onPress: handleDelete, style: 'destructive' }
  ]
);
```

#### 📖 Parte 3: Validações (15 min)

**Validação Frontend:**

```javascript
const validarUsuario = (dados) => {
  if (!dados.username || dados.username.length < 3) {
    return 'Username deve ter no mínimo 3 caracteres';
  }
  
  if (!dados.email || !dados.email.includes('@')) {
    return 'Email inválido';
  }
  
  if (!dados.senha || dados.senha.length < 6) {
    return 'Senha deve ter no mínimo 6 caracteres';
  }
  
  return null;
};

// Uso
const erro = validarUsuario({ username, email, senha });
if (erro) {
  Alert.alert('Erro', erro);
  return;
}
```

**Validação Backend:**
- Backend já valida (Part 03)
- Frontend trata erros retornados
- Exibe mensagens específicas

#### 📖 Parte 4: Atualização da Lista (15 min)

**Após CREATE:**

```javascript
const handleCreate = async (dados) => {
  const response = await api.post('/usuarios', dados);
  const novoUsuario = response.data;
  
  // Adicionar na lista
  setUsuarios([...usuarios, novoUsuario]);
};
```

**Após UPDATE:**

```javascript
const handleUpdate = async (id, dados) => {
  const response = await api.put(`/usuarios/${id}`, dados);
  const usuarioAtualizado = response.data;
  
  // Atualizar na lista
  setUsuarios(usuarios.map(u => 
    u.id === id ? usuarioAtualizado : u
  ));
};
```

**Após DELETE:**

```javascript
const handleDelete = async (id) => {
  await api.delete(`/usuarios/${id}`);
  
  // Remover da lista
  setUsuarios(usuarios.filter(u => u.id !== id));
};
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Tela de Gerenciamento de Usuários (30 min)

**Criar:** `src/screens/ManageUsersScreen.js`

```javascript
import { useState, useEffect } from 'react';
import { View, Text, StyleSheet, FlatList, TouchableOpacity, Alert, ActivityIndicator } from 'react-native';
import Header from '../components/Header';
import Button from '../components/Button';
import api from '../services/api';
import colors from '../styles/colors';

export default function ManageUsersScreen({ navigation }) {
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

  const handleDelete = (usuario) => {
    Alert.alert(
      'Confirmar Exclusão',
      `Deseja realmente excluir ${usuario.username}?`,
      [
        { text: 'Cancelar', style: 'cancel' },
        {
          text: 'Excluir',
          style: 'destructive',
          onPress: async () => {
            try {
              await api.delete(`/usuarios/${usuario.id}`);
              setUsuarios(usuarios.filter(u => u.id !== usuario.id));
              Alert.alert('Sucesso', 'Usuário excluído');
            } catch (error) {
              if (error.response?.status === 400) {
                Alert.alert('Erro', error.response.data.erro);
              } else {
                Alert.alert('Erro', 'Não foi possível excluir usuário');
              }
            }
          }
        }
      ]
    );
  };

  const renderUsuario = ({ item }) => (
    <View style={styles.userCard}>
      <View style={styles.userInfo}>
        <Text style={styles.userName}>{item.username}</Text>
        <Text style={styles.userEmail}>{item.email}</Text>
      </View>
      
      <View style={styles.actions}>
        <TouchableOpacity
          style={styles.editButton}
          onPress={() => navigation.navigate('EditUser', { usuario: item })}
        >
          <Text style={styles.editButtonText}>✏️</Text>
        </TouchableOpacity>
        
        <TouchableOpacity
          style={styles.deleteButton}
          onPress={() => handleDelete(item)}
        >
          <Text style={styles.deleteButtonText}>🗑️</Text>
        </TouchableOpacity>
      </View>
    </View>
  );

  if (loading) {
    return (
      <View style={styles.container}>
        <Header title="Gerenciar Usuários" />
        <View style={styles.loading}>
          <ActivityIndicator size="large" color={colors.primary} />
        </View>
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <Header title="Gerenciar Usuários" />
      
      <FlatList
        data={usuarios}
        renderItem={renderUsuario}
        keyExtractor={(item) => item.id.toString()}
        refreshing={refreshing}
        onRefresh={handleRefresh}
        ListEmptyComponent={() => (
          <Text style={styles.empty}>Nenhum usuário cadastrado</Text>
        )}
      />

      <View style={styles.footer}>
        <Button
          title="Adicionar Usuário"
          onPress={() => navigation.navigate('AddUser')}
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
  userCard: {
    flexDirection: 'row',
    backgroundColor: colors.white,
    padding: 15,
    marginHorizontal: 15,
    marginVertical: 5,
    borderRadius: 10,
    alignItems: 'center',
  },
  userInfo: {
    flex: 1,
  },
  userName: {
    fontSize: 16,
    fontWeight: 'bold',
    color: colors.black,
  },
  userEmail: {
    fontSize: 14,
    color: colors.gray,
    marginTop: 3,
  },
  actions: {
    flexDirection: 'row',
    gap: 10,
  },
  editButton: {
    padding: 8,
  },
  editButtonText: {
    fontSize: 20,
  },
  deleteButton: {
    padding: 8,
  },
  deleteButtonText: {
    fontSize: 20,
  },
  empty: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 16,
    color: colors.gray,
  },
  footer: {
    padding: 20,
    backgroundColor: colors.white,
  },
});
```

#### 💻 Exercício 2: Tela de Adicionar Usuário (30 min)

**Criar:** `src/screens/AddUserScreen.js`

```javascript
import { useState } from 'react';
import { View, StyleSheet, Alert, ActivityIndicator, ScrollView } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import Button from '../components/Button';
import api from '../services/api';
import colors from '../styles/colors';

export default function AddUserScreen({ navigation }) {
  const [username, setUsername] = useState('');
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');
  const [loading, setLoading] = useState(false);

  const validar = () => {
    if (!username || username.length < 3) {
      Alert.alert('Erro', 'Username deve ter no mínimo 3 caracteres');
      return false;
    }

    if (!email || !email.includes('@')) {
      Alert.alert('Erro', 'Email inválido');
      return false;
    }

    if (!senha || senha.length < 6) {
      Alert.alert('Erro', 'Senha deve ter no mínimo 6 caracteres');
      return false;
    }

    return true;
  };

  const handleSalvar = async () => {
    if (!validar()) return;

    setLoading(true);

    try {
      await api.post('/usuarios', {
        username,
        email,
        senha
      });

      Alert.alert('Sucesso', 'Usuário criado com sucesso!', [
        { text: 'OK', onPress: () => navigation.goBack() }
      ]);
    } catch (error) {
      if (error.response?.status === 409) {
        Alert.alert('Erro', 'Email ou username já cadastrado');
      } else if (error.response?.status === 400) {
        Alert.alert('Erro', error.response.data.erro);
      } else {
        Alert.alert('Erro', 'Não foi possível criar usuário');
      }
    } finally {
      setLoading(false);
    }
  };

  return (
    <View style={styles.container}>
      <Header title="Adicionar Usuário" />
      
      <ScrollView style={styles.content}>
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

        {loading ? (
          <ActivityIndicator size="large" color={colors.primary} style={styles.loading} />
        ) : (
          <Button title="Salvar" onPress={handleSalvar} />
        )}
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
    padding: 20,
  },
  loading: {
    marginTop: 20,
  },
});
```

#### 💻 Exercício 3: Tela de Editar Usuário (30 min)

**Criar:** `src/screens/EditUserScreen.js`

```javascript
import { useState } from 'react';
import { View, StyleSheet, Alert, ActivityIndicator, ScrollView } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import Button from '../components/Button';
import api from '../services/api';
import colors from '../styles/colors';

export default function EditUserScreen({ route, navigation }) {
  const { usuario } = route.params;
  
  const [username, setUsername] = useState(usuario.username);
  const [email, setEmail] = useState(usuario.email);
  const [senha, setSenha] = useState('');
  const [loading, setLoading] = useState(false);

  const validar = () => {
    if (!username || username.length < 3) {
      Alert.alert('Erro', 'Username deve ter no mínimo 3 caracteres');
      return false;
    }

    if (!email || !email.includes('@')) {
      Alert.alert('Erro', 'Email inválido');
      return false;
    }

    if (senha && senha.length < 6) {
      Alert.alert('Erro', 'Senha deve ter no mínimo 6 caracteres');
      return false;
    }

    return true;
  };

  const handleSalvar = async () => {
    if (!validar()) return;

    setLoading(true);

    try {
      const dados = { username, email };
      if (senha) {
        dados.senha = senha;
      }

      await api.put(`/usuarios/${usuario.id}`, dados);

      Alert.alert('Sucesso', 'Usuário atualizado com sucesso!', [
        { text: 'OK', onPress: () => navigation.goBack() }
      ]);
    } catch (error) {
      if (error.response?.status === 409) {
        Alert.alert('Erro', 'Email ou username já cadastrado');
      } else if (error.response?.status === 404) {
        Alert.alert('Erro', 'Usuário não encontrado');
      } else if (error.response?.status === 400) {
        Alert.alert('Erro', error.response.data.erro);
      } else {
        Alert.alert('Erro', 'Não foi possível atualizar usuário');
      }
    } finally {
      setLoading(false);
    }
  };

  return (
    <View style={styles.container}>
      <Header title="Editar Usuário" />
      
      <ScrollView style={styles.content}>
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
          placeholder="Nova Senha (deixe vazio para não alterar)"
          value={senha}
          onChangeText={setSenha}
          secureTextEntry
          editable={!loading}
        />

        {loading ? (
          <ActivityIndicator size="large" color={colors.primary} style={styles.loading} />
        ) : (
          <Button title="Salvar Alterações" onPress={handleSalvar} />
        )}
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
    padding: 20,
  },
  loading: {
    marginTop: 20,
  },
});
```

**Adicionar ao Stack Navigator:**

```javascript
// App.js
import ManageUsersScreen from './src/screens/ManageUsersScreen';
import AddUserScreen from './src/screens/AddUserScreen';
import EditUserScreen from './src/screens/EditUserScreen';

<Stack.Screen name="ManageUsers" component={ManageUsersScreen} />
<Stack.Screen name="AddUser" component={AddUserScreen} />
<Stack.Screen name="EditUser" component={EditUserScreen} />
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: CRUD de Categorias (40 min)

**Tarefa:** Implementar CRUD completo de categorias

**Telas a criar:**
- ManageCategoriesScreen (listar + deletar)
- AddCategoryScreen (criar)
- EditCategoryScreen (editar)

**Requisitos:**
- Listar categorias
- Adicionar nova categoria (nome, descrição, ícone)
- Editar categoria existente
- Deletar categoria (com confirmação)
- Validações (nome obrigatório)
- Loading states
- Error handling

**Estrutura ManageCategoriesScreen:**

```javascript
const [categorias, setCategorias] = useState([]);
const [loading, setLoading] = useState(true);

const loadCategorias = async () => {
  const response = await api.get('/categorias');
  setCategorias(response.data);
};

const handleDelete = async (id) => {
  Alert.alert('Confirmar', 'Deseja deletar esta categoria?', [
    { text: 'Cancelar', style: 'cancel' },
    {
      text: 'Deletar',
      onPress: async () => {
        await api.delete(`/categorias/${id}`);
        setCategorias(categorias.filter(c => c.id !== id));
      }
    }
  ]);
};
```

#### 🎯 Desafio 2: Testes Funcionais (20 min)

**Tarefa:** Testar fluxo completo do CRUD

**Checklist de Testes:**

**CREATE:**
- [ ] Criar usuário com dados válidos
- [ ] Tentar criar com username duplicado
- [ ] Tentar criar com email duplicado
- [ ] Tentar criar com senha curta
- [ ] Verificar se aparece na lista

**READ:**
- [ ] Listar todos os usuários
- [ ] Buscar usuário específico
- [ ] Verificar dados corretos
- [ ] Testar pull-to-refresh

**UPDATE:**
- [ ] Editar username
- [ ] Editar email
- [ ] Alterar senha
- [ ] Tentar email duplicado
- [ ] Verificar atualização na lista

**DELETE:**
- [ ] Deletar usuário sem dependências
- [ ] Tentar deletar com salas ativas (deve falhar)
- [ ] Verificar remoção da lista
- [ ] Confirmar remoção no backend

**Documentar resultados:**
```
Teste: Criar usuário com dados válidos
Resultado: ✅ Passou
Observações: Usuário criado e apareceu na lista

Teste: Deletar usuário com salas ativas
Resultado: ✅ Passou
Observações: Erro 400 retornado corretamente
```

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **O que é CRUD?**
   - Create, Read, Update, Delete

2. **Por que confirmar antes de deletar?**
   - Evitar exclusões acidentais

3. **Como atualizar lista após CREATE?**
   - Adicionar novo item ao array: [...lista, novo]

4. **Como atualizar lista após DELETE?**
   - Filtrar item removido: lista.filter(i => i.id !== id)

#### 🎯 Fluxo CRUD Completo

```
CREATE → POST → Adiciona na lista
READ   → GET  → Exibe lista
UPDATE → PUT  → Atualiza item na lista
DELETE → DELETE → Remove item da lista
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Implementar CREATE com validações
- [ ] Implementar READ com loading
- [ ] Implementar UPDATE com feedback
- [ ] Implementar DELETE com confirmação
- [ ] Atualizar lista após operações
- [ ] Tratar todos os erros
- [ ] Testar fluxo completo

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar busca em ManageUsersScreen
   - Implementar ordenação (A-Z, Z-A)
   - Adicionar paginação

2. **Testes:**
   - Testar todos os cenários de erro
   - Documentar bugs encontrados

---

## 📊 Avaliação

### Critérios (Peso: 20% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **CREATE** | 25% | Criação funcionando com validações |
| **READ** | 20% | Listagem com loading/empty |
| **UPDATE** | 25% | Edição funcionando corretamente |
| **DELETE** | 20% | Exclusão com confirmação |
| **Testes** | 10% | Fluxo completo testado |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Garantir backend com dados de teste
- [ ] Preparar cenários de erro
- [ ] Testar CRUD completo
- [ ] Ter checklist de testes pronto

### Pontos de Atenção
- ⚠️ Alunos esquecem de atualizar lista
- ⚠️ Não tratam erros específicos
- ⚠️ Esquecem confirmação no DELETE
- ⚠️ Não testam cenários de erro

### Troubleshooting

**Problema:** "Lista não atualiza após CREATE"
**Solução:** Verificar se está adicionando ao array corretamente

**Problema:** "DELETE não remove da lista"
**Solução:** Verificar filter e setState

---

## 📎 Recursos Adicionais

- [React State Management](https://react.dev/learn/managing-state)
- [Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

### Próxima Aula
**Aula 08 - Finalização e Testes**
- Testes de integração
- Correção de bugs
- Polimento da UI
- Preparação para apresentação

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
