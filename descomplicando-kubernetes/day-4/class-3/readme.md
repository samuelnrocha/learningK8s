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

Essa é uma forma de aumentar o número de réplucas do $Pod$ do $nginx$ sem precisar editar o $Deployment$, eu não recomendo, eu prefiro editar o $Deployment$ e fazer o $apply$ novamente, mas isso é uma questão de gosto e organização. Eu não gosto da ideia de ter que ficar fazendo $scale$ no $Deployment$ para aumentar ou dimunuir o número de réplicas do $Pod$ do $nginx$, sem ter isso registrado no $git$, por exemplo.

Alterando o $Deployment$ para 3 réplicas.



```yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec:
  replicas: 3
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

Pronto, você conhece as duas opções de aumentar o número de réplicas do $Pod$ do $nginx$, fique a conta para escolher a que você achar melhor.

Eu vou continuar usando a opção de editar o $Deployment$ e fazer o $apply$ novamente.

```bash

kubectl apply -f nginx-deployment.yaml

```

Vamos verificar o nosso $ReplicaSet$ novamente.

```bash

kubectl get replicasets

```

A nossa saída será parecida com essa.

```bash

NAME                           DESIRED  CURRENT READY  Age
nginx-deployment-6dd8d7cfbd    3        3       3      5m24s 

```

Perceba que o nome do $ReplicaSet$ continua o mesmo, mas o número de réplicas mudou para 3, quando somente alteramos o número de réplicas do nosso $Deployment$, o $ReplicaSet$ permanece o mesmo afinal sua principal função é fazer o gerneciamento das réplucas do $Pod$ do $nginx$.

Agora vamos mudar a versão do nginx para a versão 1.19.2.

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
      - image: nginx:1.19.2
        name: nginx
        resources:
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.25
            memory: 128Mi
```

Vamos aplicar as alterações.

```bash

kubectl apply -f nginx-deployment.yaml

```
