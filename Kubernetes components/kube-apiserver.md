Сервер API — компонент Kubernetes [панели управления](https://kubernetes.io/ru/docs/reference/glossary/?all=true#term-control-plane), который представляет API Kubernetes. API-сервер — это клиентская часть панели управления Kubernetes

Основной реализацией API-сервера Kubernetes является [kube-apiserver](https://kubernetes.io/docs/reference/generated/kube-apiserver/). kube-apiserver предназначен для горизонтального масштабирования, то есть развёртывание на несколько экземпляров. Вы можете запустить несколько экземпляров kube-apiserver и сбалансировать трафик между этими экземплярами.

