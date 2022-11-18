
[kube-proxy](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/) — сетевой прокси, работающий на каждом узле в кластере, и реализующий часть концепции [сервис](https://kubernetes.io/docs/concepts/services-networking/service/).

kube-proxy конфигурирует правила сети на узлах. При помощи них разрешаются сетевые подключения к вашими подам изнутри и снаружи кластера.

kube-proxy использует уровень фильтрации пакетов в операционной системы, если он доступен. В противном случае, kube-proxy сам обрабатывает передачу сетевого трафика.

