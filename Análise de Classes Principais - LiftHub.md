# Análise de Classes Principais - LiftHub

Baseado na análise do schema do banco de dados e dos modelos do backend, as seguintes classes principais foram identificadas:

1.  **User**
    *   Responsabilidade: Gerencia dados comuns e autenticação de usuários.
    *   Atributos Principais: `id`, `email`, `password`, `name`, `profile_picture`, `user_type`.
    *   Métodos Principais: `create()`, `findByEmail()`, `findById()`, `update()`, `verifyPassword()`.
    *   Relacionamentos: É a classe base para `Instructor` e `Student`. Relaciona-se com `Message` (como sender) e `Notification`.

2.  **Instructor**
    *   Responsabilidade: Representa o instrutor e suas funcionalidades específicas.
    *   Atributos Principais: `id`, `user_id` (FK), `specialty`, `bio`.
    *   Métodos Principais: `create()`, `findByUserId()`, `update()`, `getStudents()`, `linkStudent()`.
    *   Relacionamentos: Herda de `User` (conceitualmente, via `user_id`). Relaciona-se com `Student` através de `InstructorStudent`. Relaciona-se com `Conversation`.

3.  **Student**
    *   Responsabilidade: Representa o aluno e suas funcionalidades específicas.
    *   Atributos Principais: `id`, `user_id` (FK), `birth_date`, `phone`.
    *   Métodos Principais: `create()`, `findByUserId()`, `update()`, `getInstructors()`, `getAnamnesis()`, `getWeeklyResponses()`, `createWeeklyResponse()`.
    *   Relacionamentos: Herda de `User` (conceitualmente, via `user_id`). Relaciona-se com `Instructor` através de `InstructorStudent`. Possui uma `Anamnesis`. Possui várias `WeeklyResponse`. Relaciona-se com `Conversation`.

4.  **InstructorStudent**
    *   Responsabilidade: Tabela de associação para o relacionamento N:N entre `Instructor` e `Student`.
    *   Atributos Principais: `id`, `instructor_id` (FK), `student_id` (FK), `status`.

5.  **Anamnesis**
    *   Responsabilidade: Armazena os dados de saúde e histórico do aluno.
    *   Atributos Principais: `id`, `student_id` (FK), `age`, `weight`, `height`, `medical_history`, `objectives`, etc.
    *   Métodos Principais: `create()`, `findByStudentId()`, `update()`.
    *   Relacionamentos: Pertence a um `Student` (1:1).

6.  **WeeklyResponse**
    *   Responsabilidade: Armazena o feedback semanal do aluno.
    *   Atributos Principais: `id`, `student_id` (FK), `week_number`, `response_text`, `feeling`, etc.
    *   Relacionamentos: Pertence a um `Student` (1:N). Pode ter várias `ProgressImage`.

7.  **ProgressImage**
    *   Responsabilidade: Armazena o caminho das imagens de progresso.
    *   Atributos Principais: `id`, `weekly_response_id` (FK), `image_path`.
    *   Relacionamentos: Pertence a uma `WeeklyResponse` (1:N).

8.  **Conversation**
    *   Responsabilidade: Representa uma conversa entre um instrutor e um aluno.
    *   Atributos Principais: `id`, `instructor_id` (FK), `student_id` (FK).
    *   Métodos Principais (no ChatModel): `createConversation()`, `findConversation()`, `getMessages()`.
    *   Relacionamentos: Associa um `Instructor` e um `Student`. Contém várias `Message`.

9.  **Message**
    *   Responsabilidade: Representa uma única mensagem dentro de uma conversa.
    *   Atributos Principais: `id`, `conversation_id` (FK), `sender_id` (FK para User), `message_text`, `is_read`.
    *   Métodos Principais (no ChatModel): `sendMessage()`, `markMessagesAsRead()`.
    *   Relacionamentos: Pertence a uma `Conversation`. Enviada por um `User`.

10. **Notification** (Baseado no Schema)
    *   Responsabilidade: Armazena notificações para os usuários.
    *   Atributos Principais: `id`, `user_id` (FK), `title`, `message`, `is_read`, `notification_type`.
    *   Relacionamentos: Pertence a um `User`.

Estas classes e seus relacionamentos formarão a base para o Diagrama de Classes.

