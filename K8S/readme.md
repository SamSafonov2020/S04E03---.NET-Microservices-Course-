https://softchris.github.io/pages/kubernetes-yaml.html

```
apiVersion: apps/v1
kind: Deployment (дипломник)
metadata:
  name: mssql-depl имя в whatsUp. Так как meta это бывший facebook)
spec:
  replicas: 1 (реплика на сцене)
  selector: (селекторное совещание)
    matchLabels: (желтые карточки за матч)
      app: mssql (арбитр)
  strategy:
    type: Recreate      
  template:
    metadata:
      labels:
        app: mssql
    spec:
      terminationGracePeriodSeconds: 30 (Грэйс)
      hostname: mssqlinst (хостел)
      securityContext: (security + конь к.т. пишет текст)
        fsGroup: 10001 ( fs group. Гном(100) и Маг(01))   
      containers: (контейнеры: может быть пищевым пластиковым или 20 тонник)
        - name: mssql (ФИО)
          image: mcr.microsoft.com/mssql/server:2019-latest (Фото)
          ports: (Порты к контейнеру, типа RJ45)
            - containerPort: 1433
          env: (Обслуживаюший персонал)
          - name: MSSQL_PID (Сиквел Пид)
            value: "Developer" (Разработчик)
          - name: ACCEPT_EULA (Ассепт Юля)
            value: "Y" (Y)
          - name: SA_PASSWORD
            valueFrom:
              secretKeyRef: (секретный риф с кием)
                name: mssql
                key: SA_PASSWORD
          volumeMounts: (волуны и горы)
          - mountPath: /var/opt/mssql (путь к горе)
            name: mssqldb (название горы)
      volumes: (волуны, возможно контейнер как якорем привязан к волуну)
      - name: mssqldb (имя)
        persistentVolumeClaim: (персидский вольник Кляйн)
          claimName: mssql-claim (имя Кляйна)
```
```
apiVersion: apps/v1
kind: Deployment (дипломник в опере)
metadata: (имя в whatsUp. Так как meta это бывший facebook)
  name: commands-depl
spec:
  replicas: 1 (реплика на сцене)
  selector: (селекторное совещание, обсуждение)
    matchLabels: (гарчичники)
      app: commandservice 
  template: (кафе, тарелки)
    metadata: (страничка в facebook )
      labels: (отзывы)
        app: commandservice
    spec:
      containers: (контейнеры: может быть пищевым пластиковым)
        - name: commandservice (ФИО)
          image: SamSafonov2020/commandservice:latest (фото)
```

https://habr.com/ru/post/488796/


- **metadata.labels**
Эти поля служат для настройки связей между объектами, а также для их уникальной идентификации. В нашем случае мы отмечаем, что наш деплоймент принадлежит приложению с названием 'microservices' и слою 'gateway'.
Дополнительно хочется отметить похожий по смыслу блок metadata.annotations — он используются исключительно для предоставления метаинформации, которая может быть интроспектирована внешними инструментами.


- **spec.selector.matchLabels**
Этот элемент устанавливает связь между деплойментом и управляемыми подами. Так в нашем случае деплоймент будет управлять только теми подами, у которых есть метка tier, равная 'backend'. Далее в spec.template мы зададим шаблон для создания подов, причем для корректной работы у каждого из них в поле metadata.labels должна быть та же метка, что и здесь.



- **spec.templates.metadata.labels**
Как уже было сказано выше, это поле должно коррелировать с spec.selector.matchLabels, чтобы создаваемые поды могли быть "подхвачены" деплойментом.


Services
--------

Сервис бекенда:
```
apiVersion: v1
kind: Service
metadata:
  labels:
    tier: backend
  name: backend
spec:
  ports:
    - port: 8080
      protocol: TCP
      targetPort: 8080
  selector:
    tier: backend
 ```  
    
- **spec.ports.targetPort** — порт облуживаемых подов, spec.ports.port — выходной порт сервиса. В spec.selector мы указываем, что этот сервис будет направлять запросы подам, имеющим метку tier, равную 'backend'. Так как тип сервиса не указан явно, то он считается равным ClusterIP, и сервис доступен напрямую только изнутри кластера по адресу http://backend:8080.
