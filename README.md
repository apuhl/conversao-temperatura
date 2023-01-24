# Projeto convers√£o de temperatura

### Sobre o projeto
O projeto convers√£o de temperatura √© um projeto desenvolvido em NodeJS. O projeto tem como objetivo ser um exemplo para a cria√ß√£o de ambiente com containers usando NodeJS.

### Observa√ß√µes do projeto
A aplica√ß√£o √© exposta usando a porta 8080

### Criando a imagem Docker
Para criar a imagem docker, seguir conforme o exemplo abaixo

`docker build -t <account>/<repository>:<version> -f Dockerfile src/`

### Deploy no K8S

Para realizar o deploy nessecitamos de um cluster kubernetes, para este exemplo, È utilizado cluster local.

Os passos abaixos utilizam as seguintes ferramentas:

- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [k3d ](https://k3d.io)

As instruÁıes de instalaÁ„o e uso encontram-se nos respectivos sites.

#### Criando cluster

Para criar o cluster K8S, executar o comando abaixo:

`k3d cluster create mycluster -p "80:30000@loadbalancer"`

O comando acima criar· cluster com um nÛ, realizando bind da porta 80 do loadbalancer com a porta 30000 a ser exposta pelo serviÁo.

Para visualizar o cluster podem ser executados os comandos abaixo:

`k3d cluster list`

ou

`kubectl get nodes`

#### Realizando o deploy

Para deploy no kubernetes, fora criado o manifesto `manifests/deployment.yaml`, sendo utilizado no `kubectl` conforme exemplo abaixo:

`kubectl apply -f manifests/deployment.yaml`

Acompanhar a criaÁ„o dos `pods` com o comando

`kubectl get pods`

atÈ que ele esteja com estado ¥RUNNING`, como a linha abaixo:

```
> kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
convert-app-67b78fb586-gwf96   1/1     Running   0          4m25s
```

#### Testando

Acessar o endereÁo `http://localhost` (se modificado o bind do loadbalancer do cluster para porta diferente da 80, especificar conforme exemplo: `http://localhost:<port>`).