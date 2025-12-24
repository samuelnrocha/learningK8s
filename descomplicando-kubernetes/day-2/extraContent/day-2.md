### O que iremos ver hoje?


Durante a aula de hoje, iremos ver todos os detalhes importantes sobre o menor objeto do Kubernetes, o Pod. Vamos ver desde a criação de um simples Pod, passando por Pod com multicontainers, com volumes e ainda com limitação ao consumo de recursos, como CPU ou memória. E claro, vamos aprender como ver todos os detalhes de um Pod em execução e brancar bastante com nossos arquivos YAML.

### O que é um Pod?

Primeira coisa, o Pod é a menor unidade dentro deum cluster Kubernetes.

Quando estamos falando sobre Pod, precisamos pensar que o Pod é uma caixinha que ontém um ou mais containers. E esses containers que compartilham os mesmos recursos do Pod, como por exemplo, o IP, o namespace, o volume, etc.

Então, quando falamos de Pod, estamos falando de um ou mais containers que compartilham os mesmos recursos, pronto.

### Criando um Pod

Temos basicamente duas formas de criar um Pod, a primeira é através de um comando no terminal e a segunda é através de um arquivo YAML.

Vamos começar criando um Pod através de um comando no terminal.

```bash

kubectl run giropops --image=nginx --port=80

```

### Visualizando detalhes sobre os Pods

Para ver o Pod criado, podemos usar o comando:

```bash

kubectl get pods

```

O comando acima irá listar todos os Pods que estão em execução no cluster, na namespace default.

Sim, temos namespaces no Kubernetes, mas isso é um assunto para outro dia. Por enquando, vamos focar em Pods e apenas temos que saber que por padrão o Kubernetes irá cirar todos os objetos dentro da namespace default se não especificarmos outra.

Para ver os Pods em execução em todas as namespaces, podemos usar o comando:
```bash

kubectl get pods --all-namespaces

```

Ou ainda, podemos usar o comando:

```bash

kubectl get pods -A

```

Agora, se você quiser ver todos os Pods de uma namespace específica, você pode usar o comando:

```bash

kubectl get pods -n <namespace>

```

Por exemplo:

```bash

kubectl get pods -n kube-system

```

O comando acima irá listar todos os Pods que estão em execução na namespace kube-system, que é a namespace onde o Kubernetes irá criar todos os objetos relacionados ao cluester, como por exemplo, os Pods do CoreDNS, do Kube-Proxy, do Kube-Controller-Manager, do Kube-Scheduler, etc.

Caso você queira ver ainda mais detalhes sobre o Pod, você pode pedir para o Kubernetes mostrar os detalhes do Pod em formato YAML, usando o comando:

```bash

kubectl get pods <nome-do-pod> -o yaml

```

Por exemplo:

```bash

kubectl get pods giropops -o yaml

```
