# Amazon Relational Database Service (RDS)

## Banco de Dados gerenciado

O Amazon RDS é um **banco de dados gerenciado**, isso envolve o modelo de responsabilidade compartilhada pois você cuida apenas da **otimização de aplicações**: criação de esquema e de índice, stored procedures, criptografia de dados, controle de acesso e a otimização de consultas.

Caso você decidisse instalar um banco de dados em uma instância EC2, você estaria lidando com um **banco de dados não gerenciado**, ou seja,você além de lidar com a otimização de aplicações, terá que lidar com os backups, alta disponibilidade, escalabilidade, patches de SO e do BD, entre outras configurações.

## Instâncias do RDS

Os mecanismos disponíveis (engine types) são:

- **Open Source**: PostgreSQL, MySQL, MariaDB
- **Comercial**: Oracle, SQL Server,
- **Nativo da AWS**: Amazon Aurora

Com o Amazon RDS você cria uma instâncias de Banco de Dados junto à uma instância EC2 gerenciada pela AWS. Podendo ser das seguintes famílias:

- **Standard**: de uso geral
- **Memory Optimized**: para aplicações que usam muita memória
- **Burstable Performance**: fornece um nível de performance de linha de base com a capacidade de intermitência para o uso total da CPU

Uma instância do BD usa volumes do EBS para armazenamento, podendo ser: Uso Geral (SSD), IOPS provisionadas (SSD), e Armazenamento magnético (não recomendado pela AWS)

## RDS em uma Amazon VPC

### Instâncias em um grupo de sub-rede

- `Grupo de sub-redes de banco de dados`: Quando você cria a instância de um banco de dados RDS, você tem que selecionar uma VPC e as sub-redes que estarão as instâncias
- Para criar um grupo de sub-redes você precisa especificar uma AZ (que estarão as sub-redes) e as sub-redes dessa AZ.
- Essas sub-redes precisam ser privadas (sem rota de um Gateway de Internet)
- É possível usar `Access Control List` (ACL) e `Security Groups` (SG) para definir o tipo de trafego que deseja permitir de acesso à essas instâncias em um nível granular

### Backup de dados

Para backups você pode usar:

- **Backups automáticos**: (0-35 dias) para recuperação point-in-time
- **Snapshots manuais**: para backups maior que 35 dias

### Redundância para Disponibilidade com Multi-AZ

Quando você habilita o Amazon RDS `Multi-AZ`, é criado uma cópia redundante do banco de dados em outra AZ: você acaba com duas cópias: **uma primária** em uma sub-rede em uma AZ e uma **standyby** (não é um BD ativo) em uma sub-rede em outra AZ para funcionar como um **failover automático**.

Esse failover é feito através de um DNS fornecido pela AWS

## Outros Banco de Dados

Além do Amazon RDS há outra ofertas de banco de dados, como:

- **Amazon DynamoDB**: NoSQL para aplicações Web de alto tráfego, sistemas de comércio eletrônico, aplicações de jogos
- **Amazon Document DB** (compatível com MongoDB) para gerenciamento de conteúdo, catálogos e perfis de usuários
- **Amazon Neptune** para banco de dados de grafo, redes sociais e mecanismos de recomendação
- **Amazon QLDB** (Quantum Ledger Data Base) para Banco de dados ledger, útil para sistemas de registro, cadeia de fornecimento, registros e transações bancárias
- **Amazon Timestream**: útil para aplicações IoT, DevOops e telemetria industrial
