### O que iremos ver hoje?

Hoje é dia de falar sobre dois objetos muito importantes no Kubernetes, os $ReplicaSets$ e os $DaemonStes$.

Nós já sabemos o que é um $Deployment$ e também já sabemos o que é um $Pod$ no detalhe, então agora vamos conhecer essas duas fituras eque estão super conectadas com o $Deployment$ e com o $Pod$. Quando falamos sobre $Deployment$ é impossível não falar sobre $ReplicaSet$, pois o $Deployment$ é um objeto que cria um $ReplicaSet$ e o $ReplicaSet$ é um ojbeto que cria um $Pod$, veja que tudo está conectado.

Jà que o nosso querido $DaemonSet$ é um objeto que cria um $Pod$ e esse $Pod$ é um objeto que fica rodando em todos os nodes do cluester, super improtnate para nós, pois é com $DaemonSet$ que nós conseguimos garantir que teremos pelo menos um $Pod$ rodando em cada node do cluster. Por exemplo, imagine que você precisa isntalar os agentes do $Datalog$ ou ainda um $exporter$ do $Prometheus$ em todos os nodes do cluster, para isso você precisa de um $DaemonSet$.

Ainda no dia de hoje, nós iremos aprender como garantir que os nossos $pods$ estão rodando corretamente, através das $Probes$ do Kuberenetes.

Nós vamos falar sobre $Readiness Probe$, $Liviness Proble$ e $Startup Probe$, e claro mostrando todos os detalhes em exemplos práticos e super explicativos.

Hoje é dia de você aprender sobre esses dois objetos que são super importantes, e ainda, garantir que nós nunca colocaremos os nossos $Pods$ em produção sem antes garantir que eles estão rodando corretamente e sendo checados pelas $Probes$ do Kubernetes.

Bora lá! $VAIIII
