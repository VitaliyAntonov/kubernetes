
Ресурс [ConfigMap](https://phoenixnap.com/kb/kubernetes-configmap-create-and-use) содержит данные, используемые в процессе развертывания.

1. Создайте файл ConfigMap YAML в текстовом редакторе.

```
nano postgres-configmap.yaml
```

2. Наиболее важной частью файла является раздел данных, где вы указываете **имя базы данных** , **имя пользователя** и **пароль** для входа в экземпляр PostgreSQL.

В примере используются следующие параметры в файле ConfigMap.

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: postgres-config
  labels:
    app: postgres
data:
  POSTGRES_DB: postgresdb
  POSTGRES_USER: admin
  POSTGRES_PASSWORD: test123
```

3. Сохраните файл и выйдите. Затем примените ресурс с помощью **`kubectl`**:

```
kubectl apply -f postgres-configmap.yaml
```

Система подтверждает успешное создание файла конфигурации.

![[Pasted image 20221125195253.png]]

