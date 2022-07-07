# API de Usuários 
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL3-blue.svg)](https://opensource.org/licenses/gpl-3.0.html)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=fga-eps-mds_2021-2-SiGeD-Users&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=fga-eps-mds_2021-2-SiGeD-Users)

Essa API faz parte da arquitetura de microsserviços do projeto [`SiGeD`](https://github.com/fga-eps-mds/2021-2-SiGeD-Doc), sua funcionalidade é possibilitar o controle dos dados dos usuários. 

## Como contribuir?

Gostaria de contribuir com nosso projeto? Acesse o nosso [guia de contribuição](https://fga-eps-mds.github.io/2021-2-SiGeD-Doc/contribuicao/) onde são explicados todos os passos.
Caso reste alguma dúvida, você também pode entrar em contato conosco criando uma issue.

## Documentação

A documentação do projeto pode ser acessada pelo nosso site em https://fga-eps-mds.github.io/2021-2-SiGeD-Doc/.

## Testes

Todas as funções adicionadas nessa API devem ser testadas, o repositŕorio aceita até 10% do total de lihas não testadas. Para rodar os testes nesse repositŕio deve ser executado o comando:

```bash
docker-compose run api_users bash -c  "yarn && yarn jest --coverage --forceExit"
```

## Como rodar?

O arquivo .env possui configurações iniciais que podem ser alteradas de acordo com a necessidade. São elas:
 - SECRET: chave para criptografia das senhas
 - DB_USER: usuário de acesso ao banco de dados
 - DB_PASS: senha de acesso ao banco de dados
 - DB_NAME: nome da base de dados
 - DB_HOST: host da base de dados
 - host: o protocolo de comunicação do email
 - port: porta de comunicação do email
 - email: email que será utilizado para enviar senhas temporárias
 - pass: senha do email

Veja o exemplo abaixo:

```
SECRET=chavedesegredo
DB_USER=api_user
DB_PASS=api_password
DB_NAME=api_database
DB_HOST=db_users
host=smtp.gmail.com
port=
email=meuemail@gmail.com
pass=minhasenha
```

Para rodar a API é preciso usar os seguintes comandos usando o docker:

Crie uma network para os containers da API, caso não exista:

```bash
docker network create siged_backend
```

Suba o container com o comando:

```bash
docker-compose up
```
A API estará rodando na [porta 3001](http://localhost:3001).

## Seeders

Para popular a base de dados (após subir o docker-compose) com dados exemplos use os seguintes comandos:

```bash
docker exec -it backend_users bash -c "node src/seeders/seedUsers.js"
```

Para resetar o banco use o comando:

```bash
docker-compose rm
```

## Rotas

**GET: `/users/`**

Para receber os dados dos usuários.


**POST: `/signup/`**

Para criar um novo usuário, envie os dados nesse formato:

```json
{
    "name": "Nome do Usuário",
    "email": "usuario@email.com",
    "role": "Cargo",
    "sector": "Área de Atuação",
    "pass": "Senha"
}
```

**POST: `/login/`**

Para entrar no sitema, envie os dados nesse formato:

```json
{
    "email": "usuario@email.com",
    "pass": "Senha"
}
```

**PUT: `/users/update/:id`**

Para atualizar os dados do usuário, envie os dados atualizados seguindo o padrão:

```json
{
    "name": "Nome do Usuário",
    "email": "usuario@email.com",
    "role": "Cargo",
    "sector": "Área de Atuação",
    "pass": "Senha"
}
```

**DELETE: `/users/delete/:id`**

Para desativar um usuário pelo `id`.
