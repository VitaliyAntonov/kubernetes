
Определяем привязанный объём постоянного тома PVC:

	kubectl get pvc -n vitaliy

![[Pasted image 20221128214001.png]]

Просмотр, какие ресурсы будут удалены без фактического удаления

	helm uninstall postgresql --dry-run --namespace vitaliy

Удаляем postgresql:

	helm uninstall postgresql --namespace vitaliy

Проверяем поды в пространстве имён:

	kubectl get pods -n=vitaliy

Определяем привязанный объём постоянного тома PVC  Persistent Volume Claim:

	kubectl get pvc -n vitaliy

Определяем параметры PV Persistent Volume (Постоянное хранилище)

	kubectl get pv -n vitaliy

![[Pasted image 20221128221030.png]]

Удаляем заявку PVC Persistent Volume Claim:

	kubectl delete pvc data-postgresql-0 -n vitaliy

Повторно проверяем PV и PVC после удаления:

![[Pasted image 20221128222511.png]]

Статья по удалению PV Persistent volume  и PVC Persistent volume claim:

### Как удалить PV (Persistent Volume) и PVC (Persistent Volume Claim), застрявшие в завершающем состоянии?

https://jhooq.com/k8s-delete-pv-pvc/



