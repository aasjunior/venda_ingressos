# Imersão Full Cycle & Full Stack

## Aula 01

### Full Cycle Developer

Como desenvolvedores **Full Cycle**, as equipes de desenvolvimento passam a ter que cumprir as seguintes etapas:

- Arquitetar
- Desenvolver
- Testar
- Deployar
- Monitorar
- Dar suporte aos microsserviços

Pricipais pilares do desenvolvimento **Full Cycle**:

1. **Operate What you Build**: O desnvolvedor fica responsável desde a construção até a entrega do projeto.
2. **Ferramentas para escalar**: Necessário dominío de ferramentas que auxiliam na entrega contínua do projeto, como **pipelines** de **CI/CD**, **Docker**, **Kubernetes**, **Stacks de monitoramento**, etc.

### Full Cycle Developer x Full Cycle Stack

- **Full Stack**: Habilidades de desenvolvimento. Domínio em **stacks** e **linguagens** para desenvolvimento em diversas perspectivas, como **Front-End** e **Back-End**.
- **Full Cycle Developer**: Além de desenvolver, o desenvolvedor consegue arquitetar e entregar a aplicação de forma testada, com deplay e monitoramento.

## Projeto prático

Desenvolvimento de um sistema de venda de ingressos
- Gerenciamento de eventos / processamento de reservas
    - Integração com sistemas de parceiros
- Sistemas de parceiros
- Frontend
- API Gateway

### Dinâmica do projeto

![alt text](image-1.png)

#### Tecnologias

- Docker
- Linguagem Go
- Next.js (Frontend)
- Nest.js
- Kong API Gateway

![alt text](image-2.png)

### Arquitetura do sistema

![alt text](image-3.png)

#### Operação principal - Reservar ingresso

![alt text](image-4.png)

### Microsserviços de parceiros de ingressos com Nest.js

- **Tecnologias utilizadas**:
    - TypeScript/JavaScript
    - Nest.js
    - Prisma ORM
    - Rest
    - Autenticação

- **Etapas do projeto**:
    - Criação do projeto **Nest.js**
    - Criação do banco de dados **MySQL** e integração com o **Prisma**
    - Criação de uma **lib** para facilitar na criação de várias **APIs** de parceiros
    - Criação de uma **API** dos eventos
    - Criação de uma **API** dos spots
    - Criação do **endpoint** da **API** para reserva
    - Criação de vários **Apps** para serem as **APIs** dos parceiros
    - Permissão do acesso as **APIs** via token

#### Sobre o Nest.js

O **Nest.js** é um framework **Node.js**, que trabalha tanto com **JavaScript** e **TypeScript**, que visa principalmente ter uma arquitetura modular e escalável.

Permite a criação de aplicaçções **web** com integração a vários meios de comunicação:
- REST
- GraphQL
- Outros (RabbitMQ, Redis, Kafka, Nats, etc.)

Possui integração com vários bancos de dados por meio de vários **ORMs** famosos:
- Sequelize
- Prisma
- TypeORM
- Mikro ORM
- etc.

![ ](image-5.png)


###### Extensões VSCode
- Eslint
- Prettier
- Rest Client
- Prisma

### Iniciando o projeto via WSL/ubuntu

1. Abra o terminal WSL e execute o seguinte comando:
```bash
sudo apt-get install curl
```

**curl:** ferramenta usada para baixar conteúdo da Internet na linha de comando.

2. Instale o **NVM**:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

3. Instale o **Node.js**:
```bash
nvm install 20
```

4. Instale o **Nestjs/Cli**:
```bash
npm install -g @nestjs/cli
```

5. Crie uma nova aplicação:
```bash
nest new nestjs-partners-api
```

6. Execute o projeto com o comando:
```bash
npm run start:dev 
```

7. O projeto vai estar rodando em:
```
http://127.0.0.1:3000
```

![alt text](image-6.png)

![alt text](image-7.png)
![alt text](image-8.png)

- Criação de controller de eventos:
```bash
nest generate controller event
```

- Criação de recurso com todos endponts do CRUD:

![alt text](image-9.png)

**Obs.**: A convensão dos nomes dos arquivos gerados automaticamente é chamada de **CoC** (Convention over configuration)


**./docker-compose.yaml**:

```yaml
services:
  db:
    image: mysql:8.0.30-debian
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: nest
    
    ports:
     - 3306:3306
```

Entrar no container docker:

```bash
docker compose exec db bash
```

Entrar no console **MySQL**:

```bash
mysql -uroot -proot
```

#### Prisma

```shell
npx prisma init
```

**./prisma/schema.prisma**

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

**.env**
```shell
DATABASE_URL="mysql://root:root@localhost:3306/nest"
```

**./prisma/schema.prisma**

```prisma
model Event{
  id String @id @default(uuid())
  name String
  description String
  date DateTime
  price Float
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

```shell
npx prisma migrate dev
```

console **MySQL**
```mysql
# 1º
use Event;

# 2º
show tables;

# 3º
describe Event;
```