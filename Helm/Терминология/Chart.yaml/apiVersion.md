
Версия API chart (обязательно)


Поле `apiVersion`должно быть предназначено `v2`для диаграмм Helm, для которых требуется как минимум Helm 3. Для диаграмм, поддерживающих предыдущие версии Helm, `apiVersion`установлено значение `v1`Helm 3, которое по-прежнему можно установить.

Изменения с `v1`  на  `v2`  :

-   Поле `dependencies`, определяющее зависимости графиков, которые для графиков находились в отдельном `requirements.yaml`  файле `v1`  (см. [Зависимости](https://helm.sh/docs/topics/charts/#chart-dependencies) графиков ).
-   Полевые `type`, различительные прикладные и библиотечные диаграммы (см. [Типы диаграмм](https://helm.sh/docs/topics/charts/#chart-types) ).






