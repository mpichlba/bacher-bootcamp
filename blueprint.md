# Backup mit Blueprints
### Blueprint in Kasten K10 hinzufügen:
```
kubectl --namespace kasten-io apply -f \
    https://raw.githubusercontent.com/kanisterio/kanister/0.92.0/examples/postgresql/blueprint-v2/postgres-blueprint.yaml
```
### Annotation der Applikation hinzufügen
```
kubectl --namespace postgresql annotate statefulset/postgres-postgresql \
    kanister.kasten.io/blueprint=postgres-bp
```
