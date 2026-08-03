# notificacao

Microsserviço de **envio de notificações por e-mail**, construído em **Java 21 + Spring Boot**, parte de uma arquitetura de **microsserviços**.

## 📖 Sobre o projeto

O `notificacao` é responsável por disparar e-mails (ex.: confirmações, lembretes de tarefas) dentro do ecossistema de microsserviços. Ele usa o **Spring Mail** para o envio e o **Thymeleaf** para renderizar o conteúdo dos e-mails a partir de templates HTML, mantendo o corpo das mensagens desacoplado da lógica da aplicação.

### 🧩 Arquitetura do ecossistema

Este serviço faz parte de um conjunto de microsserviços que trabalham juntos:

| Serviço | Porta | Responsabilidade | Banco |
|---|---|---|---|
| [`usuario`](https://github.com/BrenoMelem/usuario) | 8080 | Cadastro/autenticação de usuários | PostgreSQL |
| [`agendador-tarefas`](https://github.com/BrenoMelem/agendador-tarefas) | 8081 | Agendamento de tarefas | MongoDB |
| **`notificacao`** | **8082** | **Envio de e-mails/notificações (este repositório)** | — |
| [`bff-agendador`](https://github.com/BrenoMelem/bff-agendador) | 8083 | Agrega as chamadas aos serviços acima | — |

## 🚀 Tecnologias utilizadas

**Linguagem e build**
- Java 21
- Gradle (Gradle Wrapper incluído — não precisa ter o Gradle instalado)

**Framework e core**
- Spring Boot 4.0.6
- Spring Web MVC — camada REST
- Spring Boot Starter Mail — envio de e-mails (SMTP)
- Thymeleaf — templates HTML para o conteúdo dos e-mails

**Produtividade**
- Lombok

**Testes**
- Spring Boot Starter Test (Mail, Thymeleaf e Web)
- JUnit 5 (JUnit Platform)

**Infraestrutura**
- Docker (build multi-stage)
- Docker Compose
- GitHub Actions (CI/CD)

## 📂 Estrutura do projeto

```
notificacao/
├── .github/workflows/     # Pipelines de CI (GitHub Actions)
├── gradle/wrapper/         # Gradle Wrapper
├── src/main/                # Código-fonte da aplicação (inclui templates Thymeleaf)
├── build.gradle             # Configuração de build e dependências
├── docker-compose.yml       # Orquestração local
├── Dockerfile                # Build multi-stage da imagem da aplicação
└── settings.gradle
```

## ⚙️ Pré-requisitos

- Java 21 (JDK)
- Docker e Docker Compose (para rodar via container)
- Uma conta/servidor SMTP para envio dos e-mails (ex.: Gmail com senha de app)

## ▶️ Como executar

### Opção 1 — Via Docker Compose (recomendado)

1. Crie um arquivo `.env` na raiz do projeto com as credenciais de e-mail, por exemplo:

   ```env
   MAIL_USERNAME=seu-email@gmail.com
   MAIL_PASSWORD=sua-senha-de-app
   ```

2. Suba o container:

   ```bash
   docker-compose up --build
   ```

3. A aplicação estará disponível em `http://localhost:8082`.

### Opção 2 — Localmente com Gradle

1. Configure as credenciais de e-mail em `application.properties`/`application.yml`.
2. Execute:

   ```bash
   ./gradlew bootRun
   ```

## 🧪 Testes

```bash
./gradlew test
```

## 🔁 CI/CD

O repositório conta com workflows em `.github/workflows` para automatizar build e verificações a cada push/pull request.

## 🤝 Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir uma *issue* ou enviar um *pull request*.
