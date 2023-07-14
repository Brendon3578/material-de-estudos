# Containers na AWS

- Um container é um ambiente no qual é possível "empacotar" código e suas dependências.
- Os containers são úteis para hospedar workload, aplicações web, migrações lift and shift, aplicações distribuídas e simplificar ambientes de desenvolvimento, teste e produção.
- O Docker é uma das ferramentas de container mais conhecidas.
- Containers são mais "rápidos" de se projetar que máquinas virtuais, que possuem um sistema operacional, kernel dedicado, instalação de pacotes etc

Na AWS os containers são executados em instâncias do EC2. Podendo ter muitas instâncias EC2 em várias AZs por exemplo

## Elastic Container Service (ECS)

![Elastic Container Service](../images/svg/compute/ecs.svg)

É um serviço para gerenciar **orquestração de containers** do tipo Docker. Você pode usar para monitorar clusters de instâncias EC2.

Para usar containers, é necessário instalar o agente de container do ECS nas instâncias EC2, que então se irão se chamar **instância de container**

Com as instâncias de container, você pode escalar na horizontal ou vertical, atribuir permissões, reunir requisitos de disponibilidade, saber o estado do cluster, etc.

Para a aplicação ser executada no ECS você cria uma definição de tarefa (formato JSON) que descreve 1 ou + containers. O exemplo abaixa é de uma execução realizada no web server Nginx

```json
{
  "family":"webserver",
  "containerDefinitions":[{
    "name":"web",
    "image":"nginx",
    "memory":"100",
    "cpu":"99"
  }],
  "requiresCompatibilities": ["FARGATE"],
  "networkMode":"awsvpc",
  "memory":"512",
  "cpu":"256"
}
```

## Elastic Kubernetes Service (EKS)

![Elastic Kubernetes Service](../images/svg/compute/eks.svg)

O Kubernetes é outra plataforma para gerenciar e automatizar workloads e serviços de aplicativos em containers.

É um serviço para gerenciar **orquestração de containers** Kubernetes

## Diferença entre ECS e EKS

- Uma instância EC2 com o agente ECS é chamado de `instância de container`. No EKS é chamade `nó de trabalho / worker nodes`
- Container ECS é `tarefa / task`, no EKS é um `pod`
- Enquanto o ECS é nativo do AWS, o EKS é executado sobre o Kubernetes

## AWS Fargate

![Fargate](../images/svg/compute/fargate.svg)

É uma plataforma de computação serverless para ECS ou EKS
