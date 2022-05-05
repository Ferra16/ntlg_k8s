# ntlg_k8s


Ответить на вопросы: 
● Что такое k8s?: Открытое ПО для автоматизации развертывания, управления и масштабирования контейнезированными приложениями;
● В чём преимущество контейнеризации над виртуализацией?: Дешевизна, т.к. запускается только то что необходимо для работы, а не полноценные операционные системы;
● В чём состоит принцип самоконтроля k8s?: в автоматическом режиме осуществляется контроль состояния и перезапуск контейнеров;
● Как вы думаете, зачем Вам понимать принципы деплоя в k8s?: Понимать принципы необходимо для организации работы;
● Какое из средств управления секретами наиболее распространено в использовании совместно с k8s?: Вероятно, Hashicorp Vault
● Какие типы нод есть в k8s, каковы их базовые функции? Макстер ноды: etcd - распределенное хранилище данных, API server - центральный компонент (аутентификация и авторизация), controlelr manager - контроль узлов, сбор мусора и тд, планировщик - отслеживает созданные ноды без привязанного узла и выбирает узел на котором они должны работать ; рабочие узлы: Kubelet - агент работающий на каждом узле, отдает команды Docker daemon, создает Pod и следит за их состоянием, Kube-proxy - конфиругирует правила сети на узлах, Среда выполнения контейнера (Docker), 

apiVersion: v1
kind: Deployment
metadata:
  name: netology-ml
spec:
  replicas: 2
  selector:
    matchLabels:
      app: ntlg
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: ntlg
    spec:
      containers:
        - image: tomcat:8.5.69
          name: tomcat
          ports:
            - containerPort: 8080
