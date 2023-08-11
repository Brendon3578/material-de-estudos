# Armazenamento de arquivos

Para armazenamento dr arquivos que pode ser montado em várias instâncias do EC2, pode-se usar o [Amazon Elastic File System](#amazon-elastic-file-system-efs) ou o [Amazon FSx](#amazon-fsx)

Recursos importantes do `Amazon Elastic File System (EFS)` e do `Amazon FSx`:

- Armazenamento de arquivos
- Você paga pelo que usa (sem provisionar armazenamento com antecedência - como acontece com o EBS)
- Ambos podem ser montados em várias instâncias do EC2

## Amazon Elastic File System (EFS)

![Amazon EFS](../images/svg/storage/efs.svg)

> Fornece um `sistema de armazenamento de arquivos (NFS)` elástico e serverless (totalmente gerenciado) que ajuda a compartilhar **dados de arquivos** sem provisionar nem gerenciar a capacidade e a performance do armazenamento

- Pode ser usado com **recursos locais** e da **própria AWS**, criado com o propósito para demanda de petabytes sem interromper aplicações
- Com ele, é reduzido os sistemas de arquivos, eliminando a necessidade de provisionar e gerenciar a capacidade para acomodar o crescimento
- Você pode criar **sistemas de arquivos acessíveis** a instâncias do `EC2`, serviços de containers da Amazon (`ECS`, `EKS`, E `AWS Fargate`) e funções do `AWS Lambda` por meio de uma interface de sistema de arquivo

## Amazon FSx

> Ele é utilizado para executar **sistema de arquivos** de forma escalável com **alta performance** dentro da AWS

### Casos de uso

- Migrar workloads e sistemas de arquivos para a nuvem
- Adota o modelo de `Infraestrutura como Código` para Aumentar a agilidade de desenvolvimento e teste

### Para Windows File Server

> Servidor de arquivo gerenciado integrado ao Windows Server que oferece suporte ao protocolo SMB

### Para Lustre

> Servidor de arquivo Lustre totalmente gerenciaddo que se integra ao S3
