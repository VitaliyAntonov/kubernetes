https://www.youtube.com/watch?v=s_o8dwzRlu4



всесторонний
практические демонстрации
ноль-к-эксперту

build k8s cluster from scratch  
собрать кластер k8s с нуля

configure and administer k8s cluster
настройка и администрирование кластера k8s

secure and troubleshoot k8s cluster
защищать и устранять неполадки кластера k8s

confidently pass the CKA exam
уверенно сдать экзамен CKA

Официальное описание(определение) Kubernetes
=

Open source container orchestration tool
Инструмент оркестрации контейнеров с открытым исходным кодом

developed by Google
разработано Google

helps manage containerized applications in different deployment environments
помогает управлять контейнерными приложениями в различных средах развертывания

what problems does Kubernetes solve?
какие проблемы решает Kubernetes?

what are the tasks of an orchestration tool?
каковы задачи инструмента оркестровки?

need for container orchestration tool
потребность в инструменте оркестрации контейнеров

Тренд от монолитного к микросервисной архитектуре приложений
расположенных в своих контейнерах

Использование скриптов для управления контейнерами

What features do orhestration tools offer
Какие функции предлагают инструменты оркестрации

hight Availability or no downtime
Высокая доступность или отсутствие простоев

масштабируемомть и производительность

Архитектура
=

Node(узел)  - виртуальная или физическая машина

Control plane

Node    node    node

cubelet - агент основного узла

Control Plane:
- API server = Entrypoint to k8s cluster   Точка входа в кластер k8s
- Controller manager = keeps track of whats happening in the cluster - следит за тем, что происходит в кластере
- Scheduler = ensures Pods placement  -  Планировщик = обеспечивает размещение модулей
- etcd = Kubernetes backing store  -  резервное хранилище Kubernetes

Virtual Network = Creates one unified machine  -  Виртуальная сеть = создает одну унифицированную машину

Worker Nodes    -  Рабочие узлы

higher workload  -  более высокая рабочая нагрузка

much bigger and more resources  -  гораздо больше и больше ресурсов

![[Pasted image 20221114234100.png]]


Видео: https://www.youtube.com/watch?v=NbXV07-62Bs
На русском языке

![[Pasted image 20221116230230.png]]


![[Pasted image 20221116230726.png]]

![[Pasted image 20221116232025.png]]

![[Pasted image 20221116232201.png]]

![[Pasted image 20221116232746.png]]

![[Pasted image 20221116233122.png]]

![[Pasted image 20221116233649.png]]

![[Pasted image 20221116234820.png]]

![[Pasted image 20221116235323.png]]

![[Pasted image 20221116235830.png]]

![[Pasted image 20221117000231.png]]

![[Pasted image 20221117000553.png]]

![[Pasted image 20221117002120.png]]

![[Pasted image 20221117002257.png]]

![[Pasted image 20221117002810.png]]

![[Pasted image 20221117003019.png]]

![[Pasted image 20221117230225.png]]

![[Pasted image 20221117231436.png]]

https://kubernetes.io/ru/docs/concepts/overview/components




