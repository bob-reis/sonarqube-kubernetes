# Implementação do Sonarqube no Cluster Kubernetes

## Criando o Namespace
Para implementar o sonarqube no kubernetes, primeiramente você deve criar o namespace, para isto execute

`kubectl apply -f namespace.yaml`

## Criando so Volumes
Após criar o namespace, será necessário criar os volumes para armazenamento dos arquivos, eles são para o Postgresql e 2 para o sonarqube

```
kubectl apply -f volume-postgres-data.yaml
kubectl apply -f volume-sonar-data.yaml
kubectl apply -f volume-sonar-extensions.yaml
```

## Requisitando os Volumes

Agora é necessário requisitar os volumes

```
kubectl apply -f Persistent-Volume-Claim-PG-data.yaml
kubectl apply -f Persistent-Volume-Claim-Sonar-data.yaml
kubectl apply -f Persistent-Volume-Claim-Sonar-Extensions.yaml
```

## Criando o Banco de Dados

Implementando a instancia do PostgreSQL

`kubectl apply -f postgresql.yaml`

## Criando o Sonarqube

Implementando a instancia do Sonarqube

`kubectl apply -f sonarqube.yaml`

## Publicando o Serviço do Load Balancer

Para publicar o serviço, basta aplicar o arquivo

`kubectl apply -f service.yaml`

## Verificando as implementações

Para ver se todos os serviços estão ativos

`kubectl get pods -n <namespace>`

Para ver o endereço externo do sonarkube

`kubectl get services -n <namespace>`

## Acessando pela primeira vez o Sonarqube

https://<endereço dns externo obtido do service>:9000

User: admin
Pass: admin

Será solicitada a troca da senha

