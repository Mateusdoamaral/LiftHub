# Análise de Atores e Casos de Uso - LiftHub

## Atores Principais

1.  **Aluno:** Usuário final que busca acompanhamento físico e nutricional.
2.  **Instrutor:** Profissional que acompanha e orienta os alunos.

## Casos de Uso

### Casos de Uso Comuns (Aluno e Instrutor)

*   **UC01: Autenticar:**
    *   Registrar nova conta (como Aluno ou Instrutor).
    *   Fazer login com email e senha.
    *   Fazer logout.
*   **UC02: Gerenciar Perfil:**
    *   Visualizar dados do perfil (nome, email, foto).
    *   Atualizar dados do perfil (nome, foto, dados específicos de Aluno/Instrutor como bio, especialidade, data de nascimento, telefone).
    *   Atualizar senha.
*   **UC03: Usar Chat:**
    *   Visualizar lista de conversas.
    *   Abrir uma conversa específica.
    *   Enviar mensagem de texto.
    *   Receber mensagem de texto.
    *   Marcar mensagens como lidas (implicitamente ao abrir a conversa).

### Casos de Uso Específicos do Aluno

*   **UC04: Gerenciar Anamnese:**
    *   Preencher formulário de anamnese pela primeira vez.
    *   Visualizar anamnese preenchida.
    *   Atualizar formulário de anamnese.
*   **UC05: Gerenciar Respostas Semanais:**
    *   Criar e enviar resposta semanal (texto, sentimento, dificuldades, nutrição).
    *   Adicionar imagens de progresso à resposta semanal.
    *   Visualizar histórico de respostas semanais e imagens.
*   **UC06: Visualizar Instrutores:**
    *   Ver lista de instrutores vinculados.

### Casos de Uso Específicos do Instrutor

*   **UC07: Gerenciar Alunos:**
    *   Visualizar lista de alunos vinculados (ativos, pendentes, inativos).
    *   Buscar aluno por email para vincular.
    *   Vincular novo aluno (enviar convite ou ativar vínculo).
    *   Desvincular aluno (marcar como inativo).
*   **UC08: Acompanhar Aluno:**
    *   Visualizar perfil detalhado do aluno.
    *   Visualizar anamnese do aluno.
    *   Visualizar histórico de respostas semanais e imagens de progresso do aluno.


