# Deployment einer Demo postgres Datenbank (bitnami)
### Helm Repository von Bitnami hinzufügen
`helm repo add bitnami https://charts.bitnami.com/bitnami` \
_`"bitnami" has been added to your repositories`_
### Namespace für die Applikation anlegen
`kubectl create namespace postgresql` \
_`namespace/postgresql created`_
### Postgresql mit Standadparametern anlegen
`helm install --namespace postgresql postgres bitnami/postgresql` 
```shell
NAME: postgres
LAST DEPLOYED: Wed Jun 21 09:46:00 2023
NAMESPACE: postgresql
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: postgresql
CHART VERSION: 12.5.8
APP VERSION: 15.3.0
```
### Installation überprüfen:
`kubectl get pods -n postgresql`
```
NAME                    READY   STATUS    RESTARTS   AGE
postgres-postgresql-0   1/1     Running   0          8m11s
```
`kubectl get persistentvolumeclaims -n postgresql`
```
NAME                         STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-postgres-postgresql-0   Bound    pvc-27f78722-b2db-4cac-8254-073d417d202a   8Gi        RWO            longhorn-1     8m45s
```
### Verbinden mit der Postgresql Datenbank
`export POSTGRES_PASSWORD=$(kubectl get secret --namespace postgresql postgres-postgresql -o jsonpath="{.data.postgres-password}" | base64 -d)`

`kubectl run postgres-postgresql-client --rm --tty -i --restart='Never' --namespace postgresql --image docker.io/bitnami/postgresql:15.3.0-debian-11-r7 --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgres-postgresql -U postgres -d postgres -p 5432
`

output: `postgres=#`
### Beispieldaten hinzufügen (innerhalb von `postgres=#`):
`CREATE TABLE companies(company_id SERIAL PRIMARY KEY, company_name VARCHAR(255) NOT NULL);`

`INSERT INTO companies(company_name)VALUES('BlueBird Inc'),('Dolphin LLC');`

`SELECT * FROM companies;`
```
 company_id | company_name
------------+--------------
          1 | BlueBird Inc
          2 | Dolphin LLC
(2 rows)
```
`exit`









