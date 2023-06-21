# Deployment einer Demo postgres Datenbank (bitnami)
## Helm Repository von Bitnami hinzufügen
`helm repo add bitnami https://charts.bitnami.com/bitnami`
## Namespace für die Applikation anlegen
`kubectl create namespace postgresql`
## Postgresql mit Standadparametern anlegen
`helm install --namespace postgresql postgres bitnami/postgresql`
