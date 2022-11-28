

Создание пространства имён - namespace

	kubectl create namespace mynamespace


Чткние развёртываний внутри пространства имён

	kubectl get deployment -n=development 

где development  - имя пространства имён