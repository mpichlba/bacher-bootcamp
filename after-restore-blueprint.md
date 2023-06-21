### Verbinden mit der Postgresql Datenbank
`export POSTGRES_PASSWORD=$(kubectl get secret --namespace postgresql postgres-postgresql -o jsonpath="{.data.postgres-password}" | base64 -d)`

`kubectl run postgres-postgresql-client --rm --tty -i --restart='Never' --namespace postgresql --image docker.io/bitnami/postgresql:15.3.0-debian-11-r7 --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgres-postgresql -U postgres -d postgres -p 5432
`\

output: `postgres=#`
### Beispieldaten anzeigen lassen (innerhalb von `postgres=#`):
`SELECT * FROM companies;`
```
 company_id | company_name
------------+--------------
          1 | BlueBird Inc
          2 | Dolphin LLC
(2 rows)
```
`exit`
