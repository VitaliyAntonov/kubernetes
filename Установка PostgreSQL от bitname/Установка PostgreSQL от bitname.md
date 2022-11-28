
Поиск репозиториев:

	helm search hub postgresql bitnami

![[Pasted image 20221122161703.png]]

https://artifacthub.io/packages/helm/bitnami/po

Добавляем репозитории bitnami с сайта 
https://artifacthub.io/packages/helm/bitnami/postgresql

командой :

	helm repo add my-repo https://charts.bitnami.com/bitnami

Репозитории bitnami добавляются на локальную машину(мой комп)

Ищем chart для postgresql в добавленных репозиториях:

	helm search repo postgresql

![[Pasted image 20221123164214.png]]

Так как репозитории добавлены как my-repo, нас интересует chart 

	my-repo/postgresql

Смотрим информацию по данному chart-у:

	helm show chart my-repo/postgresql

Команда выводит yaml файл данного chart - а  chart.yaml

![[Pasted image 20221123165126.png]]

	annotations:  
	 category: Database  
	apiVersion: v2  
	appVersion: 15.1.0  
	dependencies:  
	- name: common  
	 repository: https://charts.bitnami.com/bitnami  
	 tags:  
	 - bitnami-common  
	 version: 2.x.x  
	description: PostgreSQL (Postgres) is an open source object-relational database known  
	 for reliability and data integrity. ACID-compliant, it supports foreign keys, joins,  
	 views, triggers and stored procedures.  
	home: https://github.com/bitnami/charts/tree/main/bitnami/postgresql  
	icon: https://bitnami.com/assets/stacks/postgresql/img/postgresql-stack-220x234.png  
	keywords:  
	- postgresql  
	- postgres  
	- database  
	- sql  
	- replication  
	- cluster  
	maintainers:  
	- name: Bitnami  
	 url: https://github.com/bitnami/charts  
	name: postgresql  
	sources:  
	- https://github.com/bitnami/containers/tree/main/bitnami/postgresql  
	- https://www.postgresql.org/  
	version: 12.1.2


Просмотреть файл настроек values.yaml данного chart можно командой:

	helm show values my-repo/postgresql

Файл настроек довольно большой и выдача лога длинная


Установка в пространство имён пода postgresql из chart-а 

	helm install postgresql --namespace vitaliy my-repo/postgresql

выдача лога после установки:

	NAME: postgresql  
	LAST DEPLOYED: Thu Nov 24 20:15:45 2022  
	NAMESPACE: vitaliy  
	STATUS: deployed  
	REVISION: 1  
	TEST SUITE: None  
	NOTES:  
	CHART NAME: postgresql  
	CHART VERSION: 12.1.2  
	APP VERSION: 15.1.0  
	  
	** Please be patient while the chart is being deployed **  
	  
	PostgreSQL can be accessed via port 5432 on the following DNS names from within your cluster:  
	  
	   postgresql.vitaliy.svc.cluster.local - Read/Write connection  
	  
	To get the password for "postgres" run:  
	  
	   export POSTGRES_PASSWORD=$(kubectl get secret --namespace vitaliy postgresql -o jsonpath="{.data.postgres-password}" | base64 -d)  
	  
	To connect to your database run the following command:  
	  
	   kubectl run postgresql-client --rm --tty -i --restart='Never' --namespace vitaliy --image docker.io/bitnami/postgresql:15.1.0-debian-11-r0 --env="PGPASSWORD=$POSTGRES_PASS  
	WORD" \  
	     --command -- psql --host postgresql -U postgres -d postgres -p 5432  
	  
   > 	NOTE: If you access the container using bash, make sure that you execute "/opt/bitnami/scripts/postgresql/entrypoint.sh /bin/bash" in order to avoid the error "psql: loc  
	al user with ID 1001} does not exist"  
	  
	To connect to your database from outside the cluster execute the following commands:  
	  
	   kubectl port-forward --namespace vitaliy svc/postgresql 5432:5432 &  
	   PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432


Проверяем поды в пространстве имён:

	kubectl get pods -n=vitaliy

Лог:
	
	NAME                                READY   STATUS    RESTARTS   AGE  
	nginx-deployment-7bcddbd866-bxqd2   1/1     Running   0          2d21h  
	nginx-deployment-7bcddbd866-m8vkv   1/1     Running   0          2d21h  
	postgresql-0                        1/1     Running   0          9m10s


Смотрим описание модуля(пода):

	kubectl describe pods postgresql-0 -n=vitaliy

лог:

	Name:             postgresql-0  
	Namespace:        vitaliy  
	Priority:         0  
	Service Account:  default  
	Node:             p-01/192.168.1.201  
	Start Time:       Thu, 24 Nov 2022 20:20:41 +0500  
	Labels:           app.kubernetes.io/component=primary  
	                 app.kubernetes.io/instance=postgresql  
	                 app.kubernetes.io/managed-by=Helm  
	                 app.kubernetes.io/name=postgresql  
	                 controller-revision-hash=postgresql-65d8cfc467  
	                 helm.sh/chart=postgresql-12.1.2  
	                 statefulset.kubernetes.io/pod-name=postgresql-0  
	Annotations:      <none>  
	Status:           Running  
	IP:               10.42.0.74  
	IPs:  
	 IP:           10.42.0.74  
	Controlled By:  StatefulSet/postgresql  
	Containers:  
	 postgresql:  
	   Container ID:   containerd://b42a753959a772ed90623dfb9fa9ebee3fa67d8ddab2e78aa998a0111030aa0a  
	   Image:          docker.io/bitnami/postgresql:15.1.0-debian-11-r0  
	   Image ID:       docker.io/bitnami/postgresql@sha256:27915588d5203a10a1c23624d9c81644437f33b7c224e25f79bcd9bd09bbb8e2  
	   Port:           5432/TCP  
	   Host Port:      0/TCP  
	   State:          Running  
	     Started:      Thu, 24 Nov 2022 20:21:03 +0500  
	   Ready:          True  
	   Restart Count:  0  
	   Requests:  
	     cpu:      250m  
	     memory:   256Mi  
	   Liveness:   exec [/bin/sh -c exec pg_isready -U "postgres" -h 127.0.0.1 -p 5432] delay=30s timeout=5s period=10s #success=1 #failure=6  
	   Readiness:  exec [/bin/sh -c -e exec pg_isready -U "postgres" -h 127.0.0.1 -p 5432  
	[ -f /opt/bitnami/postgresql/tmp/.initialized ] || [ -f /bitnami/postgresql/.initialized ]  
	] delay=5s timeout=5s period=10s #success=1 #failure=6  
	   Environment:  
	     BITNAMI_DEBUG:                        false  
	     POSTGRESQL_PORT_NUMBER:               5432  
	     POSTGRESQL_VOLUME_DIR:                /bitnami/postgresql  
	     PGDATA:                               /bitnami/postgresql/data  
	     POSTGRES_PASSWORD:                    <set to the key 'postgres-password' in secret 'postgresql'>  Optional: false  
	     POSTGRESQL_ENABLE_LDAP:               no  
	     POSTGRESQL_ENABLE_TLS:                no  
	     POSTGRESQL_LOG_HOSTNAME:              false  
	     POSTGRESQL_LOG_CONNECTIONS:           false  
	     POSTGRESQL_LOG_DISCONNECTIONS:        false  
	     POSTGRESQL_PGAUDIT_LOG_CATALOG:       off  
	     POSTGRESQL_CLIENT_MIN_MESSAGES:       error  
	     POSTGRESQL_SHARED_PRELOAD_LIBRARIES:  pgaudit  
	   Mounts:  
	     /bitnami/postgresql from data (rw)  
	     /dev/shm from dshm (rw)  
	     /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mg749 (ro)  
	Conditions:  
	 Type              Status  
	 Initialized       True    
	 Ready             True    
	 ContainersReady   True    
	 PodScheduled      True    
	Volumes:  
	 data:  
	   Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)  
	   ClaimName:  data-postgresql-0  
	   ReadOnly:   false  
	 dshm:  
	   Type:       EmptyDir (a temporary directory that shares a pod's lifetime)  
	   Medium:     Memory  
	   SizeLimit:  <unset>  
	 kube-api-access-mg749:  
	   Type:                    Projected (a volume that contains injected data from multiple sources)  
	   TokenExpirationSeconds:  3607  
	   ConfigMapName:           kube-root-ca.crt  
	   ConfigMapOptional:       <nil>  
	   DownwardAPI:             true  
	QoS Class:                   Burstable  
	Node-Selectors:              <none>  
	Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s  
	                            node.kubernetes.io/unreachable:NoExecute op=Exists for 300s  
	Events:  
	 Type    Reason     Age    From               Message  
	 ----    ------     ----   ----               -------  
	 Normal  Scheduled  6m3s   default-scheduler  Successfully assigned vitaliy/postgresql-0 to p-01  
	 Normal  Pulling    6m3s   kubelet            Pulling image "docker.io/bitnami/postgresql:15.1.0-debian-11-r0"  
	 Normal  Pulled     5m41s  kubelet            Successfully pulled image "docker.io/bitnami/postgresql:15.1.0-debian-11-r0" in 21.089350365s  
	 Normal  Created    5m41s  kubelet            Created container postgresql  
	 Normal  Started    5m41s  kubelet            Started container postgresql





Подробная статья по установке и настройке postgresql с постоянным томом
https://phoenixnap.com/kb/postgresql-kubernetes


