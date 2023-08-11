# Procedimento de como criar uma VPC

Para criar uma Virtual Private Cloud é necessário:

- Especificar um Nome para a VPC
- Especificar uma região - por exemplo `us-west-2` - que abrangerá várias AZ dentro da região selecionada
- Um intervalo IP (CIDR)

Para criar uma sub-rede (semelhante à uma VLAn)

> Uma sub-rede é util para agrupar recursos com base em eles serem acessados publicamente (acesso à internet - Internet Gateway) ou de forma privada

- É necessário que esteja alocado em uma VPC - por exemplo em uma VPC `10.1.0.0/16`
- Especificar uma AZ (zona de disponibilidade) - por exemplo `us-west-2a` ou `us-west-2b`
- Intervalo IP específico (sub conjunto do intervalo de IP da VPC) - por exemplo `10.1.0.0/24`

Pode ser criado uma sub-rede pública (para recursos que podem ser acessados publicamente) e uma privada
Para que uma VPC se conecte com a internet é necessário ter um `Internet Gateway` (é como se fosse um modem)

Para que uma VPC se conecte com um ambiente **On-premisses** de uma empresa/data-center, é necessário ter um `Virtual Private Gateway` (VGW) se conectando via VPN (virtual private network)

## Tabela de roteamento

Quando vc cria uma VPC, a AWS cria também uma **tabela de rotas principal** que permite o tráfego entre todas as sub-redes na rede do VPC (tráfego de target `local`)

- Uma tabela de rotas é um conjunto de regras (rotas) que determina o local que o tráfego será redirecionado
- Tem a funcionalidade de permitir o trafego entre recursos que estão dentro de uma sub-rede
- Ela é composta de dois componentes principal
  - `Destination`: Intervalo de endereços IP que o trafego será direcionado
    - Pode ser `0.0.0.0/0` para levar e entregar tráfego de qualquer lugar
  - `Target`: é o alvo no qual o trafego será redirecionado (na **tabela de rotas principal** é o *local*)
    - Pode ser um `Internet Gateway` para permitir o acesso da sub-rede, que futuramente será associada, à internet
    - Por exemplo `local`, que todas as tabelas de rotas possuem, permitindo o acesso da sub-rede entre outras sub-redes

## Segurança na VPC

Para se ter segurança no acesso dentro da VPC usa-se dois recursos: **Access Control List (ACLs)** que são lista de controle de acesso e **Security Group (SG)** que são grupos de segurança no nível de instâncias

### Access Control List

> Através das ACLs você define **regras de entrada e regras de saída** (de tráfego) no nível das sub-redes

- Tudo é permitido por padrão
- Usa para **permitir (allow)** ou **negar (deny)**: **Todo o tráfego** ou tráfegos: HTTP, HTTPS, TCP, UDP, SSH
- São state-less (sem estado)

### Security Group

> Através dos **SGs** você pode permitir regras de acesso no nível das instâncias

- Tudo é bloqueado por padrão (não há nenhuma regra de acesso de entrada, ou seja só pode ser usadas regras de permissão)
- Em um servidor web permite-se **regras de entrada** de tráfego http (porta 80) e https (porta 443)
- São recursos state-ful (com estado) - se lembraram de uma conexão que foi iniciada originalmente de instância EC2 ou de fora

Um padrão de design comum é organizar recursos em diferentes grupos e criar SGS para cada um controlar a comunicação de rede entre eles: Um SG de camada da Web (https), um SG da aplicação (http) e outro SG para o banco de dados (porta tcp 3306 mysql)
