# Aula 01 - Introdução ao Frontend Mobile e Ambiente React Native

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Configuração de ambiente e fundamentos de desenvolvimento mobile

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Compreender a arquitetura completa do MeetStranger (Frontend + Backend + DB)
- ✅ Diferenciar desenvolvimento mobile nativo vs híbrido vs cross-platform
- ✅ Entender o papel do React Native no ecossistema mobile
- ✅ Configurar ambiente de desenvolvimento (Node, Expo)
- ✅ Criar projeto React Native com Expo
- ✅ Executar aplicativo em emulador/dispositivo físico

---

## 📚 Conteúdo Programático

### 1. Arquitetura do MeetStranger
- Frontend Mobile (React Native)
- Backend (Node.js/Express)
- Banco de Dados (SQLite)
- Comunicação via API REST

### 2. Conceitos de Frontend Mobile
- Aplicativos nativos vs híbridos
- React Native: "Learn once, write anywhere"
- JSX e componentes
- Expo vs React Native CLI

### 3. Configuração do Ambiente
- Node.js e NPM
- Expo CLI
- Expo Go (app para testes)
- Emuladores (Android Studio / Xcode)

### 4. Primeiro Projeto
- Criação com Expo
- Estrutura de pastas
- Execução no dispositivo

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Módulos Anteriores:**
- Part 01: Lógica de programação
- Part 02: Banco de dados SQL
- Part 03: Backend com Node.js/Express

**Atividade de Aquecimento:**
```
Discussão:
- Quais apps vocês usam no celular?
- Como esses apps se comunicam com servidores?
- Qual a diferença entre app mobile e site mobile?

Objetivo: Conectar conhecimento prévio com frontend mobile
```

**Checkpoint:**
- Desenhar no quadro: Cliente (App) ↔ API ↔ Banco de Dados
- Relembrar endpoints criados no backend

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Arquitetura do MeetStranger (15 min)

**Visão Geral:**

```
┌─────────────────────────────────────────────────┐
│           FRONTEND MOBILE (Part 04)             │
│              React Native + Expo                │
│                                                 │
│  • Telas de Login/Cadastro                      │
│  • Seleção de Categorias                        │
│  • Fila de Matching                             │
│  • Chat em Tempo Real                           │
│  • Perfil e Estatísticas                        │
└─────────────────┬───────────────────────────────┘
                  │
                  │ HTTP/HTTPS (API REST)
                  │ JSON
                  ▼
┌─────────────────────────────────────────────────┐
│            BACKEND API (Part 03)                │
│              Node.js + Express                  │
│                                                 │
│  • Autenticação (JWT)                           │
│  • CRUD Usuários                                │
│  • Sistema de Matching                          │
│  • Gerenciamento de Salas                       │
└─────────────────┬───────────────────────────────┘
                  │
                  │ SQL Queries
                  ▼
┌─────────────────────────────────────────────────┐
│          BANCO DE DADOS (Part 02)               │
│                  SQLite                         │
│                                                 │
│  • usuarios                                     │
│  • categorias                                   │
│  • salas                                        │
│  • fila_matching                                │
│  • estatisticas_usuario                         │
└─────────────────────────────────────────────────┘
```

**Fluxo de Dados:**
1. Usuário interage com app (Frontend)
2. App faz requisição HTTP para API (Backend)
3. API processa e consulta banco de dados
4. Banco retorna dados para API
5. API retorna JSON para app
6. App exibe dados na interface

#### 📖 Parte 2: React Native - Visão Geral (20 min)

**O que é React Native?**
- Framework para criar apps mobile usando JavaScript/React
- Código compartilhado entre iOS e Android
- Componentes nativos (não WebView)
- Criado pelo Facebook (Meta)

**Nativo vs Híbrido vs Cross-Platform:**

| Tipo | Tecnologia | Vantagens | Desvantagens |
|------|------------|-----------|--------------|
| **Nativo** | Swift/Kotlin | Performance máxima | Código duplicado |
| **Híbrido** | Ionic/Cordova | Web tech | Performance inferior |
| **Cross-Platform** | React Native/Flutter | Código compartilhado + Performance | Curva de aprendizado |

**Por que React Native para MeetStranger?**
- ✅ Código compartilhado (iOS + Android)
- ✅ Performance próxima ao nativo
- ✅ Comunidade grande
- ✅ Integração fácil com APIs REST
- ✅ Hot reload (desenvolvimento rápido)

**JSX - JavaScript + XML:**
```jsx
// JavaScript tradicional
const elemento = React.createElement('div', null, 'Hello');

// JSX (mais legível)
const elemento = <View><Text>Hello</Text></View>;
```

#### 📖 Parte 3: Expo vs React Native CLI (15 min)

**Expo:**
- ✅ Configuração zero
- ✅ Testa no celular sem emulador (Expo Go)
- ✅ Bibliotecas prontas
- ✅ Build na nuvem
- ❌ Limitações em módulos nativos

**React Native CLI:**
- ✅ Controle total
- ✅ Qualquer biblioteca nativa
- ❌ Configuração complexa
- ❌ Precisa Xcode/Android Studio

**Escolha para MeetStranger: Expo**
- Projeto educacional
- Funcionalidades cobertas pelo Expo
- Desenvolvimento mais rápido

#### 📖 Parte 4: Estrutura de um App React Native (10 min)

**Componentes Principais:**

```jsx
import { View, Text, Button } from 'react-native';

function App() {
  return (
    <View>
      <Text>MeetStranger</Text>
      <Button title="Entrar" onPress={() => {}} />
    </View>
  );
}
```

**Componentes Básicos:**
- `View`: Container (como `<div>`)
- `Text`: Texto (como `<p>`)
- `Button`: Botão
- `TextInput`: Campo de texto
- `ScrollView`: Área rolável
- `FlatList`: Lista otimizada

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Instalar Node.js e Expo CLI (20 min)

**Verificar Node.js:**
```bash
node --version
# Deve ser 14+

npm --version
```

**Se não tiver Node.js:**
- Baixar em: https://nodejs.org/
- Instalar versão LTS
- Reiniciar terminal

**Instalar Expo CLI:**
```bash
npm install -g expo-cli

# Verificar instalação
expo --version
```

**Instalar Expo Go no celular:**
- Android: Google Play Store
- iOS: App Store
- Buscar: "Expo Go"

#### 💻 Exercício 2: Criar Projeto MeetStranger Mobile (30 min)

**Criar projeto:**
```bash
cd "c:\Users\jerem\OneDrive\Desktop\meetStranger App"

expo init meetstranger-mobile

# Escolher template: blank
```

**Estrutura criada:**
```
meetstranger-mobile/
├── App.js              # Componente principal
├── app.json            # Configurações do app
├── package.json        # Dependências
├── node_modules/       # Bibliotecas instaladas
└── assets/             # Imagens, ícones
```

**Explorar App.js:**
```jsx
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

#### 💻 Exercício 3: Executar App (40 min)

**Iniciar servidor:**
```bash
cd meetstranger-mobile
expo start
```

**Opção 1: Dispositivo Físico (Recomendado)**
- Abre navegador com QR Code
- Abrir Expo Go no celular
- Escanear QR Code
- App carrega no celular

**Opção 2: Emulador Android**
```bash
expo start --android
```

**Testar Hot Reload:**
1. Modificar texto em App.js
2. Salvar arquivo
3. App atualiza automaticamente

**Modificar App.js:**
```jsx
export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>MeetStranger</Text>
      <Text style={styles.subtitle}>Converse com estranhos</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#6C63FF',
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 32,
    fontWeight: 'bold',
    color: '#fff',
    marginBottom: 10,
  },
  subtitle: {
    fontSize: 16,
    color: '#fff',
  },
});
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Personalizar Tela Inicial (30 min)

**Tarefa:** Criar tela de boas-vindas do MeetStranger

**Requisitos:**
- Título "MeetStranger"
- Subtítulo "Converse anonimamente sobre seus interesses"
- Ícone ou emoji (🎭)
- Cor de fundo: #6C63FF (roxo)
- Texto branco

**Dica:**
```jsx
<Text style={{ fontSize: 48 }}>🎭</Text>
```

#### 🎯 Desafio 2: Adicionar Botão (30 min)

**Tarefa:** Adicionar botão "Começar"

**Requisitos:**
- Usar componente `TouchableOpacity`
- Ao clicar, mostrar alert
- Estilizar botão

**Exemplo:**
```jsx
import { Alert, TouchableOpacity } from 'react-native';

<TouchableOpacity 
  style={styles.button}
  onPress={() => Alert.alert('Bem-vindo!', 'Em breve você poderá fazer login')}
>
  <Text style={styles.buttonText}>Começar</Text>
</TouchableOpacity>

// Styles
button: {
  backgroundColor: '#fff',
  paddingHorizontal: 40,
  paddingVertical: 15,
  borderRadius: 25,
  marginTop: 30,
},
buttonText: {
  color: '#6C63FF',
  fontSize: 18,
  fontWeight: 'bold',
},
```

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **Qual a diferença entre React e React Native?**
   - React: web / React Native: mobile

2. **Por que usar Expo?**
   - Facilita desenvolvimento, testa no celular sem emulador

3. **O que é JSX?**
   - Sintaxe que mistura JavaScript com XML/HTML

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Explicar arquitetura do MeetStranger
- [ ] Diferenciar nativo vs cross-platform
- [ ] Instalar Node.js e Expo CLI
- [ ] Criar projeto React Native
- [ ] Executar app no dispositivo
- [ ] Modificar componentes básicos

#### 📚 Para Casa

1. **Exploração:**
   - Testar outros componentes (Image, ScrollView)
   - Modificar cores e estilos

2. **Estudo:**
   - Ler documentação: https://reactnative.dev/

---

## 📊 Avaliação

### Critérios (Peso: 10% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Ambiente Configurado** | 40% | Node, Expo, app rodando |
| **Compreensão Arquitetura** | 30% | Entende fluxo Frontend-Backend-DB |
| **Personalização** | 30% | Tela inicial customizada |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Testar instalação do Expo
- [ ] Ter QR Code pronto
- [ ] Preparar emulador Android
- [ ] Verificar conexão de rede

### Pontos de Atenção
- ⚠️ Alunos com Node.js desatualizado
- ⚠️ Firewall bloqueando Expo
- ⚠️ Celular e computador em redes diferentes

### Troubleshooting

**Problema:** "Expo Go não conecta"
**Solução:** Verificar mesma rede Wi-Fi

**Problema:** "App não atualiza"
**Solução:** Pressionar 'r' no terminal

---

## 📎 Recursos Adicionais

- [React Native Docs](https://reactnative.dev/)
- [Expo Docs](https://docs.expo.dev/)

### Próxima Aula
**Aula 02 - Componentes e Estilização**
- Componentes básicos
- StyleSheet e Flexbox
- Telas de Login e Cadastro

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0
