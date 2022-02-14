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
kind: Deployment (дипломник)
metadata: (имя в whatsUp. Так как meta это бывший facebook)
  name: commands-depl
spec:
  replicas: 1 (реплика на сцене)
  selector: (селекторное совещание)
    matchLabels: (желтые карточки за матч)
      app: commandservice (арбитр)
  template:
    metadata:
      labels:
        app: commandservice
    spec:
      containers: (контейнеры: может быть пищевым пластиковым или 20 тонник)
        - name: commandservice (ФИО)
          image: SamSafonov2020/commandservice:latest (фото)
```
