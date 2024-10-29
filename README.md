# Postgres + Docker

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

# Tipos de dados no Postgresql

[Data types](https://www.postgresql.org/docs/current/datatype.html)

[Data types: Text Search Types](https://www.postgresql.org/docs/current/datatype-textsearch.html)

[Insert](https://www.postgresql.org/docs/8.1/sql-insert.html)

[Update](https://www.postgresql.org/docs/12/sql-update.html)

[Delete](https://www.postgresql.org/docs/current/sql-delete.html)


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
