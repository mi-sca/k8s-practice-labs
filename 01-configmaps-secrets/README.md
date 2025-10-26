# Lab 01 – ConfigMaps and Secrets

### Obiettivo
Creare una ConfigMap e un Secret per configurare un’applicazione.

### Passi eseguiti
```bash
kubectl create configmap app-config \
  --from-literal=DB_HOST=localhost \
  --from-literal=DB_PORT=3306

kubectl create secret generic db-secret \
  --from-literal=DB_PASSWORD=supersecret

kubectl apply -f app-pod.yaml
```

### Verifica
```bash
kubectl get po

kubectl exec app-pod -- env | grep DB_
```
Output atteso:
```bash
DB_HOST=localhost
DB_PORT=3306
DB_PASSWORD=supersecret
```
