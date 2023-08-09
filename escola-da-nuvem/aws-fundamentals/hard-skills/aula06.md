<h1>EBS, Snow Family, Glacier, VPC, DNS e Route 53</h1>

<h2>Sumário</h2>

- [Amazon EBS Elastic Block Store](#amazon-ebs-elastic-block-store)
- [Família AWS Snow](#família-aws-snow)
- [S3 Glacier \& S3 Glacier Deep Archive](#s3-glacier--s3-glacier-deep-archive)
- [Amazon VPC](#amazon-vpc)
  - [Características](#características)
- [AWS Route 53](#aws-route-53)
  - [Características do DNS](#características-do-dns)
  - [Políticas de Roteamento](#políticas-de-roteamento)

## Amazon EBS Elastic Block Store

![Elastic Block Store](./images/svg/storage/ebs.svg)

> É um serviço de **Armazenamento de blocos** (dados) **persistentes** em alta escala fácil, projetado como um **volume** e utilizado como um disco para as instâncias Amazon EC2

- Blocos persistentes (Volume, recomendado para SOs e BDs)
- Proteção por redundância (replicação entre zonas - SLA)
- Diferente tipos de volume (SSD ou HDD)
- Redimensionar em minutos (**on-the-fly**)
- Pago conforme a provisão
- Snapshot (backups) manual ou automático (**point-in-time**) - armazena fotos de tempo em tempo <br> ![Snapshot](./images/svg/storage/ebssnapshot.svg)
- Criptografia em repouso (ver depois e pesquisa sobre criptografia em trânsito)
- Replicado automaticamente em uma **zona de disponibilidade** (precisa estar na mesma zona que a instância)

---

> Os volumes de armazenamento do EBS não podem ser compartilhados entre servidores locais e instâncias EC2, para uma solução de armazenamento de arquivos compartilhado e escalável, usa-se o [Amazon Elastic File System](./extra/amazon-efs.md) (Amazon EFS)

## Família AWS Snow

![Snowcone](./images/svg/storage/snowcone.svg)
![Snowball](./images/svg/storage/snowball.svg)
![Snowmobile](./images/svg/storage/snowmobile.svg)

> É um serviço físico para lugares no qual a rede de internet é precária ou não há infraestrutura, os dados são primeiramente processados em um dos membros da Snow Family e depois são migrados para o ambiente AWS para ser processado

- `Snowcone`
  - **Lugares inóspitos**
  - Portátil
  - 8 TB e têm um poder computacionais
- `Snowball Edge`
  - **Migrar dados em Petabytes**
  - **Storage Optimized**: 100 TB (80 TB disponível), 24vCPU e 32 GB de memória
  - **Compute Optimized**: 42 TB (39,5 TB disponível), 52vCPU, 208 GB de memória e SSD 7.68 TB NVMe
    - Possui poder computacional
  - Criptografia dem 256 bits e são resistentes a violações
- `SnowMobile`
  - **Migrar Exabytes**
  - É um caminhão de armazenamento de 100 PB
  - Região e atendimento limitada
  - Armazenamento local e durável

## S3 Glacier & S3 Glacier Deep Archive

![S3 Glacier](./images/svg/storage/s3gaclier.svg)

> São classes de armazenamento de objetos de **longo prazo**, seguras e **resilientes** do Amazon S3 a partir de 1 USD por terabyte por mês
  
- Armazenamento de **longo prazo**, tendo o **conteúdo imutável** após envio
- Você pode configurar uma regra de ciclo de vida que envia de um bucket S3 Standard para um S3 Glacier (porém contem taxas extras nessas migrações)
- Objetos armazenados dentro do Glacier só podem ser manipulados através do AWS CLI ou AWS Tools e SDKs
- 1 byte até 40 terabyte
- `Glacier Instance Retrieval` 0,004 USD por GB/mês na região NV
- `Glacier Flexible Retrieval` 0,0036 USD por GB/mês na região NV
- `Glacier Deep Archive` 0,00099 USD por GB/mês na região NV
- **Disponibilidade** (SLA) de 99,99%
- **Durabilidade** anual média de 99,99999999%
- Recuperação de até 12 horas
  - Dados recuperados ficam no bucket S3 por 24 horas
  - **Recuperação padrão**: 3 a 5 horas
  - **Recuperação Massa**: 5 a 12 horas
  - **Recuperação Expressa** (< 250mb): 1 a 5 minutos

## Amazon VPC

![Amazon VPC](./images/svg/network_content-delivery/vpc.svg)

> É uma **sessão (rede) isolada logicamente** na nuvem AWS, que permite personalizar uma rede virtual e **executar recursos**, em um ambiente com controle total

- Mesmo **conceito on-premises**
- Total controle na configuração
- Camadas de segurança (SG - security group - & NACLs)
- Conectividade com outros serviços (obtendo granularidade na configuração de serviços e melhor conectividade)

### Características

- Estabelecida em uma **Região** (uma VPC só compõe 1 região) e pode ser dividido em Zonas Disponibilidade
- **Sub-rede Pública** (Tem acesso à internet), usa-se juntamente com o `Internet Gateway` para que recursos se conectem com a internet
- **Sub-rede Privada** (Não tem acesso à internet), usa-se juntamente com o `Nat Gateway` para que recursos da sub-rede privada se conectem à internet, permite que recursos conversem entre si
- **Tabela de Roteamento**: faz a comunicação entre a sub-rede e as instâncias
- `SG` (Security Group): firewall no **nível das instâncias**
- `NACLs` (Network Access List): firewall no nível das **sub-redes**

![exemplo de uma arquitetura VPC](./images/vpc-example.png)

---

> Para uma conexão privada dedicada entre instalações locais da empresa e a Nuvem AWS, usa-se o [AWS Direct Connect](./extra/aws-direct-connect.md).

---

> Explicação dos [procedimentos de como criar uma VPC](./extra/vpc.md)

## AWS Route 53

![Route 53](./images/svg/network_content-delivery/route53.svg)

> É um serviço que atua sendo DNS (Domain Name System) que encaminha as requests (solicitações) dos usuários para os aplicativos da nuvem AWS

- O nome é referência a porta 53 (de DNS)
  - DNS é um conjuntos de regras que ajudam o cliente a chegar ao destino através de uma *friendly* URL

### Características do DNS

- Gerenciamento de DNS
- Gerenciamento de Tráfego
- Monitoramento de Disponibilidade (usando health check)
- Registro de Domínios
- É utilizado através de vários tipos de registros DNS (DNS Record Types): A, CNAME, AAAA, ALIAS

### Políticas de Roteamento

Definem como o Route 53 responde a consulta de DNS. Oferece as seguintes políticas:

- **Simple Routing Policy**: encaminhar trafego para um único recurso (sem health check)
- **Weighted Routing Policy** (ponderado): Encaminhar o tráfego para vários recursos nas proporções que você define (%) (sem health check)
- **Latency Routing Policy**: Encaminhar o tráfego para o recurso com menor latência (mais próximo) (possui health check)
- **Failover Routing Policy**: Redirecionar quando há failover, redireciona para uma instância primária se falhar devido ao health check, é redirecionado à uma instância failover (healthy)
- **GeoLocation Routing Policy**: (por região) Encaminhar tráfego da internet para seus recursos com base na localização dos usuários (possui health check)
- **Multivalue Answer Routing Policy**: responder a consultas e DNS com até oito critérios selecionados (possui health check)
- **Geoproximity Routing Policy**: Encaminhar tráfego com base na localização dos recursos
- **IP-based Routing Policy**: Para rotear o tráfego com base no local dos usuários e tiver os IPs de origem do tráfego
