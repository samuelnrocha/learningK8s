### O Deployment e o ReplicaSet

Vamos criar um $Deployment$ com o nome de $nginx-deployment$ e vamos criar 3 réplicas do $Pod$ do $nginx$.

```yaml

apiVersion: apps/v1
kind: Deployment
metadata: 
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec: 
  replicas: 1
  selector: 
    matchLabels: 
      app: nginx-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: nbginx-deployment
    spec: 
      containers:
      - image: nginx:
        name: nginx
        resources: 
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.25
            memory: 128Mi
```

Vamos visualizar o $Deployment$ que foi criado.

```bash

kubectl get deployments

```

A nossa saída será parecida com essa.

```bash

NAME                Ready  Up-To-Date Available  Age
nginx deployment    1/1    1          1          7s

```

Simples, eu nós já sabiamos! Jeferson, eu quero saber sobre o $ReplicaSet$!

Calma, pois o nosso querido $Deployment$ já criou o $ReplicaSet$ para nós.

Vamos visualizar o $ReplicaSet$ que foi criado.

```bash

kubectl get replicasets

```

A nossa saída será parecida com essa.

```bash

NAME                           Ready  Up-To-Date Available  Age
nginx-deployment-6dd8d7cfbd    1/1    1          1          7s

```

Um coisa importante de observar na saída acima é que o $ReplicaSet$ tem o mesmo nome do $Deployment$ seguido de um sufixo aleatório, e ainda nessa saída podemos saber que o $ReplicaSet$ atualmente tem 1 répuca do $Pod$ do $Nginx$ rodando, de acordo com o que nós definimos no $Deployment$.

Vamos aumentar o número de réplicas do $Pod$ do $nginx$ para 3.

```bash

kubectl scale deployment nginx-deployment --replicas=3

```

Essa é uma forma de aumentar o número de réplucas do $Pod$ do $nginx$ sem precisar editar o $Deployment$, eu não recomendo, eu prefiro editar o $Deployment$ e fazer o $apply$ novamente, mas isso é uma questão de gosto e organização.
