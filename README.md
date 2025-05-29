
# LiftHub - Plataforma de Conexão entre Instrutores e Alunos

<img src="./images/logo_lifthub - Copia.jpg" align="right" width="100px">

LiftHub é uma plataforma completa que conecta personal trainers/nutricionistas com seus alunos, permitindo o acompanhamento de avaliações físicas, registros semanais, upload de fotos de progresso e comunicação direta entre aluno e instrutor.

## Tecnologias Utilizadas

- **Frontend**: React com TypeScript, Styled Components
- **Backend**: Node.js com Express
- **Banco de Dados**: PostgreSQL
- **Autenticação**: JWT (JSON Web Tokens)

## Estrutura do Projeto

```
/lifthub-project
  /frontend
    /src
      /components     # Componentes reutilizáveis
      /pages          # Páginas da aplicação
      /services       # Serviços de API
      /styles         # Estilos globais
    package.json      # Dependências do frontend

  /backend
    /src
      /controllers    # Controladores da API
      /models         # Modelos de dados
      /routes         # Rotas da API
      /middlewares    # Middlewares (auth, error handling)
    server.js         # Arquivo principal do servidor
    package.json      # Dependências do backend

  /database
    schema.sql        # Estrutura do banco de dados
    seed.sql          # Dados iniciais para testes
    connection.js     # Configuração de conexão com o banco

  .env.example        # Exemplo de variáveis de ambiente
  README.md           # Documentação do projeto
```

## Funcionalidades Principais

1. **Landing Page**
   - Página inicial com informações sobre a plataforma
   - Acesso às páginas de login e cadastro

2. **Autenticação**
   - Login e cadastro para instrutor
   - Login e cadastro para aluno
   - Validação de sessão com token (JWT)
   - Rotas protegidas por tipo de usuário

3. **Dashboard do Instrutor**
   - Listar alunos vinculados
   - Adicionar novo aluno
   - Vincular aluno a partir do e-mail
   - Visualizar ficha de anamnese de cada aluno
   - Acompanhar progresso com fotos e respostas semanais
   - Receber notificações de novos envios
   - Chat com os alunos

4. **Dashboard do Aluno**
   - Responder avaliação semanal (texto + imagem)
   - Consultar ficha de anamnese
   - Ver recomendações ou mensagens do instrutor
   - Editar perfil

5. **Anamnese**
   - Questionário inicial com múltiplos campos
   - Envio único, editável somente pelo instrutor

6. **Respostas Semanais**
   - Envio de texto
   - Upload de fotos de progresso
   - Histórico das respostas anteriores

7. **Chat**
   - Comunicação direta entre instrutor e aluno
   - Notificações de novas mensagens

## Pré-requisitos

- Node.js (v14 ou superior)
- PostgreSQL (v12 ou superior)
- npm ou yarn

## Instalação e Configuração

### 1. Clone o repositório

```bash
git clone <url-do-repositorio>
cd lifthub-project
```

### 2. Configuração do Banco de Dados

1. Instale o PostgreSQL se ainda não tiver instalado:
   ```bash
   # Ubuntu
   sudo apt update
   sudo apt install postgresql postgresql-contrib
   
   # macOS (usando Homebrew)
   brew install postgresql
   
   # Windows
   # Faça o download e instale a partir de https://www.postgresql.org/download/windows/
   ```

2. Inicie o serviço do PostgreSQL:
   ```bash
   # Ubuntu
   sudo service postgresql start
   
   # macOS
   brew services start postgresql
   
   # Windows
   # O serviço deve iniciar automaticamente após a instalação
   ```

3. Crie um banco de dados para o projeto:
   ```bash
   # Acesse o PostgreSQL como usuário postgres
   sudo -u postgres psql
   
   # No prompt do PostgreSQL, crie o banco de dados
   CREATE DATABASE lifthub;
   
   # Crie um usuário (opcional, pode usar o usuário postgres padrão)
   CREATE USER lifthub_user WITH ENCRYPTED PASSWORD 'sua_senha';
   
   # Conceda privilégios ao usuário
   GRANT ALL PRIVILEGES ON DATABASE lifthub TO lifthub_user;
   
   # Saia do prompt do PostgreSQL
   \q
   ```

4. Execute os scripts SQL para criar as tabelas:
   ```bash
   # Navegue até a pasta do projeto
   cd lifthub-project
   
   # Execute o script de schema
   psql -U postgres -d lifthub -f database/schema.sql
   
   # Execute o script de seed para dados iniciais (opcional)
   psql -U postgres -d lifthub -f database/seed.sql
   ```

### 3. Configuração do Backend

1. Navegue até a pasta do backend:
   ```bash
   cd backend
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

3. Crie um arquivo `.env` baseado no `.env.example`:
   ```bash
   cp ../.env.example .env
   ```

4. Edite o arquivo `.env` com suas configurações locais:
   ```
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=lifthub
   DB_USER=postgres  # ou o usuário que você criou
   DB_PASSWORD=sua_senha
   
   JWT_SECRET=sua_chave_secreta_para_jwt
   JWT_EXPIRES_IN=24h
   
   PORT=3001
   NODE_ENV=development
   
   UPLOAD_DIR=uploads
   MAX_FILE_SIZE=5242880
   ALLOWED_FILE_TYPES=image/jpeg,image/png,image/jpg
   
   FRONTEND_URL=http://localhost:3000
   ```

5. Crie a pasta de uploads:
   ```bash
   mkdir -p uploads
   ```

6. Inicie o servidor:
   ```bash
   # Modo de desenvolvimento com hot-reload
   npm run dev
   
   # OU modo de produção
   npm start
   ```

7. Verifique se o servidor está funcionando acessando:
   ```
   http://localhost:3001/api/health
   ```

### 4. Configuração do Frontend

1. Navegue até a pasta do frontend:
   ```bash
   cd ../frontend
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

3. Crie um arquivo `.env` para configurações do frontend:
   ```bash
   touch .env
   ```

4. Adicione a URL da API ao arquivo `.env`:
   ```
   REACT_APP_API_URL=http://localhost:3001/api
   ```

5. Inicie o servidor de desenvolvimento:
   ```bash
   npm start
   ```

6. O frontend estará disponível em:
   ```
   http://localhost:3000
   ```

## Uso da Aplicação

1. **Acesso à Landing Page**
   - Acesse `http://localhost:3000` para ver a landing page
   - Clique em "Entrar" para acessar a página de login
   - Clique em "Cadastre-se" para criar uma nova conta

2. **Login**
   - Use as credenciais de teste para instrutores:
     - Email: carlos@lifthub.com
     - Senha: senha123
   - Ou para alunos:
     - Email: joao@email.com
     - Senha: senha123

3. **Navegação como Instrutor**
   - Dashboard: Visão geral de alunos e atividades recentes
   - Alunos: Lista de alunos vinculados, com opção de adicionar novos
   - Chat: Comunicação com alunos
   - Perfil: Informações e configurações do instrutor

4. **Navegação como Aluno**
   - Dashboard: Visão geral de progresso e treinos
   - Resposta Semanal: Formulário para envio de feedback e fotos
   - Anamnese: Visualização do questionário de anamnese
   - Chat: Comunicação com o instrutor
   - Perfil: Informações e configurações do aluno

## Solução de Problemas Comuns

### Problemas de Conexão com o Banco de Dados

- **Erro**: "ECONNREFUSED" ou "Connection refused"
  - **Solução**: Verifique se o PostgreSQL está em execução e se as credenciais no arquivo `.env` estão corretas.

- **Erro**: "Role 'postgres' does not exist"
  - **Solução**: Substitua 'postgres' pelo nome de usuário correto do PostgreSQL no seu sistema.

### Problemas no Backend

- **Erro**: "Port 3001 is already in use"
  - **Solução**: Altere a porta no arquivo `.env` ou encerre o processo que está usando a porta 3001.

- **Erro**: "JWT_SECRET is not defined"
  - **Solução**: Certifique-se de que o arquivo `.env` foi criado corretamente com todas as variáveis necessárias.

### Problemas no Frontend

- **Erro**: "Failed to fetch" nas chamadas de API
  - **Solução**: Verifique se o backend está em execução e se a URL da API está configurada corretamente no arquivo `.env` do frontend.

- **Erro**: "TypeError: Cannot read property 'X' of undefined"
  - **Solução**: Verifique se os dados estão sendo carregados corretamente antes de tentar acessar suas propriedades.

## Scripts Disponíveis

### Backend

- `npm start`: Inicia o servidor em modo de produção
- `npm run dev`: Inicia o servidor em modo de desenvolvimento com hot-reload
- `npm test`: Executa os testes

### Frontend

- `npm start`: Inicia o servidor de desenvolvimento
- `npm run build`: Compila o aplicativo para produção
- `npm test`: Executa os testes
- `npm run eject`: Ejeta a configuração do Create React App

## Contribuição

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Faça commit das suas alterações (`git commit -m 'Adiciona nova feature'`)
4. Faça push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo LICENSE para mais detalhes.

## Contato

Para dúvidas ou sugestões, entre em contato com a equipe do LiftHub.

## Links

》 [Mapa de Ideação 😎](https://startunicesusc.txm-methods.com/347e49b8-a856-44b0-a194-077ad60173a6)

》 [Protótipo Figma 👾](https://www.figma.com/proto/qtRC0HdKQcYmJhlJZn0Otj/lift-hub?node-id=214-91&starting-point-node-id=214%3A91)

》 [Kanban 📋](https://trello.com/invite/b/6709a637fb0f7a31c429fc9f/ATTI77b6d9d402c94e346cb5c62130f7fc8fBF60924C/kanban-lift-hub)

》 [MoSCoW 🌎](<https://www.figma.com/board/bxt7wZ2Cbit54gXNgEPiwp/MoSCoW-Matrix-(Community)?node-id=8-49&t=MqmXKghYDrk5bdsN-1>)
