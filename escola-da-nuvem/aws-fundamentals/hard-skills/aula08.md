<h1> Monitoria, Governança e Melhores Práticas AWS </h1>

<h2> Sumário </h2>

- [AWS CloudTrail](#aws-cloudtrail)
- [AWS Config](#aws-config)
- [AWS Organizations](#aws-organizations)
- [Well Architected Framework](#well-architected-framework)
- [AWS Artifact (Acordos e Relatórios de Conformidade)](#aws-artifact-acordos-e-relatórios-de-conformidade)
- [AWS Trusted Advisor](#aws-trusted-advisor)

## AWS CloudTrail

![Cloud Trail](images/svg/management_governance/cloudtrail.svg)

> É um serviço que possibilita **governança, conformidade, auditoria operacional** e **auditoria de riscos** em sua conta AWS

É utilizado para apenas para auditoria e conformidade, quem fêz o quê na AWS

## AWS Config

![Config](images/svg/management_governance/config.svg)

> Auxilia na auditoria das **alterações dos recursos** para compliance (conformidade) validando as configurações que você define

- AWS Config é **Regional**
- Mantém **histórico das alterações** e armazena em um `Bucket S3` para posterior análise e auditoria
- Notificações de alterações são enviada com o `Amazon SNS` e disponibilizadas no **Dashboard** do AWS Config

## AWS Organizations

![Organization](images/svg/management_governance/organizations.svg)

> Usado para **gerenciar e controlar** seu ambiente de modo centralizado (várias contas AWS e consolidar faturamento)

Permite que você:

- Gerenciar contas filhas
- [Consolidar **Faturamento**](./extra/consolidated-billing.md)
- **Agregar** preços
- **Gerar economia** com pooling de instâncias reservadas
- **Utiliza** do Service Control Police (política de controle de serviço)

- É um serviço Global
- Permite gerenciar múltiplas contas AWS
- Uma conta principal (Master Account)
- API disponível para criação de contas
- Restrição das contas usando SCP (Service Control Police)

## Well Architected Framework

- Parar de ficar **adivinhando a sua capacidade**
- Testar o produto em **escala de produção**
- Automatizar a sua arquitetura para sua **experimentação ser fácil**
- Permitir a **evolução** da arquitetura
- Construir sua arquitetura **baseado em dados**
- Melhora através de gamedays

## AWS Artifact (Acordos e Relatórios de Conformidade)

![Artifact](./images/svg/security-identity-compliance/artifact.svg)

> Gerar relatórios dentro de um padrão oficial (artefatos de conformidade - compliance), por exemplo ISO

- Os documentos são chamados de **artefatos**
- Os relatórios de security e compliance, são `ISO`, `PIC` e `SOC`
- Os acordos de uso de serviços (agreements), são `BAA` e `HIPAA`
- São utilizado em **auditorias** internas e **conformidade**

## AWS Trusted Advisor

![Trusted Advisor](./images/svg/security-identity-compliance/trusted-advisor.svg)

> É o conselheiro do poderoso chefão. Esse "conselheiro de confiança" faz recomendações que ajudam a seguir as **boas prátaicas da AWS**

O plano do AWS Support **Basic** e **Developer** oferece suporte para o AWS Trusted Advisor:

- Segurança
- Limites de Serviço

Permitidos apenas para o plano do AWS Support: **Business**, **Enterprise On-Ramp** e **Enterprise**:

- Otimização de Custos
- Desempenho
- Tolerância a falhas

Com ele é possível verificar:

- Permissões de buckets do S3 que são de acesso aberto
  - Policies de bucket que concedem acesso de listagem a todos, podem resultar em altos custos, pois se usuários indesejados acessarem o bucket, irá aumentar o custo dele. Além disso, buckets com muitas policies abertas cria possíveis brechas de segurança.
- Uso de autenticação multifator (MFA) no usuário `root`
  - Avisa se a conta `root`  está com o MFA desabilitado
