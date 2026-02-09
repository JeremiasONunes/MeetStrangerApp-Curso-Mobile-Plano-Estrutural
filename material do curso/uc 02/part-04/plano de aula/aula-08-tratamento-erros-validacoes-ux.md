# Aula 08 - Tratamento de Erros, Validações e UX

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Validações, tratamento de erros e experiência do usuário

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Implementar validações robustas de formulários
- ✅ Criar mensagens de erro claras e úteis
- ✅ Tratar erros de API adequadamente
- ✅ Implementar feedback visual (loading, success, error)
- ✅ Aplicar boas práticas de UX mobile
- ✅ Criar componentes de validação reutilizáveis
- ✅ Melhorar acessibilidade do app

---

## 📚 Conteúdo Programático

### 1. Validações de Formulários
- Validação em tempo real
- Validação ao submeter
- Mensagens de erro específicas
- Validação customizada

### 2. Tratamento de Erros
- Erros de rede
- Erros de API (4xx, 5xx)
- Timeout
- Retry automático

### 3. Feedback Visual
- Loading states
- Success feedback
- Error feedback
- Empty states

### 4. Boas Práticas UX
- Desabilitar botões durante loading
- Indicadores de progresso
- Confirmações importantes
- Mensagens claras

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- CRUD completo
- Integração frontend-backend
- Atualização de listas

**Atividade de Aquecimento:**
```
Discussão:
- O que irrita você em apps mal feitos?
- Como apps bons mostram erros?
- Por que validar dados antes de enviar?

Objetivo: Sensibilizar para importância da UX
```

**Checkpoint:**
- Revisar validações já implementadas
- Identificar pontos de melhoria

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Validações Avançadas (20 min)

**Tipos de Validação:**

```javascript
// 1. Validação de formato
const validarEmail = (email) => {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
};

// 2. Validação de tamanho
const validarSenha = (senha) => {
  return senha.length >= 6 && senha.length <= 20;
};

// 3. Validação de caracteres
const validarUsername = (username) => {
  const regex = /^[a-zA-Z0-9_]+$/;
  return regex.test(username);
};

// 4. Validação customizada
const validarIdade = (idade) => {
  return idade >= 13 && idade <= 120;
};
```

**Validação em Tempo Real:**

```javascript
const [email, setEmail] = useState('');
const [emailError, setEmailError] = useState('');

const handleEmailChange = (text) => {
  setEmail(text);
  
  if (text && !validarEmail(text)) {
    setEmailError('Email inválido');
  } else {
    setEmailError('');
  }
};

<Input
  value={email}
  onChangeText={handleEmailChange}
  error={emailError}
/>
```

**Validação ao Submeter:**

```javascript
const validarFormulario = () => {
  const erros = {};
  
  if (!username) {
    erros.username = 'Username é obrigatório';
  } else if (username.length < 3) {
    erros.username = 'Username deve ter no mínimo 3 caracteres';
  }
  
  if (!email) {
    erros.email = 'Email é obrigatório';
  } else if (!validarEmail(email)) {
    erros.email = 'Email inválido';
  }
  
  if (!senha) {
    erros.senha = 'Senha é obrigatória';
  } else if (senha.length < 6) {
    erros.senha = 'Senha deve ter no mínimo 6 caracteres';
  }
  
  return erros;
};

const handleSubmit = () => {
  const erros = validarFormulario();
  
  if (Object.keys(erros).length > 0) {
    setErrors(erros);
    return;
  }
  
  // Enviar dados
};
```

#### 📖 Parte 2: Tratamento de Erros de API (15 min)

**Categorias de Erro:**

```javascript
const handleApiError = (error) => {
  // Erro de rede
  if (!error.response) {
    return 'Sem conexão com a internet';
  }
  
  // Erro do cliente (4xx)
  if (error.response.status >= 400 && error.response.status < 500) {
    switch (error.response.status) {
      case 400:
        return error.response.data.erro || 'Dados inválidos';
      case 401:
        return 'Não autorizado. Faça login novamente';
      case 404:
        return 'Recurso não encontrado';
      case 409:
        return error.response.data.erro || 'Conflito de dados';
      default:
        return 'Erro na requisição';
    }
  }
  
  // Erro do servidor (5xx)
  if (error.response.status >= 500) {
    return 'Erro no servidor. Tente novamente mais tarde';
  }
  
  return 'Erro desconhecido';
};

// Uso
try {
  await api.post('/usuarios', dados);
} catch (error) {
  const mensagem = handleApiError(error);
  Alert.alert('Erro', mensagem);
}
```

**Retry Automático:**

```javascript
const fetchComRetry = async (url, tentativas = 3) => {
  for (let i = 0; i < tentativas; i++) {
    try {
      const response = await api.get(url);
      return response.data;
    } catch (error) {
      if (i === tentativas - 1) throw error;
      await new Promise(resolve => setTimeout(resolve, 1000 * (i + 1)));
    }
  }
};
```

#### 📖 Parte 3: Feedback Visual (15 min)

**Estados de Loading:**

```javascript
// Loading inline
{loading && <ActivityIndicator />}

// Loading overlay
{loading && (
  <View style={styles.overlay}>
    <ActivityIndicator size="large" color="#fff" />
    <Text style={styles.loadingText}>Carregando...</Text>
  </View>
)}

// Loading em botão
<Button 
  title={loading ? 'Carregando...' : 'Salvar'}
  disabled={loading}
/>
```

**Toast Messages:**

```javascript
// Criar componente Toast
const Toast = ({ message, type, visible, onHide }) => {
  useEffect(() => {
    if (visible) {
      const timer = setTimeout(onHide, 3000);
      return () => clearTimeout(timer);
    }
  }, [visible]);

  if (!visible) return null;

  return (
    <View style={[
      styles.toast,
      type === 'success' && styles.toastSuccess,
      type === 'error' && styles.toastError
    ]}>
      <Text style={styles.toastText}>{message}</Text>
    </View>
  );
};
```

**Empty States:**

```javascript
const EmptyState = ({ icon, title, description, action }) => (
  <View style={styles.emptyContainer}>
    <Text style={styles.emptyIcon}>{icon}</Text>
    <Text style={styles.emptyTitle}>{title}</Text>
    <Text style={styles.emptyDescription}>{description}</Text>
    {action && <Button title={action.title} onPress={action.onPress} />}
  </View>
);

// Uso
<EmptyState
  icon="📭"
  title="Nenhuma conversa"
  description="Você ainda não iniciou nenhuma conversa"
  action={{ title: 'Começar', onPress: handleStart }}
/>
```

#### 📖 Parte 4: Boas Práticas UX (10 min)

**Desabilitar Durante Loading:**

```javascript
<Button 
  title="Salvar"
  onPress={handleSave}
  disabled={loading}
/>

<TextInput
  editable={!loading}
/>
```

**Confirmações:**

```javascript
// Ações destrutivas
Alert.alert(
  'Confirmar Exclusão',
  'Esta ação não pode ser desfeita',
  [
    { text: 'Cancelar', style: 'cancel' },
    { text: 'Excluir', style: 'destructive', onPress: handleDelete }
  ]
);

// Sair sem salvar
const handleGoBack = () => {
  if (hasChanges) {
    Alert.alert(
      'Descartar Alterações?',
      'Você tem alterações não salvas',
      [
        { text: 'Cancelar', style: 'cancel' },
        { text: 'Descartar', onPress: () => navigation.goBack() }
      ]
    );
  } else {
    navigation.goBack();
  }
};
```

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Criar Utilitário de Validação (25 min)

**Criar:** `src/utils/validation.js`

```javascript
export const validarEmail = (email) => {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
};

export const validarSenha = (senha) => {
  if (!senha) return { valido: false, erro: 'Senha é obrigatória' };
  if (senha.length < 6) return { valido: false, erro: 'Mínimo 6 caracteres' };
  if (senha.length > 20) return { valido: false, erro: 'Máximo 20 caracteres' };
  return { valido: true };
};

export const validarUsername = (username) => {
  if (!username) return { valido: false, erro: 'Username é obrigatório' };
  if (username.length < 3) return { valido: false, erro: 'Mínimo 3 caracteres' };
  if (username.length > 20) return { valido: false, erro: 'Máximo 20 caracteres' };
  
  const regex = /^[a-zA-Z0-9_]+$/;
  if (!regex.test(username)) {
    return { valido: false, erro: 'Apenas letras, números e _' };
  }
  
  return { valido: true };
};

export const validarFormularioUsuario = (dados) => {
  const erros = {};
  
  const validacaoUsername = validarUsername(dados.username);
  if (!validacaoUsername.valido) {
    erros.username = validacaoUsername.erro;
  }
  
  if (!dados.email) {
    erros.email = 'Email é obrigatório';
  } else if (!validarEmail(dados.email)) {
    erros.email = 'Email inválido';
  }
  
  const validacaoSenha = validarSenha(dados.senha);
  if (!validacaoSenha.valido) {
    erros.senha = validacaoSenha.erro;
  }
  
  return erros;
};
```

#### 💻 Exercício 2: Componente Input com Erro (25 min)

**Atualizar:** `src/components/Input.js`

```javascript
import { View, TextInput, Text, StyleSheet } from 'react-native';
import colors from '../styles/colors';

export default function Input({ 
  placeholder, 
  value, 
  onChangeText, 
  secureTextEntry,
  keyboardType = 'default',
  editable = true,
  error,
  label
}) {
  return (
    <View style={styles.container}>
      {label && <Text style={styles.label}>{label}</Text>}
      
      <TextInput
        style={[
          styles.input,
          error && styles.inputError,
          !editable && styles.inputDisabled
        ]}
        placeholder={placeholder}
        value={value}
        onChangeText={onChangeText}
        secureTextEntry={secureTextEntry}
        keyboardType={keyboardType}
        placeholderTextColor={colors.gray}
        editable={editable}
      />
      
      {error && <Text style={styles.errorText}>{error}</Text>}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    marginBottom: 15,
  },
  label: {
    fontSize: 14,
    fontWeight: '600',
    color: colors.black,
    marginBottom: 5,
  },
  input: {
    backgroundColor: colors.white,
    borderRadius: 10,
    padding: 15,
    fontSize: 16,
    borderWidth: 1,
    borderColor: '#ddd',
  },
  inputError: {
    borderColor: colors.error,
  },
  inputDisabled: {
    backgroundColor: '#f5f5f5',
    color: colors.gray,
  },
  errorText: {
    color: colors.error,
    fontSize: 12,
    marginTop: 5,
    marginLeft: 5,
  },
});
```

#### 💻 Exercício 3: Refatorar RegisterScreen com Validações (40 min)

**Atualizar:** `src/screens/RegisterScreen.js`

```javascript
import { useState } from 'react';
import { View, StyleSheet, Alert, TouchableOpacity, Text, ActivityIndicator, ScrollView, KeyboardAvoidingView, Platform } from 'react-native';
import Input from '../components/Input';
import Button from '../components/Button';
import api from '../services/api';
import { validarFormularioUsuario } from '../utils/validation';
import colors from '../styles/colors';

export default function RegisterScreen({ navigation }) {
  const [username, setUsername] = useState('');
  const [email, setEmail] = useState('');
  const [senha, setSenha] = useState('');
  const [confirmarSenha, setConfirmarSenha] = useState('');
  const [errors, setErrors] = useState({});
  const [loading, setLoading] = useState(false);

  const handleCadastro = async () => {
    // Limpar erros anteriores
    setErrors({});

    // Validar formulário
    const errosValidacao = validarFormularioUsuario({ username, email, senha });
    
    // Validar confirmação de senha
    if (senha !== confirmarSenha) {
      errosValidacao.confirmarSenha = 'Senhas não conferem';
    }

    // Se houver erros, exibir e parar
    if (Object.keys(errosValidacao).length > 0) {
      setErrors(errosValidacao);
      Alert.alert('Erro', 'Corrija os erros no formulário');
      return;
    }

    setLoading(true);

    try {
      await api.post('/usuarios', {
        username,
        email,
        senha
      });

      Alert.alert(
        'Sucesso! 🎉',
        'Cadastro realizado com sucesso! Faça login para continuar.',
        [{ text: 'OK', onPress: () => navigation.goBack() }]
      );
    } catch (error) {
      console.error(error);
      
      let mensagemErro = 'Não foi possível cadastrar. Tente novamente.';
      
      if (error.response?.status === 409) {
        mensagemErro = 'Email ou username já cadastrado';
      } else if (error.response?.status === 400) {
        mensagemErro = error.response.data.erro || 'Dados inválidos';
      } else if (!error.response) {
        mensagemErro = 'Sem conexão com a internet';
      }
      
      Alert.alert('Erro', mensagemErro);
    } finally {
      setLoading(false);
    }
  };

  return (
    <KeyboardAvoidingView 
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <ScrollView contentContainerStyle={styles.scrollContent}>
        <View style={styles.content}>
          <Input
            label="Username"
            placeholder="Escolha um username"
            value={username}
            onChangeText={setUsername}
            editable={!loading}
            error={errors.username}
          />
          
          <Input
            label="Email"
            placeholder="seu@email.com"
            value={email}
            onChangeText={setEmail}
            keyboardType="email-address"
            editable={!loading}
            error={errors.email}
          />
          
          <Input
            label="Senha"
            placeholder="Mínimo 6 caracteres"
            value={senha}
            onChangeText={setSenha}
            secureTextEntry
            editable={!loading}
            error={errors.senha}
          />
          
          <Input
            label="Confirmar Senha"
            placeholder="Digite a senha novamente"
            value={confirmarSenha}
            onChangeText={setConfirmarSenha}
            secureTextEntry
            editable={!loading}
            error={errors.confirmarSenha}
          />
          
          {loading ? (
            <View style={styles.loadingContainer}>
              <ActivityIndicator size="large" color={colors.primary} />
              <Text style={styles.loadingText}>Criando conta...</Text>
            </View>
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
      </ScrollView>
    </KeyboardAvoidingView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: colors.background,
  },
  scrollContent: {
    flexGrow: 1,
  },
  content: {
    flex: 1,
    padding: 20,
  },
  loadingContainer: {
    alignItems: 'center',
    marginVertical: 20,
  },
  loadingText: {
    marginTop: 10,
    color: colors.gray,
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

#### 🎯 Desafio 1: Componente Toast (30 min)

**Tarefa:** Criar componente de notificação toast

**Criar:** `src/components/Toast.js`

```javascript
import { useEffect } from 'react';
import { View, Text, StyleSheet, Animated } from 'react-native';
import colors from '../styles/colors';

export default function Toast({ message, type = 'info', visible, onHide, duration = 3000 }) {
  const opacity = new Animated.Value(0);

  useEffect(() => {
    if (visible) {
      Animated.sequence([
        Animated.timing(opacity, {
          toValue: 1,
          duration: 300,
          useNativeDriver: true,
        }),
        Animated.delay(duration),
        Animated.timing(opacity, {
          toValue: 0,
          duration: 300,
          useNativeDriver: true,
        }),
      ]).start(() => onHide());
    }
  }, [visible]);

  if (!visible) return null;

  const getBackgroundColor = () => {
    switch (type) {
      case 'success': return colors.success;
      case 'error': return colors.error;
      case 'warning': return '#FF9800';
      default: return colors.primary;
    }
  };

  return (
    <Animated.View 
      style={[
        styles.container,
        { backgroundColor: getBackgroundColor(), opacity }
      ]}
    >
      <Text style={styles.message}>{message}</Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  container: {
    position: 'absolute',
    bottom: 50,
    left: 20,
    right: 20,
    padding: 15,
    borderRadius: 10,
    elevation: 5,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.25,
    shadowRadius: 3.84,
  },
  message: {
    color: colors.white,
    fontSize: 14,
    textAlign: 'center',
  },
});
```

**Usar no LoginScreen:**

```javascript
const [toast, setToast] = useState({ visible: false, message: '', type: 'info' });

const showToast = (message, type = 'info') => {
  setToast({ visible: true, message, type });
};

// Após login bem-sucedido
showToast('Login realizado com sucesso!', 'success');

// Renderizar
<Toast
  message={toast.message}
  type={toast.type}
  visible={toast.visible}
  onHide={() => setToast({ ...toast, visible: false })}
/>
```

#### 🎯 Desafio 2: Empty State Component (30 min)

**Tarefa:** Criar componente de estado vazio reutilizável

**Criar:** `src/components/EmptyState.js`

```javascript
import { View, Text, StyleSheet } from 'react-native';
import Button from './Button';
import colors from '../styles/colors';

export default function EmptyState({ 
  icon = '📭', 
  title, 
  description, 
  actionTitle,
  onAction 
}) {
  return (
    <View style={styles.container}>
      <Text style={styles.icon}>{icon}</Text>
      <Text style={styles.title}>{title}</Text>
      {description && <Text style={styles.description}>{description}</Text>}
      {actionTitle && onAction && (
        <Button 
          title={actionTitle} 
          onPress={onAction}
          variant="secondary"
        />
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 40,
  },
  icon: {
    fontSize: 64,
    marginBottom: 20,
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
    color: colors.black,
    textAlign: 'center',
    marginBottom: 10,
  },
  description: {
    fontSize: 14,
    color: colors.gray,
    textAlign: 'center',
    marginBottom: 20,
  },
});
```

**Usar em ManageUsersScreen:**

```javascript
ListEmptyComponent={() => (
  <EmptyState
    icon="👥"
    title="Nenhum usuário cadastrado"
    description="Adicione o primeiro usuário para começar"
    actionTitle="Adicionar Usuário"
    onAction={() => navigation.navigate('AddUser')}
  />
)}
```

**Checklist:**
- [ ] Toast component criado
- [ ] EmptyState component criado
- [ ] Validações em todos os formulários
- [ ] Mensagens de erro claras
- [ ] Loading states implementados

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **Por que validar no frontend E no backend?**
   - Frontend: UX / Backend: Segurança

2. **Quando usar Alert vs Toast?**
   - Alert: ações importantes / Toast: feedback rápido

3. **O que é Empty State?**
   - Tela quando não há dados para exibir

#### 🎯 Hierarquia de Feedback

```
1. Inline (erro no campo)
2. Toast (notificação rápida)
3. Alert (ação importante)
4. Modal (informação detalhada)
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Validar formulários
- [ ] Criar mensagens de erro claras
- [ ] Tratar erros de API
- [ ] Implementar loading states
- [ ] Criar feedback visual
- [ ] Usar Toast e EmptyState
- [ ] Melhorar UX do app

#### 📚 Para Casa

1. **Implementação:**
   - Adicionar validação em tempo real
   - Criar componente de erro global
   - Implementar retry automático

2. **UX:**
   - Testar app com olhos de usuário
   - Identificar pontos de melhoria
   - Documentar sugestões

---

## 📊 Avaliação

### Critérios (Peso: 15% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Validações** | 30% | Formulários validados corretamente |
| **Tratamento de Erros** | 30% | Erros tratados adequadamente |
| **Feedback Visual** | 25% | Loading, toast, empty states |
| **UX** | 15% | Experiência do usuário melhorada |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Preparar exemplos de boa/má UX
- [ ] Testar componentes Toast e EmptyState
- [ ] Ter lista de validações comuns

### Pontos de Atenção
- ⚠️ Alunos fazem validações muito simples
- ⚠️ Mensagens de erro genéricas
- ⚠️ Esquecem loading states
- ⚠️ Não testam cenários de erro

---

## 📎 Recursos Adicionais

- [React Native UX Best Practices](https://reactnative.dev/docs/performance)
- [Form Validation](https://formik.org/)

### Próxima Aula
**Aula 09-10 - Finalização e Apresentação**
- Polimento final
- Testes completos
- Documentação
- Preparação da apresentação

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
