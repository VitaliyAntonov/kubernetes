
1. Создайте файл развертывания YAML.

```
nano postgres-deployment.yaml
```

2. Файл развертывания содержит конфигурацию развертывания PostgreSQL и предоставляет спецификации для контейнеров и томов:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
        - name: postgres
          image: postgres:10.1
          imagePullPolicy: "IfNotPresent"
          ports:
            - containerPort: 5432
          envFrom:
            - configMapRef:
                name: postgres-config
          volumeMounts:
            - mountPath: /var/lib/postgresql/data
              name: postgredb
      volumes:
        - name: postgredb
          persistentVolumeClaim:
            claimName: postgres-pv-claim
```

3. Сохраните файл и выйдите. Примените развертывание с помощью **`kubectl`**:

```
kubectl apply -f postgres-deployment.yaml
```

Система подтверждает успешное создание развертывания.

![[Pasted image 20221125195755.png]]




