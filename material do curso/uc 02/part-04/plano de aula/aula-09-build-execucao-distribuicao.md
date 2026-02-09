# Aula 09 - Build, Execução e Distribuição do Aplicativo

**Carga Horária:** 4 horas  
**Modalidade:** Presencial  
**Competências:** Build, testes finais e preparação para distribuição

---

## 📋 Objetivos de Aprendizagem

Ao final desta aula, o aluno será capaz de:

- ✅ Gerar build do aplicativo React Native
- ✅ Executar app em dispositivo físico
- ✅ Compreender processo de publicação (APK/IPA)
- ✅ Configurar ícone e splash screen
- ✅ Preparar app para produção
- ✅ Realizar testes finais completos
- ✅ Documentar processo de build

---

## 📚 Conteúdo Programático

### 1. Build do Aplicativo
- Build de desenvolvimento vs produção
- Expo Build vs EAS Build
- Configuração de app.json
- Geração de APK/AAB

### 2. Execução em Dispositivo
- Instalação via USB
- Instalação via QR Code
- Testes em dispositivo real
- Debug em produção

### 3. Publicação
- Google Play Store (Android)
- Apple App Store (iOS)
- Requisitos de publicação
- Processo de review

### 4. Preparação Final
- Ícone e splash screen
- Versioning
- Otimizações
- Documentação

---

## 🎯 Metodologia SENAC

### 1️⃣ Retomada (30 min)

**Revisão Aula Anterior:**
- Validações e tratamento de erros
- Feedback visual
- UX/UI mobile

**Atividade de Aquecimento:**
```
Discussão:
- Como apps chegam na Play Store?
- Diferença entre app de teste e produção?
- O que é necessário para publicar um app?

Objetivo: Preparar para processo de build e distribuição
```

**Checkpoint:**
- Verificar app funcionando completamente
- Revisar todas as funcionalidades
- Identificar bugs pendentes

---

### 2️⃣ Apresentação (60 min)

#### 📖 Parte 1: Tipos de Build (15 min)

**Build de Desenvolvimento:**
- Usado durante desenvolvimento
- Expo Go
- Hot reload ativo
- Debug habilitado
- Não otimizado

**Build de Produção:**
- Versão final para usuários
- Standalone app
- Otimizado
- Debug desabilitado
- Assinado digitalmente

**Expo Build vs EAS Build:**

| Aspecto | Expo Build (Classic) | EAS Build |
|---------|---------------------|-----------|
| **Status** | Deprecated | Atual |
| **Configuração** | Simples | Mais controle |
| **Build na nuvem** | ✅ Sim | ✅ Sim |
| **Build local** | ❌ Não | ✅ Sim |
| **Custo** | Gratuito | Free tier limitado |

#### 📖 Parte 2: Configuração do app.json (20 min)

**Arquivo:** `app.json`

```json
{
  "expo": {
    "name": "MeetStranger",
    "slug": "meetstranger",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "light",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#6C63FF"
    },
    "assetBundlePatterns": [
      "**/*"
    ],
    "ios": {
      "supportsTablet": true,
      "bundleIdentifier": "com.senac.meetstranger",
      "buildNumber": "1.0.0"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#6C63FF"
      },
      "package": "com.senac.meetstranger",
      "versionCode": 1,
      "permissions": [
        "INTERNET"
      ]
    },
    "web": {
      "favicon": "./assets/favicon.png"
    },
    "extra": {
      "eas": {
        "projectId": "seu-project-id"
      }
    }
  }
}
```

**Campos Importantes:**

- `name`: Nome exibido no dispositivo
- `slug`: Identificador único
- `version`: Versão do app (1.0.0)
- `icon`: Ícone do app (1024x1024px)
- `splash`: Tela de carregamento
- `bundleIdentifier` (iOS): Identificador único
- `package` (Android): Nome do pacote
- `versionCode` (Android): Número da versão

#### 📖 Parte 3: Processo de Build (15 min)

**Instalar EAS CLI:**
```bash
npm install -g eas-cli
```

**Login no Expo:**
```bash
eas login
```

**Configurar projeto:**
```bash
eas build:configure
```

**Gerar build Android (APK):**
```bash
eas build --platform android --profile preview
```

**Gerar build iOS:**
```bash
eas build --platform ios --profile preview
```

**Arquivo:** `eas.json`

```json
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal"
    },
    "preview": {
      "distribution": "internal",
      "android": {
        "buildType": "apk"
      }
    },
    "production": {
      "android": {
        "buildType": "app-bundle"
      }
    }
  }
}
```

#### 📖 Parte 4: Publicação (10 min)

**Google Play Store (Android):**

1. Criar conta de desenvolvedor ($25 único)
2. Gerar build de produção (AAB)
3. Criar app no Play Console
4. Upload do AAB
5. Preencher informações (descrição, screenshots)
6. Enviar para review
7. Aguardar aprovação (1-3 dias)

**Apple App Store (iOS):**

1. Conta Apple Developer ($99/ano)
2. Certificados e provisioning profiles
3. Gerar build de produção (IPA)
4. Upload via App Store Connect
5. Preencher informações
6. Enviar para review
7. Aguardar aprovação (1-7 dias)

**Requisitos Comuns:**

- Ícone do app
- Screenshots (várias resoluções)
- Descrição do app
- Política de privacidade
- Termos de uso
- Categoria
- Classificação etária

---

### 3️⃣ Prática Guiada (90 min)

#### 💻 Exercício 1: Configurar Ícone e Splash Screen (25 min)

**Criar ícone:**
- Tamanho: 1024x1024px
- Formato: PNG
- Sem transparência
- Design simples e reconhecível

**Ferramenta online:** https://www.appicon.co/

**Criar splash screen:**
- Tamanho: 1242x2436px (ou maior)
- Formato: PNG
- Pode ter transparência
- Logo centralizado

**Atualizar:** `app.json`

```json
{
  "expo": {
    "icon": "./assets/icon.png",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#6C63FF"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#6C63FF"
      }
    }
  }
}
```

**Testar:**
```bash
expo start
```

#### 💻 Exercício 2: Preparar para Produção (30 min)

**1. Remover console.log:**

```javascript
// Criar arquivo: src/utils/logger.js
const isDevelopment = __DEV__;

export const logger = {
  log: (...args) => {
    if (isDevelopment) {
      console.log(...args);
    }
  },
  error: (...args) => {
    if (isDevelopment) {
      console.error(...args);
    }
  },
  warn: (...args) => {
    if (isDevelopment) {
      console.warn(...args);
    }
  }
};

// Usar no código
import { logger } from './utils/logger';
logger.log('Debug info');
```

**2. Configurar variáveis de ambiente:**

```bash
npm install react-native-dotenv
```

**Criar:** `.env`

```
API_URL=http://localhost:3000
API_TIMEOUT=10000
```

**Criar:** `.env.production`

```
API_URL=https://api.meetstranger.com
API_TIMEOUT=10000
```

**Atualizar:** `src/services/api.js`

```javascript
import { API_URL, API_TIMEOUT } from '@env';

const api = axios.create({
  baseURL: API_URL,
  timeout: parseInt(API_TIMEOUT),
});
```

**3. Atualizar versão:**

```json
// app.json
{
  "expo": {
    "version": "1.0.0",
    "android": {
      "versionCode": 1
    },
    "ios": {
      "buildNumber": "1.0.0"
    }
  }
}
```

#### 💻 Exercício 3: Gerar Build de Preview (35 min)

**1. Instalar EAS CLI:**
```bash
npm install -g eas-cli
```

**2. Login:**
```bash
eas login
```

**3. Configurar projeto:**
```bash
eas build:configure
```

**4. Gerar build Android (APK):**
```bash
eas build --platform android --profile preview
```

**Aguardar build:**
- Build é feito na nuvem
- Leva 10-20 minutos
- Recebe link para download

**5. Baixar e instalar APK:**
- Baixar APK do link fornecido
- Transferir para dispositivo Android
- Habilitar "Instalar apps desconhecidos"
- Instalar APK
- Testar app

**Alternativa - Build local (mais rápido):**
```bash
# Instalar Android Studio primeiro
eas build --platform android --profile preview --local
```

---

### 4️⃣ Prática Autônoma (60 min)

#### 🎯 Desafio 1: Testes Finais Completos (30 min)

**Checklist de Testes:**

**Funcionalidades:**
- [ ] Login funciona
- [ ] Cadastro funciona
- [ ] Logout funciona
- [ ] Listar categorias funciona
- [ ] Selecionar categoria funciona
- [ ] Chat funciona (mock)
- [ ] Perfil funciona
- [ ] Editar perfil funciona
- [ ] Gerenciar usuários funciona (CRUD)

**Validações:**
- [ ] Email inválido é rejeitado
- [ ] Senha curta é rejeitada
- [ ] Username duplicado é rejeitado
- [ ] Campos obrigatórios validados

**Navegação:**
- [ ] Todas as telas acessíveis
- [ ] Botão voltar funciona
- [ ] Navegação fluida

**UI/UX:**
- [ ] Loading aparece quando necessário
- [ ] Mensagens de erro claras
- [ ] Feedback visual adequado
- [ ] Layout responsivo

**Performance:**
- [ ] App não trava
- [ ] Listas rolam suavemente
- [ ] Imagens carregam rápido

**Documentar bugs encontrados:**
```
Bug #1: [Descrição]
Passos para reproduzir: [...]
Severidade: Alta/Média/Baixa
Status: Pendente/Corrigido
```

#### 🎯 Desafio 2: Criar Documentação de Build (30 min)

**Criar:** `BUILD.md`

```markdown
# Guia de Build - MeetStranger

## Pré-requisitos

- Node.js 14+
- Expo CLI
- EAS CLI
- Conta Expo

## Configuração

1. Instalar dependências:
```bash
npm install
```

2. Configurar variáveis de ambiente:
```bash
cp .env.example .env
```

3. Atualizar API_URL no .env

## Build de Desenvolvimento

```bash
expo start
```

## Build de Preview (APK)

```bash
eas build --platform android --profile preview
```

## Build de Produção

```bash
eas build --platform android --profile production
```

## Instalação no Dispositivo

1. Baixar APK do link fornecido
2. Transferir para dispositivo
3. Habilitar instalação de apps desconhecidos
4. Instalar APK

## Troubleshooting

**Erro: "Build failed"**
- Verificar app.json
- Verificar eas.json
- Verificar logs do build

**Erro: "App crashes on startup"**
- Verificar variáveis de ambiente
- Verificar API_URL
- Verificar logs do dispositivo

## Versioning

- Versão atual: 1.0.0
- Atualizar em: app.json (version, versionCode, buildNumber)

## Contato

Equipe MeetStranger - SENAC
```

**Checklist:**
- [ ] Testes completos realizados
- [ ] Bugs documentados
- [ ] BUILD.md criado
- [ ] APK gerado e testado

---

### 5️⃣ Síntese (20 min)

#### 📝 Revisão dos Conceitos

**Perguntas:**

1. **Diferença entre build de dev e produção?**
   - Dev: debug ativo / Produção: otimizado

2. **O que é APK?**
   - Android Package - arquivo instalável Android

3. **Por que versionar o app?**
   - Controle de atualizações, rastreamento

4. **O que é necessário para publicar?**
   - Build de produção, conta de desenvolvedor, assets

#### 🎯 Processo de Build

```
1. Configurar app.json
2. Criar ícone e splash
3. Preparar para produção
4. Gerar build (EAS)
5. Testar APK
6. Corrigir bugs
7. Publicar (opcional)
```

#### ✅ Checklist do Aluno

**Eu sei:**
- [ ] Configurar app.json
- [ ] Criar ícone e splash screen
- [ ] Gerar build com EAS
- [ ] Instalar APK em dispositivo
- [ ] Testar app em produção
- [ ] Documentar processo de build
- [ ] Preparar app para publicação

#### 📚 Projeto Completo

**Conquistas:**
- ✅ Frontend mobile completo
- ✅ Integração com backend
- ✅ CRUD funcionando
- ✅ Validações implementadas
- ✅ UX otimizada
- ✅ Build gerado
- ✅ App testado

**Próximos Passos (Opcional):**
- Publicar na Play Store
- Adicionar mais funcionalidades
- Implementar chat real (WebSocket)
- Adicionar notificações push
- Melhorar design

---

## 📊 Avaliação

### Critérios (Peso: 10% da UC 02 Part 04)

| Critério | Peso | Descrição |
|----------|------|-----------|
| **Configuração** | 25% | app.json configurado corretamente |
| **Build** | 30% | APK gerado com sucesso |
| **Testes** | 30% | Testes completos realizados |
| **Documentação** | 15% | BUILD.md criado |

---

## 🎓 Dicas para o Professor

### Antes da Aula
- [ ] Criar conta Expo
- [ ] Testar processo de build
- [ ] Preparar ícone e splash de exemplo
- [ ] Ter APK pronto para demonstração

### Pontos de Atenção
- ⚠️ Build pode demorar (10-20 min)
- ⚠️ Problemas de configuração no app.json
- ⚠️ Dispositivos sem modo desenvolvedor
- ⚠️ Firewall bloqueando download

### Troubleshooting

**Problema:** "Build failed"
**Solução:** Verificar logs, app.json, eas.json

**Problema:** "App crashes on startup"
**Solução:** Verificar variáveis de ambiente, API_URL

**Problema:** "Cannot install APK"
**Solução:** Habilitar instalação de apps desconhecidos

---

## 📎 Recursos Adicionais

- [EAS Build Docs](https://docs.expo.dev/build/introduction/)
- [App Store Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- [Play Store Guidelines](https://play.google.com/console/about/guides/releasewithconfidence/)

### Encerramento do Módulo

**Parabéns! 🎉**

Você completou o módulo de Frontend Mobile React Native!

**O que você aprendeu:**
- React Native e Expo
- Componentes e navegação
- Integração com API REST
- CRUD completo
- Validações e UX
- Build e distribuição

**Projeto MeetStranger:**
- ✅ App mobile funcional
- ✅ Integrado com backend
- ✅ Pronto para uso

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0  
**Última atualização:** Janeiro 2024
