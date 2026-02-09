# UC 02 - Part 03: Desenvolvimento Backend com Node.js e Express

**Carga Horária Total:** 40 horas  
**Modalidade:** Presencial  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo

---

## 📋 Visão Geral

Este módulo aborda o desenvolvimento completo do backend da aplicação MeetStranger, desde os fundamentos do Node.js até a implementação de APIs REST seguras e documentadas, integradas ao banco de dados SQLite.

---

## 🎯 Competências Desenvolvidas

Ao concluir este módulo, o aluno será capaz de:

- ✅ Desenvolver APIs REST com Node.js e Express
- ✅ Implementar arquitetura em camadas (MVC adaptado)
- ✅ Integrar backend com banco de dados relacional
- ✅ Aplicar operações CRUD completas
- ✅ Implementar tratamento de erros centralizado
- ✅ Aplicar segurança (JWT, bcrypt, CORS)
- ✅ Documentar APIs profissionalmente
- ✅ Utilizar controle de versão com Git

---

## 📚 Estrutura do Módulo

### Aula 01 - Fundamentos Backend e Node.js (4h)
**Conteúdo:**
- Arquitetura cliente-servidor
- Instalação e configuração do Node.js
- NPM e gerenciamento de pacotes
- Primeiro projeto com Express
- Hello World API

**Entregáveis:**
- Servidor Express básico funcionando
- Primeira rota GET implementada

---

### Aula 02 - Express e Estruturação de Projeto (4h)
**Conteúdo:**
- Framework Express em profundidade
- Middlewares (conceito e uso)
- Estrutura profissional de projeto
- Separação de responsabilidades (Routes, Controllers, Services)
- CRUD com dados mockados

**Entregáveis:**
- Projeto estruturado em camadas
- UserController e UserService com mock data
- Rotas REST organizadas

---

### Aula 03 - APIs REST e Métodos HTTP (4h)
**Conteúdo:**
- Princípios REST (stateless, uniform interface)
- Métodos HTTP (GET, POST, PUT, DELETE)
- Códigos de status HTTP (200, 201, 204, 400, 404, 409, 500)
- Estrutura de requisição/resposta
- Query parameters e route parameters

**Entregáveis:**
- UserController com REST completo
- CategoriaController implementado
- SalaController (desafio)
- 17+ testes de API realizados

---

### Aula 04 - Análise de Requisitos e Modelagem Backend (4h)
**Conteúdo:**
- Análise de requisitos funcionais
- Diagrama de caso de uso
- Diagrama de classes (entidades)
- Organização de rotas por domínio
- Definição completa da API MeetStranger

**Entregáveis:**
- 15+ endpoints definidos
- Documentação de requisitos
- MatchingController com lógica de fila
- API_DOCUMENTATION.md

---

### Aula 05 - Integração com Banco de Dados - CRUD Parte 1 (4h)
**Conteúdo:**
- Conexão Node.js + SQLite3
- Arquitetura em 3 camadas (Controller → Service → Repository)
- Operações CREATE (INSERT)
- Operações READ (SELECT)
- Prepared statements (SQL injection prevention)

**Entregáveis:**
- UserRepository com Promises
- CategoriaRepository completo
- Dados persistindo no banco
- 10 testes de CREATE/READ

---

### Aula 06 - Integração com Banco de Dados - CRUD Parte 2 (4h)
**Conteúdo:**
- Operações UPDATE
- Operações DELETE
- Regras de negócio complexas
- Integridade referencial
- Hard delete vs Soft delete

**Entregáveis:**
- CRUD completo para Usuários e Categorias
- Validação de dependências
- UPDATE dinâmico
- 17 testes completos de CRUD

---

### Aula 07-08 - Tratamento de Erros, Depuração e Qualidade (8h)
**Conteúdo:**
- Middleware de erro centralizado
- Refatoração para async/await
- Debugging com VS Code (breakpoints)
- Logging estruturado
- asyncHandler para rotas
- Boas práticas de código

**Entregáveis:**
- AppError class implementada
- Todo código refatorado para async/await
- Middleware de validação
- errorMiddleware funcionando

---

### Aula 09-10 - Segurança, Versionamento e Documentação (8h)
**Conteúdo:**
- Criptografia de senhas (bcrypt)
- Autenticação JWT
- Middleware de autenticação
- CORS configurado
- Variáveis de ambiente (.env)
- Git básico (init, commit, branches)
- Documentação Swagger/OpenAPI
- README.md profissional

**Entregáveis:**
- Sistema de autenticação completo
- Rotas protegidas
- Documentação Swagger interativa
- README.md do projeto
- Repositório Git configurado

---

## 🗂️ Estrutura Final do Projeto

```
meetstranger-backend/
├── src/
│   ├── config/
│   │   ├── database.js
│   │   └── swagger.js
│   ├── controllers/
│   │   ├── AuthController.js
│   │   ├── UserController.js
│   │   ├── CategoriaController.js
│   │   ├── MatchingController.js
│   │   └── SalaController.js
│   ├── services/
│   │   ├── AuthService.js
│   │   ├── UserService.js
│   │   ├── CategoriaService.js
│   │   ├── MatchingService.js
│   │   └── SalaService.js
│   ├── repositories/
│   │   ├── UserRepository.js
│   │   ├── CategoriaRepository.js
│   │   ├── MatchingRepository.js
│   │   └── SalaRepository.js
│   ├── middleware/
│   │   ├── authMiddleware.js
│   │   ├── errorMiddleware.js
│   │   └── validationMiddleware.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── userRoutes.js
│   │   ├── categoriaRoutes.js
│   │   ├── matchingRoutes.js
│   │   └── salaRoutes.js
│   ├── app.js
│   └── server.js
├── database/
│   ├── init.js
│   └── meetstranger.db
├── .env
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Finalidade |
|------------|--------|------------|
| Node.js | 14+ | Runtime JavaScript |
| Express | 4.x | Framework web |
| SQLite3 | 5.x | Banco de dados |
| JWT | 9.x | Autenticação |
| Bcrypt | 5.x | Criptografia de senhas |
| CORS | 2.x | Política de segurança |
| Dotenv | 16.x | Variáveis de ambiente |
| Swagger UI | 5.x | Documentação interativa |

---

## 📊 Sistema de Avaliação

### Distribuição de Notas

| Aula | Peso | Tipo de Avaliação |
|------|------|-------------------|
| Aula 01 | 10% | Formativa + Prática |
| Aula 02 | 10% | Formativa + Prática |
| Aula 03 | 15% | Somativa (SalaController + Testes) |
| Aula 04 | 15% | Somativa (Documentação + MatchingController) |
| Aula 05 | 20% | Somativa (CategoriaRepository + Testes) |
| Aula 06 | 20% | Somativa (CRUD Completo + Testes) |
| Aula 07-08 | 15% | Somativa (Refatoração + Debugging) |
| Aula 09-10 | 15% | Somativa (Autenticação + Documentação) |
| **Total** | **120%** | *Nota máxima: 100%* |

### Critérios de Avaliação

**Técnicos (60%):**
- Código funcional e sem erros
- Arquitetura em camadas implementada
- CRUD completo funcionando
- Segurança aplicada (JWT, bcrypt)
- Documentação técnica completa

**Boas Práticas (40%):**
- Nomenclatura clara e consistente
- Tratamento de erros adequado
- Validações implementadas
- Código limpo e organizado
- Commits semânticos no Git

---

## 🎯 Endpoints da API MeetStranger

### Autenticação
- `POST /auth/login` - Fazer login

### Usuários
- `POST /usuarios` - Criar usuário (público)
- `GET /usuarios` - Listar usuários (protegido)
- `GET /usuarios/:id` - Buscar usuário (protegido)
- `PUT /usuarios/:id` - Atualizar usuário (protegido)
- `DELETE /usuarios/:id` - Deletar usuário (protegido)

### Categorias
- `GET /categorias` - Listar categorias (público)
- `GET /categorias/:id` - Buscar categoria (público)
- `POST /categorias` - Criar categoria (protegido)
- `PUT /categorias/:id` - Atualizar categoria (protegido)
- `DELETE /categorias/:id` - Deletar categoria (protegido)

### Matching
- `POST /matching/entrar` - Entrar na fila (protegido)
- `DELETE /matching/sair` - Sair da fila (protegido)
- `GET /matching/fila` - Ver fila (protegido)
- `GET /matching/posicao` - Ver posição (protegido)

### Salas
- `GET /salas` - Minhas salas (protegido)
- `GET /salas/:id` - Buscar sala (protegido)
- `POST /salas/:id/encerrar` - Encerrar sala (protegido)

---

## 📈 Estatísticas do Módulo

- **Total de Aulas:** 10 sessões (40 horas)
- **Linhas de Código:** ~2.000 linhas
- **Arquivos Criados:** 25+ arquivos
- **Endpoints Implementados:** 15+
- **Testes Realizados:** 50+
- **Conceitos Abordados:** 40+

---

## 🔗 Conexão com Outros Módulos

### ⬅️ Pré-requisitos (Part 01 e 02)
- **Part 01 - Lógica de Programação:** Algoritmos, estruturas de dados, pseudocódigo
- **Part 02 - Banco de Dados:** SQL, modelagem, CRUD, relacionamentos

### ➡️ Próximo Módulo (Part 04)
- **Part 04 - Frontend Mobile:** React Native, integração com API, interface do usuário

---

## 💡 Dicas para o Aluno

### Para Ter Sucesso
1. ✅ Pratique todos os exercícios propostos
2. ✅ Teste cada endpoint criado
3. ✅ Leia a documentação oficial do Express
4. ✅ Use o debugger do VS Code
5. ✅ Faça commits frequentes no Git
6. ✅ Documente seu código
7. ✅ Tire dúvidas durante as aulas

### Recursos Adicionais
- [Documentação Express](https://expressjs.com/)
- [Node.js Docs](https://nodejs.org/docs/)
- [SQLite Tutorial](https://www.sqlitetutorial.net/)
- [JWT.io](https://jwt.io/)
- [REST API Tutorial](https://restfulapi.net/)

---

## 🎓 Competências SENAC Desenvolvidas

### Competências Técnicas
- Desenvolvimento de APIs REST
- Integração com banco de dados
- Implementação de segurança
- Controle de versão
- Documentação técnica

### Competências Socioemocionais
- Resolução de problemas
- Pensamento analítico
- Trabalho em equipe
- Comunicação técnica
- Autonomia no aprendizado

---

## 📞 Suporte

**Dúvidas Técnicas:**
- Durante as aulas: Pergunte ao professor
- Fora das aulas: Fórum da turma

**Materiais:**
- Todos os planos de aula estão em: `material do curso/uc 02/part-03/plano de aula/`
- Código de exemplo disponível no repositório

---

## ✅ Checklist de Conclusão do Módulo

Ao final do módulo, você deve ter:

- [ ] Servidor Express funcionando
- [ ] Banco de dados SQLite configurado
- [ ] 5 tabelas criadas (usuarios, categorias, salas, fila_matching, estatisticas_usuario)
- [ ] 15+ endpoints REST implementados
- [ ] Sistema de autenticação JWT funcionando
- [ ] Senhas criptografadas com bcrypt
- [ ] Tratamento de erros centralizado
- [ ] Código refatorado para async/await
- [ ] Documentação Swagger completa
- [ ] README.md profissional
- [ ] Repositório Git configurado
- [ ] Todos os testes realizados com sucesso

---

## 🏆 Projeto Final - MeetStranger Backend

**Descrição:** API REST completa para aplicativo de chat anônimo

**Funcionalidades Implementadas:**
- ✅ Cadastro e autenticação de usuários
- ✅ Gerenciamento de categorias
- ✅ Sistema de matching por categoria
- ✅ Criação e gerenciamento de salas
- ✅ Estatísticas de uso
- ✅ Segurança com JWT
- ✅ Documentação interativa

**Tecnologias:** Node.js, Express, SQLite, JWT, Bcrypt, Swagger

**Arquitetura:** REST API com 3 camadas (Controller → Service → Repository)

---

**Desenvolvido para:** Curso Técnico em Desenvolvimento de Sistemas - SENAC  
**Projeto:** MeetStranger - Aplicativo de Chat Anônimo  
**Versão:** 1.0  
**Última atualização:** Janeiro 2024

---

## 📝 Observações Finais

Este módulo é fundamental para o desenvolvimento do projeto MeetStranger. O backend criado aqui será consumido pelo frontend mobile (Part 04) e pelo frontend web (futuro). Certifique-se de compreender bem cada conceito antes de avançar.

**Boa sorte e bons estudos! 🚀**
