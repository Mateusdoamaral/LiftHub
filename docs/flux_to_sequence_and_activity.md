# Análise de Fluxos para Diagramas de Sequência e Atividade - LiftHub

Baseado nos casos de uso e na estrutura da aplicação, selecionamos os seguintes fluxos principais para detalhamento nos diagramas de sequência e atividade:

1.  **Fluxo de Autenticação (Login):**
    *   **Objetivo:** Permitir que um usuário (Aluno ou Instrutor) acesse o sistema.
    *   **Passos Principais:**
        1.  Usuário acessa a página de Login no Frontend.
        2.  Usuário insere email e senha.
        3.  Frontend envia as credenciais para a API Backend (AuthController).
        4.  AuthController busca o usuário pelo email (UserModel).
        5.  UserModel consulta o banco de dados.
        6.  Se o usuário existe, AuthController verifica a senha (UserModel/bcrypt).
        7.  Se a senha está correta, AuthController gera um token JWT.
        8.  Backend retorna o token e dados do usuário para o Frontend.
        9.  Frontend armazena o token e redireciona o usuário para o Dashboard apropriado.
    *   **Diagramas:** Sequência (detalhando interações), Atividade (mostrando o fluxo geral).

2.  **Fluxo de Envio de Resposta Semanal (Aluno):**
    *   **Objetivo:** Permitir que um Aluno envie seu feedback semanal.
    *   **Passos Principais:**
        1.  Aluno acessa a página de Resposta Semanal no Frontend.
        2.  Aluno preenche os campos (texto, sentimento, etc.) e opcionalmente anexa imagens.
        3.  Frontend envia os dados (e imagens, se houver) para a API Backend (StudentController).
        4.  StudentController valida os dados.
        5.  StudentController chama o StudentModel para criar a resposta semanal.
        6.  StudentModel insere os dados na tabela `weekly_responses`.
        7.  Se houver imagens, StudentController (ou um serviço dedicado) faz o upload para o servidor e obtém os caminhos.
        8.  StudentController chama o StudentModel para associar as imagens à resposta criada (tabela `progress_images`).
        9.  Backend retorna confirmação de sucesso para o Frontend.
        10. Frontend exibe mensagem de sucesso ao Aluno.
    *   **Diagramas:** Sequência (detalhando interações entre Frontend, Backend e Banco), Atividade (mostrando o fluxo do aluno).

3.  **Fluxo de Envio de Mensagem no Chat:**
    *   **Objetivo:** Permitir que Aluno ou Instrutor envie uma mensagem em uma conversa existente.
    *   **Passos Principais:**
        1.  Usuário (Aluno ou Instrutor) abre uma conversa na página de Chat do Frontend.
        2.  Usuário digita a mensagem e clica em enviar.
        3.  Frontend envia a mensagem (texto, ID da conversa, ID do remetente) para a API Backend (ChatController).
        4.  ChatController valida os dados.
        5.  ChatController chama o ChatModel para salvar a mensagem.
        6.  ChatModel insere a mensagem na tabela `messages`, associada à `conversation_id`.
        7.  (Opcional/Ideal: Backend envia a nova mensagem via WebSocket para o outro participante da conversa).
        8.  Backend retorna confirmação de sucesso para o Frontend.
        9.  Frontend atualiza a interface do chat exibindo a nova mensagem enviada.
    *   **Diagramas:** Sequência (detalhando interações), Atividade (mostrando o fluxo do usuário no chat).

Estes fluxos servirão como base para a criação dos diagramas de Sequência e Atividade.

