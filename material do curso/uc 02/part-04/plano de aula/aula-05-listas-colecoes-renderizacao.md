# Aula 05 - Listas, Coleções e Renderização de Dados

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Renderização eficiente de listas e manipulação de coleções

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Renderizar listas com map() e FlatList
- ✅ Diferenciar ScrollView de FlatList
- ✅ Implementar renderização condicional
- ✅ Trabalhar com coleções de dados
- ✅ Otimizar performance de listas grandes
- ✅ Criar componentes de lista reutilizáveis
- ✅ Implementar pull-to-refresh e infinite scroll

---

## 📚 Conteúdo Programático

### 1. Renderização de Listas
- map() para arrays pequenos
- FlatList para listas grandes
- key prop (importância)
- Performance

### 2. FlatList
- renderItem
- keyExtractor
- ItemSeparatorComponent
- ListEmptyComponent
- ListHeaderComponent / ListFooterComponent

### 3. Renderização Condicional
- Operador ternário
- Operador &&
- Função auxiliar
- Estados de loading/empty/error

### 4. Manipulação de Dados
- Filter, map, sort
- Busca em listas
- Paginação

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Navegação entre telas
- Stack Navigator
- Passagem de parâmetros

**Atividade de Aquecimento:**
```
Discussão:
- Como apps como Instagram exibem feed de posts?
- Por que alguns apps "travam" com muitos itens?
- Como exibir mensagem quando lista está vazia?

Objetivo: Preparar para renderização eficiente
```

**Checkpoint:**
- Revisar map() básico usado anteriormente
- Demonstrar problema de performance com ScrollView

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: map() vs FlatList (15 min)

**map() - Arrays Pequenos:**

```jsx
const categorias = ['Filmes', 'Jogos', 'Séries'];

// Renderizar com map
<ScrollView>
  {categorias.map((cat, index) => (
    <Text key={index}>{cat}</Text>
  ))}
</ScrollView>
```

**Problemas do map():**
- ❌ Renderiza todos os itens de uma vez
- ❌ Não otimiza memória
- ❌ Lento com muitos itens (>100)

**FlatList - Arrays Grandes:**

```jsx
const categorias = ['Filmes', 'Jogos', 'Séries'];

<FlatList
  data={categorias}
  renderItem={({ item }) => <Text>{item}</Text>}
  keyExtractor={(item, index) => index.toString()}
/>
```

**Vantagens do FlatList:**
- ✅ Renderiza apenas itens visíveis (virtualização)
- ✅ Otimiza memória
- ✅ Rápido com milhares de itens
- ✅ Pull-to-refresh integrado
- ✅ Infinite scroll

**Quando usar cada um:**

| Cenário | Usar |
|---------|------|
| < 20 itens simples | map() + ScrollView |
| > 20 itens | FlatList |
| Lista dinâmica (cresce) | FlatList |
| Performance crítica | FlatList |

#### 📖 Parte 2: FlatList em Profundidade (20 min)

**Anatomia do FlatList:**

```jsx
<FlatList
  // Dados
  data={usuarios}
  
  // Como renderizar cada item
  renderItem={({ item, index }) => (
    <Text>{item.nome}</Text>
  )}
  
  // Chave única para cada item
  keyExtractor={(item) => item.id.toString()}
  
  // Separador entre itens
  ItemSeparatorComponent={() => <View style={{ height: 1, backgroundColor: '#ddd' }} />}
  
  // Quando lista está vazia
  ListEmptyComponent={() => <Text>Nenhum usuário encontrado</Text>}
  
  // Header da lista
  ListHeaderComponent={() => <Text>Usuários Online</Text>}
  
  // Footer da lista
  ListFooterComponent={() => <Text>Fim da lista</Text>}
  
  // Pull to refresh
  refreshing={loading}
  onRefresh={handleRefresh}
  
  // Infinite scroll
  onEndReached={loadMore}
  onEndReachedThreshold={0.5}
/>
```

**renderItem - Objeto Completo:**

```jsx
renderItem={({ item, index, separators }) => {
  // item: objeto do array
  // index: posição no array
  // separators: controle de separadores
  
  return (
    <View>
      <Text>{index + 1}. {item.nome}</Text>
    </View>
  );
}}
```

**keyExtractor - Importância:**

```jsx
// ❌ Usar index (pode causar bugs)
keyExtractor={(item, index) => index.toString()}

// ✅ Usar ID único
keyExtractor={(item) => item.id.toString()}

// ✅ Combinar campos se não tiver ID
keyExtractor={(item) => `${item.nome}-${item.email}`}
```

#### 📖 Parte 3: Renderização Condicional (15 min)

**Operador Ternário:**

```jsx
{isLoggedIn ? (
  <Text>Bem-vindo!</Text>
) : (
  <Text>Faça login</Text>
)}
```

**Operador && (E Lógico):**

```jsx
{isLoggedIn && <Text>Você está logado</Text>}

{usuarios.length === 0 && <Text>Nenhum usuário</Text>}
```

**Estados de UI:**

```jsx
function UserList() {
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [usuarios, setUsuarios] = useState([]);

  if (loading) {
    return <Text>Carregando...</Text>;
  }

  if (error) {
    return <Text>Erro: {error}</Text>;
  }

  if (usuarios.length === 0) {
    return <Text>Nenhum usuário encontrado</Text>;
  }

  return (
    <FlatList
      data={usuarios}
      renderItem={({ item }) => <Text>{item.nome}</Text>}
    />
  );
}
```

#### 📖 Parte 4: Manipulação de Arrays (10 min)

**Filter (Filtrar):**

```jsx
const [busca, setBusca] = useState('');
const [usuarios, setUsuarios] = useState([...]);

const usuariosFiltrados = usuarios.filter(u => 
  u.nome.toLowerCase().includes(busca.toLowerCase())
);

<FlatList data={usuariosFiltrados} ... />
```

**Sort (Ordenar):**

```jsx
const usuariosOrdenados = [...usuarios].sort((a, b) => 
  a.nome.localeCompare(b.nome)
);
```

**Map (Transformar):**

```jsx
const nomes = usuarios.map(u => u.nome);
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Lista de Usuários Online (30 min)

**Criar:** `src/screens/UsersOnlineScreen.js`

```jsx
import { useState } from 'react';
import { View, Text, StyleSheet, FlatList } from 'react-native';
import Header from '../components/Header';
import colors from '../styles/colors';

export default function UsersOnlineScreen() {
  const [usuarios] = useState([
    { id: 1, nome: 'João Silva', categoria: 'Filmes', online: true },
    { id: 2, nome: 'Maria Santos', categoria: 'Jogos', online: true },
    { id: 3, nome: 'Pedro Costa', categoria: 'Séries', online: false },
    { id: 4, nome: 'Ana Lima', categoria: 'Filmes', online: true },
    { id: 5, nome: 'Carlos Souza', categoria: 'Música', online: true },
  ]);

  const renderUsuario = ({ item }) => (
    <View style={styles.userCard}>
      <View style={styles.avatar}>
        <Text style={styles.avatarText}>
          {item.nome.charAt(0)}
        </Text>
      </View>
      
      <View style={styles.userInfo}>
        <Text style={styles.userName}>{item.nome}</Text>
        <Text style={styles.userCategory}>{item.categoria}</Text>
      </View>
      
      <View style={[
        styles.status,
        item.online && styles.statusOnline
      ]}>
        <Text style={styles.statusText}>
          {item.online ? '● Online' : '○ Offline'}
        </Text>
      </View>
    </View>
  );

  return (
    <View style={styles.container}>
      <Header title="Usuários Online" />
      
      <FlatList
        data={usuarios}
        renderItem={renderUsuario}
        keyExtractor={(item) => item.id.toString()}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
        ListEmptyComponent={() => (
          <Text style={styles.empty}>Nenhum usuário online</Text>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  userCard: {
    flexDirection: 'row',
    alignItems: 'center',
    backgroundColor: colors.white,
    padding: 15,
  },
  avatar: {
    width: 50,
    height: 50,
    borderRadius: 25,
    backgroundColor: colors.primary,
    justifyContent: 'center',
    alignItems: 'center',
  },
  avatarText: {
    color: colors.white,
    fontSize: 20,
    fontWeight: 'bold',
  },
  userInfo: {
    flex: 1,
    marginLeft: 15,
  },
  userName: {
    fontSize: 16,
    fontWeight: 'bold',
    color: colors.black,
  },
  userCategory: {
    fontSize: 14,
    color: colors.gray,
    marginTop: 3,
  },
  status: {
    paddingHorizontal: 10,
    paddingVertical: 5,
    borderRadius: 10,
    backgroundColor: '#f0f0f0',
  },
  statusOnline: {
    backgroundColor: '#E8F5E9',
  },
  statusText: {
    fontSize: 12,
    color: colors.gray,
  },
  separator: {
    height: 1,
    backgroundColor: '#f0f0f0',
  },
  empty: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 16,
    color: colors.gray,
  },
});
```

**Adicionar ao Stack Navigator:**

```jsx
// App.js
import UsersOnlineScreen from './src/screens/UsersOnlineScreen';

<Stack.Screen 
  name="UsersOnline" 
  component={UsersOnlineScreen}
  options={{ title: 'Usuários Online' }}
/>
```

#### 💻 Exercício 2: Lista com Busca (30 min)

**Criar:** `src/screens/SearchUsersScreen.js`

```jsx
import { useState } from 'react';
import { View, StyleSheet, FlatList } from 'react-native';
import Header from '../components/Header';
import Input from '../components/Input';
import colors from '../styles/colors';

export default function SearchUsersScreen() {
  const [busca, setBusca] = useState('');
  const [usuarios] = useState([
    { id: 1, nome: 'João Silva', categoria: 'Filmes' },
    { id: 2, nome: 'Maria Santos', categoria: 'Jogos' },
    { id: 3, nome: 'Pedro Costa', categoria: 'Séries' },
    { id: 4, nome: 'Ana Lima', categoria: 'Filmes' },
    { id: 5, nome: 'Carlos Souza', categoria: 'Música' },
    { id: 6, nome: 'Julia Oliveira', categoria: 'Jogos' },
    { id: 7, nome: 'Lucas Pereira', categoria: 'Filmes' },
  ]);

  const usuariosFiltrados = usuarios.filter(u =>
    u.nome.toLowerCase().includes(busca.toLowerCase()) ||
    u.categoria.toLowerCase().includes(busca.toLowerCase())
  );

  const renderUsuario = ({ item }) => (
    <View style={styles.userCard}>
      <Text style={styles.userName}>{item.nome}</Text>
      <Text style={styles.userCategory}>{item.categoria}</Text>
    </View>
  );

  return (
    <View style={styles.container}>
      <Header title="Buscar Usuários" />
      
      <View style={styles.searchContainer}>
        <Input
          placeholder="Buscar por nome ou categoria..."
          value={busca}
          onChangeText={setBusca}
        />
      </View>

      <FlatList
        data={usuariosFiltrados}
        renderItem={renderUsuario}
        keyExtractor={(item) => item.id.toString()}
        ListEmptyComponent={() => (
          <Text style={styles.empty}>
            Nenhum usuário encontrado para "{busca}"
          </Text>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  searchContainer: {
    padding: 15,
    backgroundColor: colors.white,
  },
  userCard: {
    backgroundColor: colors.white,
    padding: 15,
    marginHorizontal: 15,
    marginVertical: 5,
    borderRadius: 10,
  },
  userName: {
    fontSize: 16,
    fontWeight: 'bold',
    color: colors.black,
  },
  userCategory: {
    fontSize: 14,
    color: colors.gray,
    marginTop: 3,
  },
  empty: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 16,
    color: colors.gray,
    paddingHorizontal: 20,
  },
});
```

#### 💻 Exercício 3: Lista de Mensagens do Chat (30 min)

**Atualizar:** `src/screens/ChatScreen.js`

```jsx
import { useState } from 'react';
import { View, Text, StyleSheet, FlatList, TextInput, TouchableOpacity } from 'react-native';
import colors from '../styles/colors';

export default function ChatScreen({ route }) {
  const { categoriaNome, categoriaIcon } = route.params;
  
  const [mensagens, setMensagens] = useState([
    { id: 1, texto: 'Olá!', autor: 'outro', timestamp: '10:30' },
    { id: 2, texto: 'Oi! Tudo bem?', autor: 'eu', timestamp: '10:31' },
    { id: 3, texto: 'Você gosta de que tipo de filme?', autor: 'outro', timestamp: '10:32' },
    { id: 4, texto: 'Gosto de ficção científica!', autor: 'eu', timestamp: '10:33' },
  ]);
  
  const [novaMensagem, setNovaMensagem] = useState('');

  const enviarMensagem = () => {
    if (!novaMensagem.trim()) return;

    const mensagem = {
      id: mensagens.length + 1,
      texto: novaMensagem,
      autor: 'eu',
      timestamp: new Date().toLocaleTimeString('pt-BR', { 
        hour: '2-digit', 
        minute: '2-digit' 
      })
    };

    setMensagens([...mensagens, mensagem]);
    setNovaMensagem('');
  };

  const renderMensagem = ({ item }) => (
    <View style={[
      styles.message,
      item.autor === 'eu' && styles.messageMe
    ]}>
      <Text style={[
        styles.messageText,
        item.autor === 'eu' && styles.messageTextMe
      ]}>
        {item.texto}
      </Text>
      <Text style={[
        styles.timestamp,
        item.autor === 'eu' && styles.timestampMe
      ]}>
        {item.timestamp}
      </Text>
    </View>
  );

  return (
    <View style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.icon}>{categoriaIcon}</Text>
        <Text style={styles.categoria}>{categoriaNome}</Text>
        <Text style={styles.status}>● Online</Text>
      </View>

      <FlatList
        data={mensagens}
        renderItem={renderMensagem}
        keyExtractor={(item) => item.id.toString()}
        contentContainerStyle={styles.messagesList}
        inverted={false}
      />

      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Digite uma mensagem..."
          value={novaMensagem}
          onChangeText={setNovaMensagem}
          onSubmitEditing={enviarMensagem}
        />
        <TouchableOpacity 
          style={styles.sendButton}
          onPress={enviarMensagem}
        >
          <Text style={styles.sendButtonText}>Enviar</Text>
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
  messagesList: {
    padding: 15,
  },
  message: {
    backgroundColor: colors.white,
    padding: 12,
    borderRadius: 15,
    marginBottom: 10,
    maxWidth: '75%',
    alignSelf: 'flex-start',
  },
  messageMe: {
    backgroundColor: colors.primary,
    alignSelf: 'flex-end',
  },
  messageText: {
    fontSize: 16,
    color: colors.black,
  },
  messageTextMe: {
    color: colors.white,
  },
  timestamp: {
    fontSize: 10,
    color: colors.gray,
    marginTop: 5,
  },
  timestampMe: {
    color: '#E0E0FF',
  },
  inputContainer: {
    flexDirection: 'row',
    padding: 10,
    backgroundColor: colors.white,
    borderTopWidth: 1,
    borderTopColor: '#ddd',
    gap: 10,
  },
  input: {
    flex: 1,
    backgroundColor: colors.background,
    borderRadius: 20,
    paddingHorizontal: 15,
    paddingVertical: 10,
    fontSize: 16,
  },
  sendButton: {
    backgroundColor: colors.primary,
    borderRadius: 20,
    paddingHorizontal: 20,
    justifyContent: 'center',
  },
  sendButtonText: {
    color: colors.white,
    fontWeight: 'bold',
  },
});
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Lista de Histórico de Conversas (30 min)

**Tarefa:** Criar tela com histórico de conversas

**Arquivo:** `src/screens/HistoryScreen.js`

**Requisitos:**
- FlatList com conversas anteriores
- Cada item mostra: categoria, data, duração
- Ordenar por data (mais recente primeiro)
- ListEmptyComponent quando não houver histórico
- Ao clicar, navegar para detalhes

**Estrutura:**

```jsx
import { useState } from 'react';
import { View, Text, StyleSheet, FlatList, TouchableOpacity } from 'react-native';
import Header from '../components/Header';
import colors from '../styles/colors';

export default function HistoryScreen({ navigation }) {
  const [conversas] = useState([
    { 
      id: 1, 
      categoria: 'Filmes', 
      icon: '🎬',
      data: '2024-01-15', 
      duracao: '15 min',
      mensagens: 42
    },
    { 
      id: 2, 
      categoria: 'Jogos', 
      icon: '🎮',
      data: '2024-01-14', 
      duracao: '23 min',
      mensagens: 67
    },
    { 
      id: 3, 
      categoria: 'Séries', 
      icon: '📺',
      data: '2024-01-13', 
      duracao: '10 min',
      mensagens: 28
    },
  ]);

  const renderConversa = ({ item }) => (
    <TouchableOpacity 
      style={styles.card}
      onPress={() => {/* navegar para detalhes */}}
    >
      <Text style={styles.icon}>{item.icon}</Text>
      <View style={styles.info}>
        <Text style={styles.categoria}>{item.categoria}</Text>
        <Text style={styles.details}>
          {item.data} • {item.duracao} • {item.mensagens} mensagens
        </Text>
      </View>
    </TouchableOpacity>
  );

  return (
    <View style={styles.container}>
      <Header title="Histórico" subtitle="Suas conversas anteriores" />
      
      <FlatList
        data={conversas}
        renderItem={renderConversa}
        keyExtractor={(item) => item.id.toString()}
        ListEmptyComponent={() => (
          <Text style={styles.empty}>Nenhuma conversa ainda</Text>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  card: {
    flexDirection: 'row',
    backgroundColor: colors.white,
    padding: 15,
    marginHorizontal: 15,
    marginVertical: 5,
    borderRadius: 10,
    alignItems: 'center',
  },
  icon: {
    fontSize: 40,
    marginRight: 15,
  },
  info: {
    flex: 1,
  },
  categoria: {
    fontSize: 18,
    fontWeight: 'bold',
    color: colors.black,
  },
  details: {
    fontSize: 12,
    color: colors.gray,
    marginTop: 5,
  },
  empty: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 16,
    color: colors.gray,
  },
});
```

#### 🎯 Desafio 2: Lista com Pull-to-Refresh (30 min)

**Tarefa:** Adicionar pull-to-refresh em UsersOnlineScreen

**Requisitos:**
- Implementar refreshing state
- Função handleRefresh que simula carregamento
- Mostrar indicador de loading
- Atualizar lista após 2 segundos

**Dica:**

```jsx
const [refreshing, setRefreshing] = useState(false);

const handleRefresh = () => {
  setRefreshing(true);
  
  // Simular carregamento
  setTimeout(() => {
    // Atualizar dados aqui
    setRefreshing(false);
  }, 2000);
};

<FlatList
  data={usuarios}
  renderItem={renderUsuario}
  keyExtractor={(item) => item.id.toString()}
  refreshing={refreshing}
  onRefresh={handleRefresh}
/>
```

**Checklist:**
- [ ] HistoryScreen criada
- [ ] Pull-to-refresh funcionando
- [ ] Todas as listas usando FlatList
- [ ] ListEmptyComponent em todas

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **Quando usar FlatList vs map()?**
   - FlatList: listas grandes (>20 itens) / map(): listas pequenas

2. **Por que keyExtractor é importante?**
   - Identifica itens únicos, melhora performance

3. **Como filtrar lista?**
   - array.filter() antes de passar para data

4. **O que é virtualização?**
   - Renderizar apenas itens visíveis na tela

#### 🎯 Componentes de Lista

```
ScrollView + map()  → Listas pequenas
FlatList           → Listas grandes
SectionList        → Listas com seções
VirtualizedList    → Customização avançada
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Usar FlatList
- [ ] Implementar renderItem
- [ ] Usar keyExtractor
- [ ] Filtrar listas
- [ ] Renderização condicional
- [ ] ListEmptyComponent
- [ ] Pull-to-refresh

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar ordenação (A-Z, Z-A)
   - Implementar infinite scroll
   - Criar lista com seções (SectionList)

2. **Estudo:**
   - Ler sobre SectionList
   - Explorar otimizações de FlatList

---

## 📊 Avaliação

### Critérios (Peso: 15% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **FlatList** | 35% | Uso correto e eficiente |
| **Busca/Filtro** | 25% | Implementação funcional |
| **Renderização Condicional** | 20% | Estados empty/loading |
| **HistoryScreen** | 20% | Desafio completo |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Preparar exemplos com muitos itens
- [ ] Demonstrar diferença de performance
- [ ] Revisar FlatList props

### Pontos de Atenção
- ⚠️ Alunos esquecem keyExtractor
- ⚠️ Usam index como key
- ⚠️ Não entendem virtualização
- ⚠️ Confundem data com renderItem

### Troubleshooting

**Problema:** "Warning: Each child should have unique key"
**Solução:** Adicionar keyExtractor

**Problema:** "Lista não atualiza"
**Solução:** Verificar se data é novo array

---

## 📎 Recursos Adicionais

- [FlatList Docs](https://reactnative.dev/docs/flatlist)
- [Performance Optimization](https://reactnative.dev/docs/optimizing-flatlist-configuration)

### Próxima Aula
**Aula 06 - Integração com API Backend**
- Fetch e Axios
- Consumir endpoints
- AsyncStorage
- Autenticação JWT

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
