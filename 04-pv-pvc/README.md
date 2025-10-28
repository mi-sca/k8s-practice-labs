In questo scenario devi:

- Creare un PersistentVolume (PV)
- Creare un PersistentVolumeClaim (PVC)
- Montare il PVC in un Pod
- Verificare che i dati rimangano dopo l'eliminazione del Pod
---

## Crea il PV
Applica il file `pv.yaml`
```bash
kubectl apply -f pv.yaml
```
Verifica che il PV sia stato creato
```bash
kubectl get pv
```

## Crea il PVC
Applica il file `pvc.yaml`
```bash
kubectl apply -f pvc.yaml
```
Verifica che il PVC sia stato creato
```bash
kubectl get pvc
```

## Crea il Pod con il PVC
Applica il file `pod.yaml`
```bash
kubectl apply -f pod.yaml
```
Verifica che il Pod sia in `Running`
```bash
kubectl get pods
```

## Scrivi dati nel PV
Scrivere un file nel volume montato
```bash
kubectl exec -it pv-test-pod -- sh -c "echo Si funziona come deve!!! > /data/hello.txt"
```
Verifica il contenuto
```bash
kubectl exec -it pv-test-pod -- cat /data/hello.txt
```

## Cancella e ricrea il Pod
Cancella il Pod
```bash
kubectl delete pod pv-test-pod
```
Ricrea il Pod
```bash
kubectl apply -f pod.yaml
```

## Verifica la persistenza dei dati
Controlla se il file esiste ancora dopo aver ricreato il pod
```bash
kubectl exec -it pv-test-pod -- cat /data/hello.txt
```
Risultato atteso:
```bash
Si funziona come deve!!!
```

