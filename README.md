# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 1»

### Цель задания

В тестовой среде Kubernetes необходимо обеспечить доступ к приложению, установленному в предыдущем ДЗ и состоящему из двух контейнеров, по разным портам в разные контейнеры как внутри кластера, так и снаружи.

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым Git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) Deployment и примеры манифестов.
2. [Описание](https://kubernetes.io/docs/concepts/services-networking/service/) Описание Service.
3. [Описание](https://github.com/wbitt/Network-MultiTool) Multitool.

------

### Задание 1. Создать Deployment и обеспечить доступ к контейнерам приложения по разным портам из другого Pod внутри кластера

1. Создать Deployment приложения, состоящего из двух контейнеров (nginx и multitool), с количеством реплик 3 шт.

**kubectl apply -f deployment.yaml**

<img width="502" alt="deployment" src="https://github.com/user-attachments/assets/cf0d060a-5508-4b3c-bf42-28d7cd5cd98a">

2. Создать Service, который обеспечит доступ внутри кластера до контейнеров приложения из п.1 по порту 9001 — nginx 80, по 9002 — multitool 8080.

**kubectl apply -f service-dep.yaml**

<img width="453" alt="service" src="https://github.com/user-attachments/assets/40715554-cb39-4ab2-8ef6-72dfdb42e33d">

3. Создать отдельный Pod с приложением multitool и убедиться с помощью `curl`, что из пода есть доступ до приложения из п.1 по разным портам в разные контейнеры.

**kubectl apply -f pod-multitool.yaml**

<img width="691" alt="pod" src="https://github.com/user-attachments/assets/f3212850-e047-47ac-9d86-f6900c5f83a9">

<img width="665" alt="curl1" src="https://github.com/user-attachments/assets/2ac030af-6064-4eae-b492-348a4cabb338">

<img width="561" alt="curl2" src="https://github.com/user-attachments/assets/e683d365-2341-4e4c-ac22-3e5418fe5483">

<img width="525" alt="curl3" src="https://github.com/user-attachments/assets/a7603e11-fd42-42ec-b5ae-adb7f6b5fe28">

<img width="713" alt="curl 6080" src="https://github.com/user-attachments/assets/bd8e0b81-3db9-4c55-b8da-0454dcaa2bfc">

*поменял на 8080, скрины идентичные будут на 8080

4. Продемонстрировать доступ с помощью `curl` по доменному имени сервиса.

<img width="629" alt="curl svc by name" src="https://github.com/user-attachments/assets/e56b0c32-19e2-45ea-a1cc-a1e2f3d6afae">

5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

[deployment.yaml](https://github.com/sash3939/Kubernetes4-Network/blob/main/deployment.yaml)

[service-dep.yaml](https://github.com/sash3939/Kubernetes4-Network/blob/main/service-dep.yaml)

[pod-multitool.yaml](https://github.com/sash3939/Kubernetes4-Network/blob/main/pod-multitool.yaml)

------

### Задание 2. Создать Service и обеспечить доступ к приложениям снаружи кластера

1. Создать отдельный Service приложения из Задания 1 с возможностью доступа снаружи кластера к nginx, используя тип NodePort.
2. Продемонстрировать доступ с помощью браузера или `curl` с локального компьютера.
3. Предоставить манифест и Service в решении, а также скриншоты или вывод команды п.2.

------

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl` и скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
