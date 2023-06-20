# Introdução à Computação em Nuvem

![Conteúdo](./images/services2.png)

## O que é computação na nuvem

> É a entrega sob demanda de recursos computacionais, através de uma plataforma de serviços via Internet, sem o gerenciamento ativo do usuário

Atualmente as empresas estão migrando para o ambiente cloud. Alguns dos motivos são:

- Reduzir custos
- Reduzir Infraestrutura física (On Premises)
- Economizar dinheiro da corporação
- Por não ter necessidade de fazer suposições na implementação um datacenter
- Despesas variáveis (sob demanda)
- Grandes economias em escala (a nuvem oferece serviços de gestão e faturamento)
- Aumentar a velocidade e agilidade de toda aplicação
- Tornar-se global

Ainda hoje há modelos de turnos de 20/7, no qual ficam monitorando o cloud 24 horas

## Modelos de Computação

Define qual é sua responsabilidade, e qual é do do provedor da nuvem AWS

- Modelo Tradicional: On Premises
- **Infraestrutura como Serviço** (IaaS) para Hospedar: AWS cuida da infraestrutura como um todo (Network, Storage, Servers), com você cuidando do Sistema Operacional, Banco de Dados,
- **Plataforma como Serviço** (PaaS) para Programar: AWS cuida do Sistema Operacional
- **Software como Serviço** (SaaS) para Usar: Você só cuida dos dados que são sendo manipulados pelo sistema

## Escalabilidade e Elasticidade

Exemplo para estudo: No contexto de construir um terreno para moradia, ao escalar horizontalmente você adiciona **novas** moradias (**escalabilidade**), escalando verticalmente você adiciona novos andares para a mesma moradia (**elasticidade**)

### Escalabilidade

É sobre expandir horizontalmente (quantidade), para para ser **tolerante a falhas**

- Amazon EC2 Auto Scaling
  - O significado de Amazon EC2 é Amazon Elastic Compute Cloud
- É sobre o sistema ser capaz de escalar sob demanda (pico de uso) e ser tolerante a falhas, ter mais capacidade computacional.
- Você define um número **mínimo**, **desejado** e o **número máximo** de computadores EC2
- Com isso você: **melhora a disponibilidade** da aplicação; Obtêm um ambiente tolerante a falhas; Essa abordagem reflete nos custos operacionais, você só paga conforme o uso

### Elasticidade

- É sobre expandir verticalmente (capacidade) o recurso computacional, **distribuir carga de trabalho**
- Capacidade de expandir para se adaptar à outra forma

## Disponibilidade

### Região

- Uma **Região** é a disponibilização de uma coleção de recursos AWS em **localização geográfica**, sendo ele composto por um **conjunto de zonas de disponibilidade**.

### Zona de disponibilidade

- Uma **Zona de disponibilidade** é um ou mais datacenters que estão na mesma Região, porém separados por uma distância significativa, **atuando de forma independente** em caso de falha de uma zona
- São conectas com alta velocidade, com segurança local, refrigeração e rede
- São **redundantes** entre si via conectividade, rede e energia

### Ponto de Presença

- **Points of Presence** ou **Edge Locations** (locais de borda)
- É uma infraestrutura de servidores, localizado próximo de uma Zona de disponibilidade, que **armazena os dados** mais solicitados no **cache**, para entregar com **menor latência** uma requisição de consulta
- São utilizados como **cache de dados** para **distribuição de conteúdo**
