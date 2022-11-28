
https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/

Файл deployment.yaml (консоль открыта в папке с этим файлом)

![[Pasted image 20221121234429.png]]

Установка:

	kubectl apply -f ./deployment.yaml -n=vitaliy

Проверки:

	kubectl get deployment -n=vitaliy

	kubectl get pods -n=vitaliy

	kubectl get pods -l app=nginx -n=vitaliy

	kubectl describe pods

	kubectl describe deployment nginx-deployment -n=vitaliy

	kubectl describe pod nginx-deployment-7bcddbd866-bxqd2 -n=vitaliy

	kubectl describe pod/nginx-deployment-7bcddbd866-bxqd2 -n=vitaliy




