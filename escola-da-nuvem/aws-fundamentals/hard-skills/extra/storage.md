<h1> Tipos de Armazenamento na AWS </h1>

<h2>Sumário</h2>

- [Serviços de Armazenamento](#serviços-de-armazenamento)
  - [Armazenamento de arquivos](#armazenamento-de-arquivos)
- [Armazenamento de blocos](#armazenamento-de-blocos)
- [Armazenamento de objetos](#armazenamento-de-objetos)
  - [Casos de usos](#casos-de-usos)
- [Armazenamento no EC2](#armazenamento-no-ec2)
  - [Volumes do EBS](#volumes-do-ebs)
- [Amazon S3 - Casos de uso, versionamento e Ciclo de vida](#amazon-s3---casos-de-uso-versionamento-e-ciclo-de-vida)
  - [Automatizando transições de camada com gerenciamento do ciclo de vida de objetos](#automatizando-transições-de-camada-com-gerenciamento-do-ciclo-de-vida-de-objetos)
    - [Casos de uso para o gerenciamento de ciclo de vida](#casos-de-uso-para-o-gerenciamento-de-ciclo-de-vida)
- [Anotações extras](#anotações-extras)
- [Data lake x Data warehouse](#data-lake-x-data-warehouse)
- [Links utilitários](#links-utilitários)

## Serviços de Armazenamento

> São agrupados em 3 categorias: **Armazenamento de arquivos**, **armazenamento de blocos** e **armazenamento de objetos**

### Armazenamento de arquivos

É semelhante ao Windows File Explorer, tendo uma hierarquia de arquivos através de pastas e subpastas

## Armazenamento de blocos

Armazenamento em blocos divide arquivos e dados em blocos de tamanho iguais. Cada bloco tem um ID único, armazenado em uma tabela de pesquisa de dados

Um exemplo é o Amazon Elastic Block Storage (EBS)

## Armazenamento de objetos

> Usado para armazenar dados não estruturados, os dados são armazenados de uma forma plana e possuem metadados que ajudam a armazenar e identificar o objeto

Um exemplo comum é o Amazon Simple Storage Service (S3)

### Casos de usos

- Guardar análise de big data
- Data lake - repositório centralizado que armazena dados estruturados e não estruturados

## Armazenamento no EC2

> O armazenamento do EC2 é composto do `Instance Store` (armazenamento de instância) que provê um armazenamento **temporário** em nível de bloco para as instâncias EC2.

### Volumes do EBS

- Para um armazenamento persistente usa-se **volumes EBS**, serve-se como um HD externo de um computador, com você definindo o tamanho de armazenamento do volume (é escalonável).
  - É um recurso zonal e replicado em vários servidores na mesma zona.
- Não pode ser compartilhado ou anexado a várias instâncias  **ao mesmo tempo**
  - Para anexar o mesmo volume EBS à várias instâncias usa-se o EBS Multi-attach
- Para backups do EBS usa-se **snapshots**
- O tipo de volume SSD fornece alta performance para E/S aleatória, enquanto o HDD fornece alta performance para E/S sequencial.
  - **SSD iops provisionadas do** EBS, útil para: NoSQL e BDs relacionais com alta E/S
  - **SSD de uso geral do EBS**, útil para: volumes de boot, aplicações interativas de baixa latência, desenvolvimento e teste
  - **HDD com taxa de transferência otimizada**, útil para big data, data warehouse, processamento de logs
  - **HDD frio**, útil para:  dados menos acessados que precisam de menos varreduras por dia

## Amazon S3 - Casos de uso, versionamento e Ciclo de vida

Ele é utilizado para:

- Backup e armazenamento (pode ser de recurso da própria AWS)
- Hospedagem de mídia (limite do tamanho de objeto de 5 TB)
- Entrega de software (download)
- Data lakes
- Sites estáticos e Conteúdos estático

É possível também habilitar o **versionamento do S3** para manter várias versões de um único objeto no mesmo bucket. Com isso o Amazon S3 gerará um ID de versão exclusivo automaticamente para o objeto.

Os de versionamento do bucket podem ser: `UnVersioned` que é default, `Versioning-enabled` e `Versioning-suspended`

### Automatizando transições de camada com gerenciamento do ciclo de vida de objetos

É possível automatizar o processo de alternar os objetos nas camadas de armazenamento definindo uma **política de ciclo de vida**:

- Podem ser **ações de transição**, que definem quando os objetos devem fazer a transição para outra classe de armazenamento
- Podem ser **ações de expiração**, que definem quando os objetos expiram e devem ser excluídos permanentemente

#### Casos de uso para o gerenciamento de ciclo de vida

- **Logs periódicos**: logs para um intervalo, podendo ser excluídos após uma semana ou um mês
- **Dados com diferentes frequências de acesso**: Você pode fazer a transição de objetos para a classe de armazenamento S3 Standard-IA 30 dias após criá-los ou arquivar objetos para o S3 Glacier um anos após sua criação, para cumprir com requisitos regulatórios

## Anotações extras

## Data lake x Data warehouse

Um `Data lake` é para armazenar quaisquer tipos dados: não relacionais, relacionais, de fontes IoT, sites, apps, mídias sociais, etc. Serve para análises de ML, análises preditivas, etc

Já o `Data warehouse` é util para armazenar dados relacionais de sistemas transacionais, bancos de dados operacionais, e aplicações de linha de negócios. Armazenam dados altamente selecionados (versão central da verdade). Serve para análises de geração de relatório em lote, BI

---

## Links utilitários

[AWS - O que é armazenamento na nuvem?](https://aws.amazon.com/pt/what-is/cloud-storage/)
[AWS - O que é armazenamento de objetos?](https://aws.amazon.com/pt/what-is/object-storage)
