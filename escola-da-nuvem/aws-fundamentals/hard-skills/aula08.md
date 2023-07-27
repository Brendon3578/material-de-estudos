<h1> Monitoria, Governança e Melhores Práticas AWS </h1>

<h2> Sumário </h2>

- [AWS CloudTrail](#aws-cloudtrail)
  - [Amazon CloudWatch x AWS CloudTrail](#amazon-cloudwatch-x-aws-cloudtrail)
- [AWS Config](#aws-config)
- [AWS Organizations](#aws-organizations)
- [Well Architected Framework](#well-architected-framework)
  - [Princípios do Design](#princípios-do-design)
  - [6 pilares Well-Architected](#6-pilares-well-architected)
- [AWS Artifact (Acordos e Relatórios de Conformidade)](#aws-artifact-acordos-e-relatórios-de-conformidade)
- [AWS Trusted Advisor](#aws-trusted-advisor)

## AWS CloudTrail

![Cloud Trail](images/svg/management_governance/cloudtrail.svg)

> É um serviço que possibilita **governança, conformidade, auditoria operacional** e **auditoria de riscos** em sua conta AWS

É utilizado para apenas para auditoria e conformidade, quem fêz o quê na AWS (quem apagou, criou, ou parou uma instância)

### Amazon CloudWatch x AWS CloudTrail

- `CloudWatch`: para monitorar **Performance e Desempenho** de recursos
  - Usado para monitorar o desempenho dos recursos ao longo do tempo através de logs e relatórios diante das métricas definidas
  - Visualização através de uma dashboard

- `CloudTrail`: para efetuar **Auditoria e Conformidade**
  - É uma trilha (*trail*), no qual é possível ver os rastros das operações que foram efetuadas dentro do ambiente cloud AWS (que tipo dde operação foi realizada e em que momento, qual o endereço IP de origem, etc)
  - É registrado em um trail log (temporário ou permanente, ambos armazenados em um bucket do S3)
  - Cada trail pode armazenar Events, podendo ser Management events, Data events e Insights events

## AWS Config

![Config](images/svg/management_governance/config.svg)

> Auxilia na auditoria das **alterações dos recursos** para compliance (conformidade) validando as configurações que você define
> Permite **acessar, auditar e avaliar** as configurações dos recursos da AWS

- Acompanhar a linha do tempo das configurações dos recursos
- AWS Config é **Regional**
- Mantém **histórico das alterações** e armazena em um `Bucket S3` para posterior análise e auditoria
- **Notificações** de alterações são enviadas através do `Amazon SNS` e disponibilizadas no **Dashboard** do AWS Config
- Não faz parte do free tier

## AWS Organizations

![Organization](images/svg/management_governance/organizations.svg)

> Usado para **gerenciar e controlar** seu ambiente de modo centralizado (várias contas AWS e consolidar faturamento)

Permite que você:

- Gerenciar contas filhas
- [**Consolidar Faturamento**](./extra/consolidated-billing.md)
- **Agregar** preços
- **Gerar economia** com pooling de instâncias reservadas
- **Utilizar** de Service Control Police (política de controle de serviço) para colocar restrições nas contas

- É um **serviço Global**
- Permite **gerenciar** múltiplas contas AWS
- Há uma conta principal (**Master Account**) para gerenciar as outras contas AWS
- API disponível para **criação de contas**
- Restrição das contas usando SCP (**Service Control Police**)

## Well Architected Framework

> Significa seguir as boas práticas estabelecidas pelos engenheiros AWS para que tenha um ambiente prático, seguro e econômico dentro do ambiente cloud AWS

- Parar de ficar **adivinhando a sua capacidade**
- Testar o produto em **escala de produção**
- Automatizar a sua arquitetura para sua **experimentação ser fácil**
- Permitir a **evolução** da arquitetura
- Construir sua arquitetura **baseado em dados**
- **Melhora** através de gamedays
- Utiliza-se da ferramenta `AWS Well-Architected Tool` para revisar as cargas de trabalho, comparando com as melhores práticas da arquitetura AWS

### Princípios do Design

- **Escalabilidade**: vertical & horizontal
- **Recursos descartáveis**: nada é para sempre (projetar o sistema sendo desacoplados)
- **Automação**: serverless, IaaS, autoscaling
- **Loose couple**: falhas não podem cascatear & não ao monólito
- **Serviços não Servidores**: será que não tem um serviço para isso?

### 6 pilares Well-Architected

1.**Operational Excellence**: executar e monitorar para entregar valor
2. Security: proteger informações e sistemas
3. **Reliability**: garantir que uma carga de trabalho execute sua função pretendida corretamente e de modo consistente
4. **Performance Efficiency**: uso eficiente de recursos e computação
5. **Cost Optimization**: compreensão e controle de onde o dinheiro está sendo gasto, ajustando os recursos e serviços
6. **Sustainability**: (novo na AWS) Reflete sobre o modelo de responsabilidade compartilhada para sustentabilidade

## AWS Artifact (Acordos e Relatórios de Conformidade)

![Artifact](./images/svg/security-identity-compliance/artifact.svg)

> Gerar relatórios dentro de um padrão oficial (artefatos de conformidade - compliance), por exemplo ISO

- Os documentos são chamados de **artefatos**
- Os relatórios de security e compliance, são `ISO`, `PIC` e `SOC`
- Os acordos de uso de serviços (agreements), são `BAA` e `HIPAA`
- São utilizado em **auditorias** internas e **conformidade**

## AWS Trusted Advisor

![Trusted Advisor](./images/svg/security-identity-compliance/trusted-advisor.svg)

> É o "conselheiro do poderoso chefão". Esse conselheiro de confiança faz recomendações que ajudam a seguir as **boas práticas da AWS**

- É um serviço Global
- É possível através das verificações, configurar e-mails para serem notificados semanalmente, separando os destinatários por (contato de faturamento, operações e segurança)
- O plano do AWS Support **Basic** e **Developer** oferece suporte para o AWS Trusted Advisor apenas para:
  - Segurança
  - Limites de Serviço
- Permitidos apenas para o plano do AWS Support: **Business**, **Enterprise On-Ramp** e **Enterprise**:
  - Segurança
  - Limites de Serviço
  - Otimização de Custos
  - Desempenho
  - Tolerância a falhas

Com ele é possível verificar:

- Segurança
  - Grupos de seguranças que tem portas específicas sem restrição
  - Se há o MFA na conta `root`
  - Permissões de buckets do S3 que são de acesso aberto
    - > Buckets políticas abertas cria possíveis brechas de segurança, o que ocasionará futuramente um aumento nos custos se haver acessos indesejados.
  - Se há pelo menos um usuário do IAM criado para a conta AWS
- Otimização de custos (Business, Enterprise)
  - Load balancers ociosos ou instâncias EC2 subutilizadas
  - Savings Plans, verificando o uso de serviços computacionais (EC2) e fornecendo recomendação na compra de um Saving Plans
- Desempenho (Business, Enterprise)
  - Otimização de entrega de conteúdo do CloudFront
- Tolerância a falhas (Business, Enterprise)
  - Backups do Amazon RDS
  - Recursos do grupo Auto Scaling
  - Implantações Multi-AZ do Amazon RDSD
