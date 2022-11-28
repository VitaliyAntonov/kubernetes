
команда приведена здесь:

https://serveradmin.ru/rabota-s-helm-3-v-kubernetes/


Kubeapps использует отдельный namespace, создадим его:

	kubectl create namespace kubeapps

Ставим приложение Kubeapps через Helm:

	helm install kubeapps --namespace kubeapps bitnami/kubeapps


Краткое руководство по развертыванию идентичных сред с диаграммами управления в нескольких пространствах имен

https://medium.com/@tomerf/helm-and-namespaces-cce64fcdcced





