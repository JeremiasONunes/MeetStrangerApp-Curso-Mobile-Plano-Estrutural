# UC 02 - Part 04: Desenvolvimento Frontend Mobile com React Native

**Carga Horária Total:** 40 horas  
**Modalidade:** Presencial  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo

---

## 📋 Visão Geral

Este módulo aborda o desenvolvimento completo do frontend mobile da aplicação MeetStranger usando React Native e Expo, desde a configuração do ambiente até a geração do build final, integrando com o backend desenvolvido na Part 03.

---

## 🎯 Competências Desenvolvidas

Ao concluir este módulo, o aluno será capaz de:

- ✅ Desenvolver aplicativos mobile com React Native
- ✅ Criar interfaces responsivas e intuitivas
- ✅ Gerenciar estado e navegação
- ✅ Integrar frontend com APIs REST
- ✅ Implementar CRUD completo no mobile
- ✅ Aplicar validações e melhorar UX
- ✅ Gerar builds e preparar para distribuição
- ✅ Documentar aplicativos profissionalmente

---

## 📚 Estrutura do Módulo

### Aula 01 - Introdução ao Frontend Mobile e Ambiente React Native (4h)
**Conteúdo:**
- Arquitetura MeetStranger (Frontend + Backend + DB)
- React Native vs Nativo vs Híbrido
- Expo vs React Native CLI
- Instalação Node.js e Expo CLI
- Criação do projeto meetstranger-mobile
- Execução no dispositivo/emulador
- Componentes básicos (View, Text, TouchableOpacity)

**Entregáveis:**
- Ambiente configurado
- Projeto criado
- App rodando no dispositivo

---

### Aula 02 - Estrutura do Projeto e Componentização (4h)
**Conteúdo:**
- Estrutura de pastas profissional
- Componentes funcionais e props
- JSX em profundidade
- Header, Button, Card components
- colors.js para padronização
- HomeScreen completa

**Entregáveis:**
- Estrutura de pastas organizada
- 4+ componentes reutilizáveis
- Primeira tela funcional

---

### Aula 03 - Propriedades (Props) e Estados (State) (4h)
**Conteúdo:**
- Props vs State
- useState hook
- Formulários controlados
- CounterScreen (exemplo prático)
- LoginScreen com validação
- CategoryScreen (lista selecionável)
- RegisterScreen e ProfileScreen

**Entregáveis:**
- 5+ telas com estado
- Formulários funcionando
- Validações básicas

---

### Aula 04 - Navegação entre Telas (4h)
**Conteúdo:**
- React Navigation instalação
- Stack Navigator
- NavigationContainer
- Navegação (navigate, goBack, replace)
- Passagem de parâmetros (route.params)
- Configuração de header
- Fluxo Login → Home → Categories → Chat

**Entregáveis:**
- Navegação completa
- 6+ telas integradas
- Parâmetros funcionando

---

### Aula 05 - Listas, Coleções e Renderização de Dados (4h)
**Conteúdo:**
- map() vs FlatList
- FlatList completo (renderItem, keyExtractor, separators)
- Renderização condicional
- UsersOnlineScreen
- SearchUsersScreen (busca em tempo real)
- ChatScreen com FlatList de mensagens
- Pull-to-refresh

**Entregáveis:**
- 3+ telas com FlatList
- Busca implementada
- Empty states

---

### Aula 06 - Integração com APIs REST (4h)
**Conteúdo:**
- Comunicação HTTP cliente-servidor
- Fetch vs Axios
- Configuração api.js com interceptors
- AsyncStorage para JWT
- LoginScreen com API real
- RegisterScreen com API
- CategoryScreen buscando do backend
- Tratamento de erros (401, 409, 400, 500)

**Entregáveis:**
- api.js configurado
- Login/Logout funcionando
- 3+ telas integradas com backend

---

### Aula 07 - CRUD Completo no Frontend (4h)
**Conteúdo:**
- CRUD completo (Create, Read, Update, Delete)
- ManageUsersScreen (listar + deletar)
- AddUserScreen (criar)
- EditUserScreen (atualizar)
- Atualização de lista após operações
- Confirmações de ações destrutivas
- CRUD de Categorias (desafio)

**Entregáveis:**
- CRUD de usuários completo
- CRUD de categorias completo
- Validações implementadas

---

### Aula 08 - Tratamento de Erros, Validações e UX (4h)
**Conteúdo:**
- Validações avançadas (regex)
- validation.js utilitário
- Input component com erro
- Tratamento de erros de API
- Toast component com animação
- EmptyState component
- KeyboardAvoidingView
- Boas práticas UX

**Entregáveis:**
- Validações em todos os formulários
- Toast e EmptyState components
- UX otimizada

---

### Aula 09 - Build, Execução e Distribuição (4h)
**Conteúdo:**
- Build de desenvolvimento vs produção
- Configuração app.json
- Ícone (1024x1024) e splash screen
- EAS CLI e processo de build
- Geração de APK
- Instalação em dispositivo físico
- Preparação para publicação
- BUILD.md

**Entregáveis:**
- APK gerado
- App instalado em dispositivo
- Documentação de build

---

### Aula 10 - Documentação, Manuais e Encerramento (4h)
**Conteúdo:**
- Documentação de código (JSDoc)
- README.md profissional
- Manual de instalação
- Manual do usuário
- Documentação de componentes
- Documentação de API
- Apresentação do projeto
- Avaliação e feedback

**Entregáveis:**
- README.md completo
- Documentação técnica
- Manuais criados
- Projeto finalizado

---

## 🗂️ Estrutura Final do Projeto

```
meetstranger-mobile/
├── src/
│   ├── components/
│   │   ├── Button.js
│   │   ├── Input.js
│   │   ├── Header.js
│   │   ├── Card.js
│   │   ├── CategoryCard.js
│   │   ├── Toast.js
│   │   └── EmptyState.js
│   ├── screens/
│   │   ├── LoginScreen.js
│   │   ├── RegisterScreen.js
│   │   ├── HomeScreen.js
│   │   ├── CategoryScreen.js
│   │   ├── ChatScreen.js
│   │   ├── ProfileScreen.js
│   │   ├── ManageUsersScreen.js
│   │   ├── AddUserScreen.js
│   │   ├── EditUserScreen.js
│   │   ├── UsersOnlineScreen.js
│   │   ├── SearchUsersScreen.js
│   │   └── HistoryScreen.js
│   ├── services/
│   │   └── api.js
│   ├── styles/
│   │   └── colors.js
│   └── utils/
│       ├── validation.js
│       └── logger.js
├── assets/
│   ├── icon.png
│   ├── splash.png
│   └── adaptive-icon.png
├── docs/
│   ├── COMPONENTS.md
│   ├── API.md
│   ├── APRESENTACAO.md
│   └── REFLEXAO.md
├── .env
├── .env.example
├── .gitignore
├── App.js
├── app.json
├── eas.json
├── package.json
├── BUILD.md
└── README.md
```

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Finalidade |
|------------|--------|------------|
| React Native | 0.71+ | Framework mobile |
| Expo | 48+ | Plataforma de desenvolvimento |
| React Navigation | 6.x | Navegação entre telas |
| Axios | 1.x | Cliente HTTP |
| AsyncStorage | 1.x | Armazenamento local |
| React Native Screens | 3.x | Otimização de navegação |

---

## 📊 Sistema de Avaliação

### Distribuição de Notas

| Aula | Peso | Tipo de Avaliação |
|------|------|-------------------|
| Aula 01 | 10% | Formativa + Prática |
| Aula 02 | 15% | Somativa (Componentes) |
| Aula 03 | 20% | Somativa (Estado e Formulários) |
| Aula 04 | 20% | Somativa (Navegação) |
| Aula 05 | 15% | Somativa (Listas) |
| Aula 06 | 20% | Somativa (Integração API) |
| Aula 07 | 20% | Somativa (CRUD) |
| Aula 08 | 15% | Somativa (Validações) |
| Aula 09 | 10% | Somativa (Build) |
| Aula 10 | 10% | Somativa (Documentação) |
| **Total** | **155%** | *Nota máxima: 100%* |

### Critérios de Avaliação

**Técnicos (60%):**
- Código funcional e sem erros
- Componentes reutilizáveis
- Navegação implementada
- Integração com API funcionando
- CRUD completo
- Validações implementadas

**Boas Práticas (40%):**
- Código limpo e organizado
- Nomenclatura consistente
- Componentização adequada
- Tratamento de erros
- UX otimizada
- Documentação completa

---

## 🎯 Funcionalidades Implementadas

### Autenticação
- ✅ Tela de login
- ✅ Tela de cadastro
- ✅ Validação de credenciais
- ✅ Armazenamento de token JWT
- ✅ Logout

### Navegação
- ✅ Stack Navigator
- ✅ 12+ telas
- ✅ Passagem de parâmetros
- ✅ Navegação fluida

### Categorias
- ✅ Listagem de categorias
- ✅ Seleção de categoria
- ✅ CRUD de categorias (admin)

### Chat
- ✅ Tela de chat (mock)
- ✅ Envio de mensagens
- ✅ Lista de mensagens
- ✅ Indicador de status

### Perfil
- ✅ Visualização de perfil
- ✅ Edição de dados
- ✅ Estatísticas (mock)

### Gerenciamento
- ✅ CRUD de usuários
- ✅ Listagem com busca
- ✅ Validações completas
- ✅ Feedback visual

### UX/UI
- ✅ Loading states
- ✅ Empty states
- ✅ Toast notifications
- ✅ Confirmações
- ✅ Validações em tempo real

---

## 📈 Estatísticas do Módulo

- **Total de Aulas:** 10 sessões (40 horas)
- **Componentes Criados:** 10+
- **Telas Criadas:** 12+
- **Linhas de Código:** ~3.000 linhas
- **Arquivos Criados:** 30+
- **Conceitos Abordados:** 50+
- **Integrações:** Frontend ↔ Backend ↔ Database

---

## 🔗 Conexão com Outros Módulos

### ⬅️ Pré-requisitos

**Part 01 - Lógica de Programação:**
- Algoritmos e estruturas de dados
- Variáveis e operadores
- Estruturas condicionais e de repetição

**Part 02 - Banco de Dados:**
- SQL e modelagem
- CRUD em banco de dados
- Relacionamentos

**Part 03 - Backend:**
- APIs REST
- Node.js e Express
- Autenticação JWT
- Integração com banco

### ➡️ Próximo Módulo

**UC 03 - Testes e Qualidade:**
- Testes unitários
- Testes de integração
- Testes de usabilidade
- Qualidade de software

---

## 💡 Dicas para o Aluno

### Para Ter Sucesso

1. ✅ Pratique todos os exercícios
2. ✅ Teste no dispositivo real
3. ✅ Leia a documentação oficial
4. ✅ Faça commits frequentes
5. ✅ Documente seu código
6. ✅ Peça ajuda quando necessário
7. ✅ Explore além do conteúdo

### Recursos Adicionais

- [React Native Docs](https://reactnative.dev/)
- [Expo Docs](https://docs.expo.dev/)
- [React Navigation](https://reactnavigation.org/)
- [Axios](https://axios-http.com/)
- [AsyncStorage](https://react-native-async-storage.github.io/async-storage/)

### Comunidade

- [React Native Community](https://www.reactnative.dev/community/overview)
- [Expo Forums](https://forums.expo.dev/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/react-native)

---

## 🎓 Competências SENAC Desenvolvidas

### Competências Técnicas
- Desenvolvimento mobile
- React Native e Expo
- Integração de sistemas
- APIs REST
- Gerenciamento de estado
- Navegação mobile
- Validações e UX

### Competências Socioemocionais
- Resolução de problemas
- Pensamento lógico
- Trabalho em equipe
- Comunicação técnica
- Autonomia no aprendizado
- Persistência

---

## 📞 Suporte

**Dúvidas Técnicas:**
- Durante as aulas: Pergunte ao professor
- Fora das aulas: Fórum da turma

**Materiais:**
- Todos os planos de aula: `material do curso/uc 02/part-04/plano de aula/`
- Código de exemplo: Repositório GitHub

---

## ✅ Checklist de Conclusão do Módulo

Ao final do módulo, você deve ter:

### Ambiente
- [ ] Node.js instalado
- [ ] Expo CLI instalado
- [ ] Projeto criado
- [ ] App rodando no dispositivo

### Componentes
- [ ] 10+ componentes reutilizáveis
- [ ] Todos estilizados
- [ ] Props documentadas

### Telas
- [ ] 12+ telas criadas
- [ ] Navegação funcionando
- [ ] Todas integradas

### Integração
- [ ] API configurada
- [ ] Login/Logout funcionando
- [ ] CRUD completo
- [ ] Validações implementadas

### Build
- [ ] APK gerado
- [ ] App testado em dispositivo
- [ ] Ícone e splash configurados

### Documentação
- [ ] README.md completo
- [ ] Código documentado
- [ ] Manuais criados
- [ ] BUILD.md criado

---

## 🏆 Projeto Final - MeetStranger Mobile

**Descrição:** Aplicativo mobile completo de chat anônimo

**Funcionalidades Implementadas:**
- ✅ Autenticação completa
- ✅ Navegação entre 12+ telas
- ✅ Integração com backend
- ✅ CRUD de usuários e categorias
- ✅ Chat (mock)
- ✅ Perfil e estatísticas
- ✅ Validações robustas
- ✅ UX otimizada
- ✅ Build gerado

**Tecnologias:** React Native, Expo, React Navigation, Axios, AsyncStorage

**Arquitetura:** Frontend Mobile → API REST → Banco de Dados

---

## 📝 Observações Finais

Este módulo é a culminação do projeto MeetStranger, integrando todo o conhecimento adquirido nas partes anteriores. O aplicativo mobile desenvolvido aqui consome a API criada na Part 03, que por sua vez acessa o banco de dados modelado na Part 02, tudo baseado no planejamento da UC 01.

**Parabéns por chegar até aqui! 🎉**

Você agora possui as habilidades necessárias para desenvolver aplicativos mobile completos, desde a concepção até a distribuição.

**Continue aprendendo e construindo! 🚀**

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0  
**Última atualização:** Janeiro 2024

---

## 🙏 Agradecimentos

- **SENAC** pela estrutura e suporte
- **Professores** pelo conhecimento compartilhado
- **Alunos** pela dedicação e empenho
- **Comunidade React Native** pelos recursos e documentação

---

**"O sucesso é a soma de pequenos esforços repetidos dia após dia."**

*Boa sorte em sua jornada como desenvolvedor mobile!* 🌟
