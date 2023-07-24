<h1> Identidade, Segurança & Computação </h1>

<h2> Sumário </h2>

- [Usuário Root (Raiz)](#usuário-root-raiz)
  - [MFA - Multi-factor Authentication](#mfa---multi-factor-authentication)
- [Identidade - AWS Identity and Access Management](#identidade---aws-identity-and-access-management)
  - [User Groups \& Roles](#user-groups--roles)
  - [Autenticação e Autorização](#autenticação-e-autorização)
  - [Regras gerais](#regras-gerais)
- [Segurança (AWS WAF e AWS Shield)](#segurança-aws-waf-e-aws-shield)
  - [AWS WAF](#aws-waf)
  - [AWS Shield](#aws-shield)
  - [AWS Shield Standard](#aws-shield-standard)
  - [AWS Shield Advanced](#aws-shield-advanced)
- [Computação na AWS](#computação-na-aws)
  - [Elastic Compute Cloud - EC2](#elastic-compute-cloud---ec2)
  - [Tipos de Instâncias do EC2](#tipos-de-instâncias-do-ec2)
  - [Nomenclatura das Instâncias](#nomenclatura-das-instâncias)
- [Bibliografia](#bibliografia)

## Usuário Root (Raiz)

Quando criamos uma conta na AWS pela primeira vez, ele se torna o usuário raiz da conta, tendo acesso á todos os recursos e serviços da conta AWS, qualquer um que tenha acesso a essa conta, possui todos as permissões sobre o ambiente AWS.

É recomendado que não se utilize o user `root` para tarefas administrativas ou diárias, em vez disso, crie outro usuário IAM para administrar cada operação e atribua para ele as políticas necessárias

> Com grandes poderes, vem grandes responsabilidades

É necessário adicionar vários níveis de segurança para bloquear o acesso ao usuário root e proteger a conta AWS.

### MFA - Multi-factor Authentication

É recomendado habilitar o **MFA** (autenticação com multi-fatores) para a conta `root`, podendo ser um dispositivo físico, virtual ou U2F (hardware que conecta a porta USB do computador), para a maior proteção e segurança da conta

## Identidade - AWS Identity and Access Management

![AWS IAM](./images/svg/security-identity-compliance/iam.svg)

Usa-se o serviço de IAM (**Identity and Access Management**) do AWS, que é um serviço global, para gerenciar ***quem*** (**autenticação**) têm acesso a ***o que*** (**autorização**)

### User Groups & Roles

- **Usuários (Users)**: representa uma pessoa ou um serviço que interage com a AWS, tendo credenciais **permanentes**.
  - Não compartilhe o user `root`
  - Use o `least privilege` (privilégio mínimo)
- **Grupos (Groups)**: Coleção de usuários que permite os usuários herdarem as permissões atribuídas ao grupo.
  - Não podem ser aninhados (estar dentro do outro).
- **Funções (Roles)**: Não são permissões, é uma método de autenticação **temporária**, geralmente atribuído para serviços e recursos. Sendo assumidas programaticamente, elas expiram e são alternadas, rotacionando automaticamente
  - Toda comunicação na AWS é feita via uma API
  - Para estabelecer essa comunicação é necessário uma **função**

### Autenticação e Autorização

Primeiro acontece a autenticação e depois a autorização

- **Autenticação** é você existir no IAM
- **Autorização** é a permissão à acessar ou alterar um recurso atrelado à uma Autenticação (toda chamada de API da AWS tem que ser autenticada e assinada)

- A **Autenticação** no AWS refere-se aos recursos de Usuários, Grupos e Funções, que interage com a **Autorização**, que são as políticas e permissões definidas (policy documents)

As **Políticas e Permissões** (autorização) são definidos através de um `documento JSON`, que define as permissões de acesso podendo permitir ou negar as ações (chamadas de API) de um recurso. Você cria as **polices** e atribui elas a um usuário, recurso ou grupo de usuário.

A política abaixo **permite** que seja possível a listagem de um único bucket do S3 (Simple Storage Service) chamado `example_bucket`

```js
{
  "Version": "2012-10-17", // Define a versão da linguagem da política,
  // Ela especifica as regras de sintaxe de linguagem necessárias para a AWS processar uma política
  "Statement": {
    "Effect": "Allow", // Efeito: Allow ou Deny
    // Action e Resource podem utilizar do carácter curinga (*) que simboliza (all/todos) os recursos ou permissões
    "Action": "s3:ListBucket", // Ação
    "Resource": "arn:aws:s3:::example_bucket" // Objetos que serão afetados pela política
  }
}
```

Outro exemplo, a política abaixo define que o usuário do IAM altere sua própria senha e obtenha informações sobre seu próprio usuário

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1689277490068",
      "Action": [
        "iam:ChangePassword",
        "iam:GetUser"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
    }
  ]
}
```

![Exemplificação do AWS IAM](./images/aws-iam.png)

### Regras gerais

- **Usuários** possuem credenciais **permanentes**
- **Funções** possuem credenciais **temporárias**
- Usuários root **Não** devem ser compartilhados
- Use o `least privilege principle` nos usuários
- **Documentos JSON** definem as permissões dde acesso
- **Grupos** contém outros usuários, mas **Não** podem conter outros grupos

## Segurança (AWS WAF e AWS Shield)

### AWS WAF

![AWS WAF](./images/svg/security-identity-compliance/waf.svg)

> O **AWS WAF** (Web Application Firewall) é um **firewall de aplicativos** que permite especificar qual tráfego tem o acesso permito ou bloqueado, mediante a definição de **regras** personalizadas.

- Filtra o tráfego com regras de `Web Access Control List` WEB ACL, sobre a camada 7 da aplicação (http)
- Bloqueia **SQL injection** (SQLi) e cross-site scripting (XSS)
- **Geo-match** (bloqueio de países), **size constraints** (limitar o tamanho das requisições) e **rate based-rules** (limitar quantidade de requisições por segundo)

### AWS Shield

![AWS Shield](./images/svg/security-identity-compliance/shield.svg)

> É usado pra mitigar (tratar) ataques DDos

O AWS Shield (Standard e Advanced) fornece proteção contra ataques DDoS (negação de serviço distribuído - *Distributed Denial of Service*) e nas camadas de transporte (camada 3 e 4) e na camada da aplicação (camada 7).

Um ataque DDos foca em vários sistemas sobrecarregar um alvo com tráfego.

![Ataque DDoS](./images/ddos.png)

### AWS Shield Standard

- **Gratuito**
- Proteção SYN/UDP Floods, Reflection Attacks
- Proteção de ataques na camada 3 e 4

### AWS Shield Advanced

- **Pago** e oferece Suporte 24x7
- **Proteção extra** em vários serviços como: EC2, Elastic Load Balancing, Amazon CloudFront, AWS Global Accelerator e Route 53

## Computação na AWS

> É mais fácil e rápido de se gerenciar poder computacional e sendo um modelo na nuvem de infraestrutura como serviço.

Um `servidor` é o componente essencial para hospedar uma aplicação, geralmente lidando com **solicitações HTTP** através do modelo client-server. Os servidores hospedam a aplicação fornecendo capacidade de CPU, memória e rede para trabalhar com as solicitações. As opções mais comuns para servidores de HTTP (para Linux) é: Apache, Nginx e Apache Tomcat

Alguns dos serviços de Computação que a AWS oferece é: Elastic Beanstalk, AWS Lambda, AWS Fargate e o mais comum sendo as Máquinas Virtuais do EC2(EC2)

### Elastic Compute Cloud - EC2

![Elastic Compute Cloud](./images/svg/compute/ec2.svg)

> O **Amazon Elastic Compute Cloud** (EC2) é um serviço web que oferece **capacidade computacional**, sendo uma **instância redimensionável** (elástica) na AWS.

- É um Infraestrutura como Serviço (IaaS)
- Você escolhe e modela um **Amazon Machine Image** (AMI) do tipo Windows, MacOS, Ubuntu, Amazon Linux etc
- **Cobrança por hora ou segundo** (mínimo de 60 segundos)
- É composto de outros serviços para ter o seu funcionamento melhorado
  - Você aluga máquinas virtuais - o próprio **EC2**
  - Para armazenar dados em volumes virtuais - com o `EBS - Elastic Block Store`
  - Distribuir cargas de trabalho - com o `ELB - Elastic Load Balancing`
  - Pode escalar o serviço de acordo com a demanda - utilizando `ASG - Auto Scaling Group`

Você pode usar o EC2 com o Elastic Block Storage (EBS) para ter maior controle sobre o armazenamento da VM, que se por acaso a instância do EC2 for  interrompida, o armazenamento não será perdido (bloco de volume `/root`), servindo como um HD externo

### Tipos de Instâncias do EC2

Quando você executa uma instância EC2, a AWS aloca uma VM (que é executada em um hypervisor), e a AMI é copiada para o volume root da VM, contendo a imagem usada para iniciar o volume. Tendo no final o servidor, que você pode instalar pacotes ou softwares adicionais.

![Tipos de Instâncias do EC2](./images/ec2-instance-types.jpg)

<details>
  <summary>Tipos de instâncias</summary>

  <ul>
    <li>T para Turbo (Burstable)</li>
    <li>M para a maioria dos casos (propósito geral) = 1:4 vCPU para RAM</li>
    <li>C para Compute (com a melhor CPU) = 1:2 vCPU para RAM</li>
    <li>R para Random-Access Memory = 1:8 vCPU para RAM</li>
    <li>X para Extra-Large Memory (~4TB DRAM)</li>
    <li>H para HDD (16TB Local)</li>
    <li>D para Dense Storage (48TB Local)</li>
    <li>I para I/O (NVMe Local)</li>
    <li>HS para High Storage</li>
    <li>G para GPU</li>
    <li>P para Performance (High-end GPU)</li>
    <li>F para FPGA</li>
    <li>A para ARM</li>
    <li>Z para High Frequency</li>
    <li>MAC para Mac Mini</li>
  </ul>
</details>

<details>
  <summary>Capacidades Adicionais (additional capabilities)</summary>

  <ul>
    <li>a para AMD CPUs</li>
    <li>b sendo Otimizado para Block Storage</li>
    <li>d para Directly-Attached Instance Storage (NVMe)</li>
    <li>e para Extra Capacity (Storage or RAM)</li>
    <li>g para Processadores Graviton2 (AWS)</li>
    <li>i para Processadores Intel (atualmente Ice Lake)</li>
    <li>n sendo Otimizado para Networking (redes)</li>
    <li>z para High Frequency</li>
  </ul>
</details>

<details>
  <summary>Tamanho das Instâncias (instance sizes)</summary>

  <ul>
    <li>nano, micro, small, medium = 2 vCPUs com 0.5, 1, 2, 4GB RAM (T series only)</li>
    <li>large = 2 vCPUs</li>
    <li>xlarge = 4 vCPUs</li>
    <li>2xlarge = 8, 16xlarge = 64 etc.</li>
  </ul>
</details>

### Nomenclatura das Instâncias

![Nomeação das instâncias do EC2](./images/ec2-names.png)

## Bibliografia

[Meaning of the number in AWS instance type name - Stack Overflow](https://stackoverflow.com/questions/48235393/meaning-of-the-number-in-aws-instance-type-name)
