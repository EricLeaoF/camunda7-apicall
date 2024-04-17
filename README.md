# Camunda 7 com envio de email

Esse projeto é uma demonstração que contém um simples preenchimento de formulário integrado a um serviço de envio de email.  

## Subir o serviço de email

A request realizada nesse projeto é para [mailSender](https://github.com/EricLeaoF/mailsender-sb) do qual basta fazer o download e iniciar a aplicação

Lembrando que a porta do serviço de emails deve ser 8081, já que o camunda já executará na porta 8080. No arquivo aplication.properties devem ser definidas as variáveis do seu servidor de emails:

```Java

spring.application.name=
spring.mail.host=sandbox.smtp.mailtrap.io
spring.mail.port=
spring.mail.username=a0e9f5c7acc0fd
spring.mail.password=39d60bf2a64d4d
spring.mail.properties.mail.smtp.auth=
spring.mail.properties.mail.smtp.starttls.enable=
server.port=8081

```

## Rodar o projeto

O projeto contém uma aplicação **Camunda Spring Boot**. Para rodar o projeto e iniciar uma instância de processo na seção TaskList, siga os passos seguintes:

1. Baixe o projeto e abra a aplicação **Camunda Spring Boot** na sua IDE usando Java 11.
2. Inicie a aplicação.
3. Inicie o processo o start process ou inicie através do REST. 
4. Se você [Iniciar a instancia via REST](https://docs.camunda.org/manual/latest/reference/rest/process-definition/post-start-process-instance/) garanta que as variáveis necessárias sejam incluidas.

Exemplo de inicio via REST:

```Json
{
  "variables": {
    "nome_solicitante" : {
        "value" : "Nome do solicitante",
        "type": "String"
    },
    "nome_produto" : {
      "value" : "Nome do produto",
      "type": "String"
    },
    "valor_produto" : {
      "value": 10
    },
    "email_destino" : {
      "value" : "Email de aprovação ou reprovação",
      "type" : "String"
    }
  },
 "businessKey" : "myBusinessKey"
}

```
## Aprovar ou reprovar a solicitação

Ao iniciar o processo, a primeira tarefa será uma userTask, do qual deve ser informada a variável "aprovado" como sendo true ou false. Basta acessar a seção taskList no camunda, buscar pela tarefa e adicionar essa variável antes de mandar a tarefa se completar.

## Verificação da caixa de email

