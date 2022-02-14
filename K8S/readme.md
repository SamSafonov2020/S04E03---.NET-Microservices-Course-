https://softchris.github.io/pages/kubernetes-yaml.html


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
