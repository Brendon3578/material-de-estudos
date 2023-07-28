<h1> Containers na AWS e Serverless </h1>

<h2> Sumário </h2>

- [Containers na AWS](#containers-na-aws)
  - [Amazon Elastic Container Service (ECS)](#amazon-elastic-container-service-ecs)
  - [Amazon Elastic Kubernetes Service (EKS)](#amazon-elastic-kubernetes-service-eks)
  - [Diferença entre ECS e EKS](#diferença-entre-ecs-e-eks)
- [Serverless (sem servidor)](#serverless-sem-servidor)
  - [AWS Fargate](#aws-fargate)
- [AWS Lambda](#aws-lambda)

## Containers na AWS

> Na AWS os containers são executados em instâncias do EC2 (clusters de instâncias EC2). Podendo ter muitas instâncias EC2 em várias AZs por exemplo.

O gerenciamento de containers é chamado de `orquestração`.

### Amazon Elastic Container Service (ECS)

![Elastic Container Service](../images/svg/compute/ecs.svg)

> É um serviço para gerenciar **orquestração de containers** do tipo Docker. Você pode usar para monitorar e automatizar o redimensionamento de clusters de instâncias EC2.

Para usar containers, é necessário instalar o **agente de container** do ECS nas instâncias EC2, que então se irão se chamar **instância de container**

Com as instâncias de container, você pode escalar na horizontal ou vertical, atribuir permissões, reunir requisitos de disponibilidade, saber o estado do cluster, etc.

Para a aplicação ser executada no ECS você cria uma **definição de tarefa** (formato JSON) que descreve 1 ou + containers. O exemplo abaixa é de uma execução realizada no web server Nginx

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

### Amazon Elastic Kubernetes Service (EKS)

![Elastic Kubernetes Service](../images/svg/compute/eks.svg)

> É um serviço para gerenciar **orquestração de containers** Kubernetes, possui um mecanismo de autoscaling

O Kubernetes é outra plataforma para gerenciar e automatizar workloads e serviços de aplicativos em containers.

### Diferença entre ECS e EKS

- Uma instância EC2 com o agente ECS é chamado de `instância de container`. No EKS é chamade `nó de trabalho / worker nodes`
- Container ECS é `tarefa / task`, no EKS é um `pod`
- Enquanto o ECS é nativo do AWS, o EKS é executado sobre o Kubernetes

## Serverless (sem servidor)

A AWS cuida do gerenciamento da infraestrutura subjacente do serviço (sistema operacional, escalabilidade, provisionamento, tolerância a falhas e outros recursos), tendo o desenvolvedor focando apenas na entrega da aplicação e não na implementação

### AWS Fargate

![Fargate](../images/svg/compute/fargate.svg)

> É uma plataforma de computação serverless para ECS ou EKS

## AWS Lambda

- Você cria o código que será executado sendo uma `função` do AWS Lambda que é ativada por um `trigger` (gatilho) que você define (solicitações http, upload no bucket S3, etc)
- O código é executado em um ambiente seguro, isolado e redimensionável gerenciado pelo AWS Lambda
- No máximo 15 minutos de execução
- Cobrado pelo tempo de execução
- Você controla a linguagem que o código será escrito, a quantidade de CPU e memória, dependências, etc.
