<p align="center">
	<img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Postgresql_elephant.svg" width=80>
	<img src="https://upload.wikimedia.org/wikipedia/en/f/f4/Docker_logo.svg" width=200>
</p>
<p align="center">
</p>

<h1 align="center">Postgres + Docker</h1>

Esse projeto cria um banco de dados Postgres dentro de um container Docker.

Depois de criado o container a partir do arquivo [docker compose](docker-compose.yaml) é possível executar scripts SQL presentes no diretório `scripts`.





# Criando o container a partir do docker-compose.yaml

```sh
$ docker compose up -d
```

Verifique se o container esta em execução com:

```sh
$ docker container ls
```






# Executando scripts SQL

Depois de criar o container com o comando `docker compose up -d`, abra um terminal dentro do container com o seguinte comando:

```bash
$ docker exec -it pgtest bash
```

Em seguida execute o seguinte comando para executar um dos scripts da pasta `scripts`

```bash
$ psql -U postgres -d postgres -a -f /scripts/create_db.sql
```

É possível usilizar o comando acima apenas mudando o nome do script a ser executado, ex:


```bash
$ psql -U postgres -d escola -a -f /scripts/create_table.sql
```

Em seguida podemos inserir dados no banco através do scritp `insert_data.sql`


```bash
$ psql -U postgres -d escola -a -f /scripts/insert_data.sql
```




# Comando `psql`

É uma aplicação de linha de comando utilizada para se conectar com o servidor Postgres.

[Documentação oficial](https://www.postgresql.org/docs/current/app-psql.html)




# Importanto dados de um arquivo CSV

via linha de comando (`psql`):

`COPY table_name FROM 'path/to/file.txt' WITH (FORMAT csv)`

[Referência:Stackoverflow](https://stackoverflow.com/questions/46395085/how-to-seed-data-into-a-postgres-database-table-from-a-csv-file)

`\copy <table_name> from '<path/to/file.csv>' delimiter ',' CSV HEADER;`

[Referênia](https://hasura.io/docs/2.0/schema/postgres/postgres-guides/import-data-from-csv/)





# Tipos de dados no Postgresql

[Data types](https://www.postgresql.org/docs/current/datatype.html)

[Data types: Text Search Types](https://www.postgresql.org/docs/current/datatype-textsearch.html)

[Insert](https://www.postgresql.org/docs/8.1/sql-insert.html)

[Update](https://www.postgresql.org/docs/12/sql-update.html)

[Delete](https://www.postgresql.org/docs/current/sql-delete.html)






# Criando um container Postgres manualmente

[Imagem oficial](https://hub.docker.com/_/postgres)

```sh
$ docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

```sh
$ docker run -it --rm --network some-network postgres psql -h some-postgres -U postgres
```

```sh
$ docker run -d \
	--name some-postgres \
	-e POSTGRES_PASSWORD=mysecretpassword \
	-e PGDATA=/var/lib/postgresql/data/pgdata \
	-v /custom/mount:/var/lib/postgresql/data \
	postgres
```





# Referencias

### Comandos `psql` úteis

`\l` -> lista bancos de dados

`\c <db_name>` -> conecta a um banco de dados

`\q` > sair

### Executar script SQL dentro do container

`psql -U <user> -d <db_name> -a -f <file.sql>`

[Stackoverflow](https://stackoverflow.com/questions/9736085/run-a-postgresql-sql-file-using-command-line-arguments)


### Erros

`role "root" does not exist postgres in docker-compose`

[Stackoverflow](https://stackoverflow.com/questions/60193781/postgres-with-docker-compose-gives-fatal-role-root-does-not-exist-error)




# Minimal Docker Compose File

```yaml
services:
  db:
    image: postgres
    container_name: db
    restart: always
    environment:
      POSTGRES_PASSWORD: 12345
      POSTGRES_USER: tiago
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:

```