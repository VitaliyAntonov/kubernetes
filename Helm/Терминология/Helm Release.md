
Что такое релиз, информация отсюда:
https://habr.com/ru/company/dataart/blog/588258/

Helm Release генерируется из чарта (Chart) с использованием входных значений (Values):

Chart + Values = Release

При помощи команды helm list мы можем просмотреть релизы, установленные в конкретном Kubernetes Namespace.

![[Pasted image 20221123192025.png]]

С релизами связано понятие Release backend — места, в котором Helm хранит и версионирует переданные на деплой релизы.

Это может быть configmap/secret/SQL. По умолчанию это secret — Helm создает объект этого типа (в котором хранится JSON, завернутый в gzip + Base64) на каждый релиз в Namespace, куда его и устанавливает. Хотя он может сделать это и, например, в SQL-базе.

![[Pasted image 20221123192155.png]]





