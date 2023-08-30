<h1> EC2, AutoScaling, Lambda e Elastic Beanstalk </h1>

</h2> Sumário </h2>

- [EC2 Launch types / Tipos de compra de instâncias](#ec2-launch-types--tipos-de-compra-de-instâncias)
  - [Sob Demanda (On-Demand)](#sob-demanda-on-demand)
  - [Instâncias Reservadas (Reserved Instances)](#instâncias-reservadas-reserved-instances)
  - [Saving Plans](#saving-plans)
  - [Servidores físicos dedicados](#servidores-físicos-dedicados)
    - [Instâncias dedicadas (Dedicated Instances)](#instâncias-dedicadas-dedicated-instances)
    - [Hosts dedicados (Dedicated Host)](#hosts-dedicados-dedicated-host)
- [Spot Instances](#spot-instances)
- [AWS Auto Scaling Group](#aws-auto-scaling-group)
  - [Regra geral](#regra-geral)
  - [Guias úteis](#guias-úteis)
- [AWS Elastic Beanstalk](#aws-elastic-beanstalk)
- [AWS Lambda](#aws-lambda)

## EC2 Launch types / Tipos de compra de instâncias

### Sob Demanda (On-Demand)

- É a compra de instâncias EC2 padrão, tendo a cobrança sobre demanda (conforme o uso, sendo hora ou segundo)
- Alto custo se usado por longo prazo
- **Sem compromisso de uso** (anos)
- Sem pagamento adiantado
- Aumenta o Diminui a capacidade computacional
- **Útil para**: Workload de curto prazo, validar hipótese, com **pico de uso imprevisível**, testar e experimentar um ambiente

### Instâncias Reservadas (Reserved Instances)

- São um desconto de Faturamento (até 72% de desconto) aplicado ao uso de instâncias on-demand
- Aplicações que exigem capacidade Reservadas
- **Comprometimento de uso** por um período e 1 ou 3 anos
- Possui pagamento adiantado
- **Útil para**: ambiente de produção que foi testado, aplicações que precisam estar em **estado constante**; útil para databases

### Saving Plans

- 72% de desconto comparado a On-Demand
- **Comprometimento de gasto por hora** (1 ou 3 anos)
- 3 formas de pagamentos: antecipado, parcial e sem pagamento antecipado
- **Útil para**: Workloads de longa duração, como em aplicativo em 24x7

### Servidores físicos dedicados

#### Instâncias dedicadas (Dedicated Instances)

- **Hardware dedicado**
- Pode compartilhar o hardware com outras instâncias na mesma conta
- Sem controle sobre o posicionamento da instância
- **Comprometimento** por um período de 3 anos

#### Hosts dedicados (Dedicated Host)

- **Hardware dedicado**, porém oferece uma visibilidade e controle maior sobre como as instâncias são colocadas em um servidor físico, permitindo também que você sempre as implante no mesmo servidor físico ao longo do tempo
- Servidor físico EC2 **exclusivo** ao seu uso, ajuda a cumprir requisitos regulatórios de **Conformidade**
- Fornecem visibilidade de soquetes, núcleos, IDs de Host
- **Comprometimento** por um período de 3 anos
- Pode ser comprado sob demanda de horas
- Se optar por **reversa**: até 70% de desconto em comparação a ON-demand
- **Útil para**: Vincular licenças de software (Windows Server, SQL Server e SUSE Linux Enterprise Server)

## Spot Instances

- Até 90% de desconto comparado a On-Demand
- Terminadas quando o preço do spot, é maior que o preço que você estabeleceu para pagar **(oferta e demanda)**. É como se fosse um leilão de instâncias
- **Terminate** = preço spot da AWS > seu preço
- **Útil para**: Quando se tem uma urgência de grande capacidade computacional, workloads que podem parar e serem iniciados novamente, trabalho em lote, análise de dados, processamento de imagens

## AWS Auto Scaling Group

![EC2 Auto Scaling](./images/svg/compute/ec2autoscaling.svg)

> Utilizado quando se precisa de **Escalabilidade automatizada**: Scale Out (+ instâncias) e Scale In (- instâncias)

![auto scaling group](images/as-basic-diagram.png)

- Pode ser utilizado com o **Elastic Load Balancing** para distribuir o tráfego de acesso às aplicações entre todas as instâncias do EC2 em execução.
- Você cria um `EC2 launch template` para o **Auto Scaling Group** (ASG) além de especificar a VPC e as sub-redes que as instâncias serão executadas.
- É possível também especificar o tipo de compra para as instâncias do EC2, sendo sob demanda spot ou a combinação dos dois.
- Voce pode criar uma **política de escalabilidade** para responder a alarmes adicionais (alarmes do CloudWatch) mesmo quando uma ação de escalabilidade ou substituição de healthy check estiver em andamento, por exemplo adicionar novas instâncias apenas quando uma outra já estiver sido inicializada

### Regra geral

- Você define uma quantidade **mínima, desejável e máxima das instâncias**
- Realiza verificações de integridade (**health checks**), finaliza as instâncias não íntegras (**unhealthy**) e inicia novas instâncias
- Você pode: aumentar conforme a demanda (**Scale Out**) e diminuir quando a demanda diminui (**Scale In**)
- É **gratuito**, você paga apenas sob demanda das instâncias

---

<small>

Você pode definir o que o EC2 Auto Scaling precisa através de uma **configuração de execução**, porém ela não permite o versionamento usando uma configuração de **execução**  criada anteriormente como modelo. Além de não permitir a criação por meio de uma instância do EC2 já existente.

> A AWS recomenda usar um **modelo de inicialização** em vez de uma configuração de execução.

### Guias úteis

- [AWS: Modelos de Execução (Launch Templates)](https://docs.aws.amazon.com/pt_br/autoscaling/ec2/userguide/launch-templates.html)
- [AWS: definição de limites de capacidade para o seu grupo do Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/asg-capacity-limits.html)
- [AWS: políticas de escalabilidade simples e de etapas para o Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-simple-step.html)
- [AWS: políticas de dimensionamento com monitoramento do target para o Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-target-tracking.html)
- [AWS: criação de um grupo do Auto Scaling usando um modelo de inicialização](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html)

</small>

## AWS Elastic Beanstalk

![AWS Elastic Beanstalk](./images/svg/compute/beanstalk.svg)

> É um **serviço gerenciado**, para os desenvolvedores fazerem a implementação (**deploy**) de forma fácil (pode ser escalável - Load Balancing e Escalabilidade) de **aplicações e serviços web**.

---

> Ele permite **implantar e dimensionar** serviços e aplicativos Web desenvolvido em uma linguagem de programação em infraestrutura implantada automaticamente com gerenciamento de capacidade, balanceamento de carga, auto scaling e monitoramento, ele facilita o **provisionamento** e a **conformidade** de um aplicativo

Pode ser usado com várias tecnologias (Python, Ruby, PHP, Node.js, Docker, .NET, JAV) etc

- Ele é um serviço **gerenciado e gratuito**.
- É um **PaaS**
- Upload de código fonte < 512 mb ou upload via URL Bucket S3
- Balanceamento de carga (load balancer)
- Alta disponibilidade (multi-az)
- Auto Scaling Group (ASG)

Para decorar: **beanstalk** se refere ao pé de feijão gigante da história de joão e o pé de feijão, Você **planta** o código e AWS conecta todos os serviços para subir sua aplicação.

## AWS Lambda

![AWS Lambda](./images/svg/compute/lambda.svg)

> Permite que você execute código **sem provisionar (serverless)** ou **gerenciar servidores**, pagando apenas pelo **número de solicitações** e pelo **tempo de computação** que você utiliza

- Serverless (você não se preocupa com o provisionamento de máquinas e servidores)
- AWS Lambda **dimensiona** suas aplicações
- Baixo custo: **Cobrança** por **número de solicitações feitas** e pela **duração** por cada milissegundo que leva para que o código seja executado
- Permite múltiplas linguagens (Go, Java, C#, Python, Ruby, Node.js, APIS, etc)
