# Installation von Kasten K10
### Helm Repository hinzufügen:
`helm repo add kasten https://charts.kasten.io/`
### Kasten-io Namespace anlegen:
`kubectl create namespace kasten-io`

### Pre-Flight-Check ausführen
- `curl https://docs.kasten.io/tools/k10_primer.sh | bash`

### IP Adresse vom Worker Node ermitteln ###
```
kubectl get nodes -o wide
```

Die ingress.host Adresse setzt sich wie folgt zusammen: kasten.\<IP-addresse-workernode\>.nip.io zb kasten.10.2.2.223.nip.io

### Kasten K10 installieren:
```
helm install k10 kasten/k10 --namespace=kasten-io \
    --set ingress.create=true \
    --set ingress.class=nginx \
    --set ingress.host=<FQDN for name-based virtual host> \
    --set auth.tokenAuth.enabled=true
```
### Kasten K10 Pods überprüfen
`kubectl get pods -n kasten-io`
```
NAME                                     READY   STATUS    RESTARTS   AGE
aggregatedapis-svc-867d7b4486-j4p6b      1/1     Running   0          12d
auth-svc-69bf7bc8d-j8p29                 2/2     Running   0          12d
catalog-svc-7584d47f5f-spztn             2/2     Running   0          12d
controllermanager-svc-7897f5c95b-rxx65   1/1     Running   0          12d
crypto-svc-847d99847b-47657              4/4     Running   0          12d
dashboardbff-svc-78bd66bcd9-qdmq7        2/2     Running   0          12d
executor-svc-5756dd4467-4c68k            2/2     Running   0          12d
executor-svc-5756dd4467-9gl5m            2/2     Running   0          12d
executor-svc-5756dd4467-csmzf            2/2     Running   0          12d
frontend-svc-6475dbddf6-sp55k            1/1     Running   0          12d
gateway-7957b4ccbb-ld6pk                 1/1     Running   0          12d
jobs-svc-8478965c8c-dfk7b                1/1     Running   0          12d
k10-grafana-767d9b4b8d-dzkl7             1/1     Running   0          12d
kanister-svc-56b4f9dbc9-nttg8            1/1     Running   0          12d
logging-svc-5ff9dbb454-hkhdn             1/1     Running   0          12d
metering-svc-55fff8c87-bhm7x             1/1     Running   0          12d
prometheus-server-77b8cccc7c-hj8rb       2/2     Running   0          12d
state-svc-7cbf9f5c9d-2kgbt               2/2     Running   0          12d
```
### Ingress überprüfen:
`kubectl get ingress -n kasten-io`
```
NAMESPACE   NAME          CLASS    HOSTS                               ADDRESS          PORTS   AGE
kasten-io   k10-ingress   nginx    <FQDN for name-based virtual host>  192.168.20.111   80      12d
```
### K10 Token anzeigen für den Login:
`sa_secret=$(kubectl get serviceaccount k10-k10 -o jsonpath="{.secrets[0].name}" --namespace kasten-io)`\
`kubectl get secret $sa_secret --namespace kasten-io -ojsonpath="{.data.token}{'\n'}" | base64 --decode`
