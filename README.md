[![](https://kubedev.io/wp-content/uploads/2020/08/Artboard-1@2x.png)](https://kubedev.io/wp-content/uploads/2020/08/Artboard-1@2x.png)

## Desafio KubeDev
Agora, você precisa pegar o projeto do desafio 01 - o conversão temperatura (Questão 3 - https://github.com/KubeDev/conversao-temperatura) e rodar no Kubernetes. (Coloca aqui embaixo o seu repositório com o Dockerfile e os manifestos).


## Requisitos 

- Docker
- K3D
- Kubectl

## Executando o projeto

Executando o projeto
```bash
git@github.com:carlosmendesrv/conversao-temperatura-kubernetes.git
```

Criando Cluster com 3 agentes e 3 servers
```
k3d cluster create cluster-temperatura --agents 3 --servers 3 -p "8080:30000@loadbalancer"
```

Para realizar o Deploy da aplicação, vamos execlutar o arquivo deployment

```
kubectl apply -f src/k8s/deployment.yaml
```
Para verificar sua estrutura do kubernetes, podemos utilizar
``` 
kubetl get all
```
```
NAME                                         READY   STATUS    RESTARTS   AGE
pod/conversao-temperatura-699565c7d5-b22l2   1/1     Running   0          7m57s
pod/conversao-temperatura-699565c7d5-q85kq   1/1     Running   0          7m49s

NAME                            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/conversao-temperatura   NodePort    10.43.89.166   <none>        80:30000/TCP   9m36s
service/kubernetes              ClusterIP   10.43.0.1      <none>        443/TCP        77m

NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/conversao-temperatura   2/2     2            2           9m37s

NAME                                               DESIRED   CURRENT   READY   AGE
replicaset.apps/conversao-temperatura-699565c7d5   2         2         2       7m57s
replicaset.apps/conversao-temperatura-6fc6fc79c8   0         0         0       9m36s
```

O projeto estará disponível na seguinte url http://127.0.0.1:30000
