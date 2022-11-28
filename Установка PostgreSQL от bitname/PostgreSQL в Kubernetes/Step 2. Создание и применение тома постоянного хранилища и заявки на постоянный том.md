
1. Создайте файл YAML для конфигурации хранилища.

```
nano postgres-storage.yaml
```

2. Метод развертывания Helm chart использует два отдельных файла для [постоянного тома](https://phoenixnap.com/kb/kubernetes-persistent-volumes) и заявки на постоянный том, но вы также можете поместить обе конфигурации в один файл, как в примере ниже.

```
kind: PersistentVolume
apiVersion: v1
metadata:
  name: postgres-pv-volume
  labels:
    type: local
    app: postgres
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/mnt/data"
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: postgres-pv-claim
  labels:
    app: postgres
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 5Gi
```

3. Сохраните файл и выйдите. Примените ресурсы с помощью **`kubectl`**:

```
kubectl apply -f postgres-storage.yaml
```

Система подтверждает успешное создание как PV, так и PVC.

![[Pasted image 20221125195443.png]]

4. Убедитесь, что PVC подключен к PV, с помощью следующей команды:

```
kubectl get pvc
```

PVC находится в состоянии **Bound** , и PVC готов к использованию в развертывании PostgreSQL.

![[Pasted image 20221125195514.png]]





