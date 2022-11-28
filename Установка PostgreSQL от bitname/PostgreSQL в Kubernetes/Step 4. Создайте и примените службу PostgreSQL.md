
1. Наконец, создайте файл YAML для настройки службы PostgreSQL.

```
nano postgres-service.yaml
```

2. Укажите тип службы и порты. В примере используется следующая конфигурация:

```
apiVersion: v1
kind: Service
metadata:
  name: postgres
  labels:
    app: postgres
spec:
  type: NodePort
  ports:
   - port: 5432
  selector:
   app: postgres
```

3. Сохраните файл и выйдите. Примените конфигурацию с помощью **`kubectl`**:

```
kubectl apply -f postgres-service.yaml
```

Система подтверждает успешное создание услуги.

![[Pasted image 20221125200115.png]]

4. Используйте следующую команду, чтобы вывести список всех ресурсов в системе.

```
kubectl get all
```

Модуль и развертывание показывают состояние готовности **1/1 .** Желаемое количество наборов реплик отражает то, что настроено в файле развертывания YAML.

![[Pasted image 20221125200156.png]]








