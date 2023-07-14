<h1> EC2, AutoScaling, Lambda e Elastic Beanstalk </h1>

</h2> Sumário </h2>

- [EC2 Launch types](#ec2-launch-types)
  - [Sob Demanda (On-Demand)](#sob-demanda-on-demand)
  - [Instâncias Reservadas (Reserved Instances)](#instâncias-reservadas-reserved-instances)
  - [Saving Plans](#saving-plans)
  - [Dedicated Host](#dedicated-host)
  - [Dedicated Instances](#dedicated-instances)
  - [Spot Instances](#spot-instances)
- [AWS Auto Scaling Group](#aws-auto-scaling-group)
  - [Regra geral](#regra-geral)
- [AWS Elastic Beanstalk](#aws-elastic-beanstalk)
- [AWS Lambda](#aws-lambda)

## EC2 Launch types

### Sob Demanda (On-Demand)

- Alto custo se usado por longo prazo
- Cobrança sobre demanda (hora ou segundo)
- **Sem compromisso de uso** (anos)
- Sem pagamento adiantado
- Aumenta o Diminui a capacidade computacional
- **Útil para**: Workload de curto prazo, validar hipótese, com **pico de uso imprevisível**, testar e experimentar um ambiente

### Instâncias Reservadas (Reserved Instances)

- 72% de desconto comparado a On-Demand
- Aplicações que exigem capacidade Reservadas
- **Comprometimento de uso** (1 ou 3 anos)
- Com pagamento adiantado
- **Útil para**: ambiente de produção que foi testado, aplicações que precisam estar em **estado constante**; útil para databases

### Saving Plans

- 72% de desconto comparado a On-Demand
- **Comprometimento de gasto por hora** (1 ou 3 anos)
- 3 formas dde pagamentos: antecipado, parcial e sem pagamento antecipado
- **Útil para**: Workloads de longa duração, como em aplicativo em 24x7

### Dedicated Host

- Hardware dedicado
- Servidor físico EC2 **exclusivo**
- Cumprir requisitos de conformidade
- Visibilidade de soquetes, núcleos, IDs de Host
- **Comprometimento** por um período de 3 anos
- Pode ser comprado sob demanda de horas
- Se optar por **reversa**: até 70% de desconto em comparação a ON-demand
- **Útil para**: Vincular licenças de software (Windows Server, SQL Server e SUSE Linux Enterprise Server)

### Dedicated Instances

- **Hardware dedicado**
- Pode compartilhar o hardware com outras instâncias na mesma conta
- Sem controle sobre o posicionamento da instância
- **Comprometimento** por um período de 3 anos

### Spot Instances

- Até 90% de desconto comparado a On-Demand
- Terminadas quando o preço do spot, é maior que o preço que você estabeleceu para pagar
- É como se fosse um leilão de instâncias
- **Terminate** = preço spot da AWS > seu preço
- **Útil para**: Quando se tem uma urgência de grande capacidade computacional, workloads que podem parar e serem iniciados novamente, trabalho em lote, análise de dados, processamento de imagens

## AWS Auto Scaling Group

![EC2 Auto Scaling](./images/svg/compute/ec2autoscaling.svg)

Quando se precisa de **Escalabilidade automatizada**: Scale Out (+ instâncias) e Scale In (- instâncias)

![auto scaling group](images/as-basic-diagram.png)

Pode ser utilizado com o **Elastic Load Balancing** para distribuir o tráfego de acesso às aplicações entre todas as instâncias do EC2 em execução.

### Regra geral

- Você define uma quantidade **mínima, desejável e máxima das instâncias**
- Realiza verificações de integridade (**health checks**), finaliza as instâncias não íntegras (**unhealthy**) e inicia novas instâncias
- Você pode: aumentar conforme a demanda (**Scale Out**) e diminuir quando a demanda diminui (**Scale In**)
- É **gratuito**, você paga apenas sob demanda das instâncias

## AWS Elastic Beanstalk

![AWS Elastic Beanstalk](./images/svg/compute/beanstalk.svg)

É um **serviço gerenciado**, para os desenvolvedores fazerem a implementação (**deploy**) de forma fácil (pode ser escalável - Load Balancing e Escalabilidade) de **aplicações e serviços web**.

Pode ser usado com várias tecnologias (Python, Ruby, PHP, Node.js, Docker, .NET, JAV) etc

- Ele é um serviço **gerenciado e gratuito**.
- É um **PaaS**
- Upload de código fonte < 51 mb ou upload via URL Bucket S3
- Balanceamento de carga (load balancer)
- Alta disponibilidade (multi-az)
- Auto Scaling Group (ASG)

Para decorar: **beanstalk** se refere ao pé de feijão gigante da história de joão e o pé de feijão, Você **planta** o código e AWS conecta todos os serviços para subir sua aplicação.

## AWS Lambda

![AWS Lambda](./images/svg/compute/lambda.svg)

Permite que você execute código **sem provisionar (serverless)** ou **gerenciar serviços**, pagando apenas pelo **número de solicitações** e pelo **tempo de computação** que você utiliza

- Serverless (você não se preocupa com o provisionamento de máquinas e servidores)
- Escalável
- Baixo custo: **Cobrança** por número de solicitações e pela duração por cada milissegundo que leva para que o código seja executado
- Permite múltiplas linguagens (Go, Java, C#, Python, Ruby, Node.js, etc)
