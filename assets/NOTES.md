## CONTAINER COM POSTGRESQL
> - Necessário ter o docker instalado em sua maquina
> - Necessário ter o docker-compose instalado em sua maquina

Observe que no diretório raiz temos um docker-compose.yml ele serve para criar o nosso container com postgreSQL já configurado com um usuário, bancod e dados e uma senha, para isso execute o comando abaixo:

```bash
$ sudo docker-compose up
```

Você também pode executar o comando para criar e executar seu container com postgreSQL em background liberando seu terminal para isso basta acrescentar o **'-d'** deixando o comandod essa forma `sudo docker-compose up -d`

#### COMANDOS BÁSICOS PARA CONTAINER DOCKER
```bash
# Listar containers ver status e informacoes dos containers
$ sudo docker ps -a

# Iniciar container
$ sudo docker start CONTAINER_ID

# Acessar container via terminal
$ sudo docker container exec -it CONTAINER_ID bash

# Copiar um arquivo para fora do container
$ sudo docker cp CONTAINER_ID:FILE_NAME.example ./DIRECTORY_DESTINATION

# Copiar um arquivo para dentro do seu container
# (primeiro acesse o diretorio em sua maquina pessoal que contem o arquivo)
$ sudo docker cp FILE_NAME.example CONTAINER_ID:DIRECTORY_DESTINATION

# Baixar imagens do docker a partir de um arquivo do docker-compose configurado na raiz do projeto
# Acesse a raiz onde contem o arquivo docker-compose
$ sudo docker-compose pull

# Executar docker-compose baixado
# Acesse a raiz onde contem o arquivo docker-compose
$ sudo docker-compose up
# OBS: para executar em background sem travar o terminal use o parametro -d
$ sudo docker-compose up -d
```

#### COMANDOS BÁSICOS PARA POSTGRESQL
```bash
# Primeiro acessar o container do docker onde contem o postgres!!

# Fazer backup (dump) de um banco
$ pg_dump -c --if-exists -h 127.0.0.1 -U USER -d DATABASE -W > NAME_BACKUP.sql
# OBS: O exemplo abaixo é quando voce quer manter uma tabela 
# Ex: $ pg_dump -c --if-exists --exclude-table=strapi_administrator -h 127.0.0.1 -U strapi -d strapi -W > strapi.sql
$ pg_dump -c --if-exists --exclude-table=NOME_DA_TABELA_QUE_VC_QUER_MANTER -h 127.0.0.1 -U USER -d DATABASE -W > NAME_BACKUP.sql

# Fazer restore de um backup (dump) de um banco
# Ex: $ psql -h 127.0.0.1 -U strapi -d strapi -W < strapi.sql
$ psql -h HOST_ADDRESS -U USER -d DATABASE -W < BACKUP.sql
```


## CRIANDO API COM STRAPI 
Para criar a api vamos seguir os passos abaixo, lembrando que é necessário que primeiro você tenha criado o bancod e dados PostgreSQL local ou em um container docker como mostramos acima.

```bash
# Criar a api com create-strapi-app
$ yarn create strapi-app NOMEDOPROJETO

# Responda as perguntas com os dados de acesso ao bancod e dados

# Navegar até o diretorio da api/projeto
$ cd NOMEDOPROJETO

# Iniciar api
$ yarn develop

# Acesse a interface do seu strapi headless CMS pelo navegador
http://localhost:1337/admin/
``` 

## CONTAINER COM STRAPI E POSTGRESQL
> - Necessário ter o docker instalado em sua maquina
> - Necessário ter o docker-compose instalado em sua maquina

##### 1 navegar até o diretorio com a api
```bash
$ cd wongames-api
```

##### 2 Atualizar as imagens do strapi e do postgreSQL
```bash
$ sudo docker-compose pull
```

##### 3 Baixar e executar o container com strapi e postgreSQL (-d para executar em background)
```bash
  $ sudo docker-compose up -d
```

##### 4 Executar o comando de permissões toda vez que for alterar algo na pasta .app
```bash
sudo chown -R USUARIO ./app
```


## DEPLOY 
API E CMS NO HEROKU: https://dashboard.heroku.com/

FRONT-END NO NETLIFY: https://app.netlify.com/sites/curso-react-avancado/overview

ASSETS NO S3 AMAZON: 