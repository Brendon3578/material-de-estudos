<h1> Descrever a computação em nuvem </h1>

- [O que é computação em nuvem](#o-que-é-computação-em-nuvem)
- [Modelo de responsabilidade compartilhada](#modelo-de-responsabilidade-compartilhada)
  - [Tipos de Serviço de Nuvem](#tipos-de-serviço-de-nuvem)
- [Modelos da nuvem](#modelos-da-nuvem)
  - [Nuvem privada](#nuvem-privada)
  - [Nuvem pública](#nuvem-pública)
  - [Nuvem híbrida](#nuvem-híbrida)
  - [MultiCloud (Multi Nuvem)](#multicloud-multi-nuvem)
  - [Azure Arc](#azure-arc)
  - [Solução VMware No Azure](#solução-vmware-no-azure)
- [Modelo baseado em consumo](#modelo-baseado-em-consumo)
  - [Comparar os modelos de preços de nuvem](#comparar-os-modelos-de-preços-de-nuvem)
- [Recursos adicionais](#recursos-adicionais)

# O que é computação em nuvem

É a entrega em serviços de computação pela Internet (Infraestrutura de TI, máquinas virtuais, armazenamento, banco de dados, rede, etc). Como por exemplo: **Compute Power** (quantidade de processamento que o computador consegue executar) e **Storage** (volume de dados que podem ser armazenado no computador).

- Os serviços de nuvem expande para outras áreas como **Internet of Things** (IoT), **Machine Learning** (ML), e **Artificial Intelligence** (AI ou IA)
- Não fica restrita pela infraestrutura física (**On Premisses**), ou seja, há um escalonamento da infraestrutura de TI conforme o uso

# Modelo de responsabilidade compartilhada

No modelo tradicional o setor de TI de uma empresa é responsável por manter a infraestrutura e softwares de um datacenter em funcionamento através de: garantir a segurança e manter o espaço físico; substituir os servidores quando necessário

Com o Modelo de Responsabilidade Compartilhada , essas responsabilidades são compartilhadas entre o **Cloud Provider** (provedor de nuvem) e o **Consumidor** (aquele que consome os serviços da nuvem).

- Fatores como segurança, energia, resfriamento são responsabilidades do **provedor de nuvem**.
- A única responsabilidade do consumidor são os dados e informações que são armazenados na nuvem, e a segurança de acesso à elas.

Por exemplo em um banco de dados SQL, você é responsável pelos dados que são ingeridos no banco de dados. Enquanto o provedor da nuvem é responsável pela infraestrutura física do banco de dados.

## Tipos de Serviço de Nuvem

O modelo de responsabilidade compartilhada está fortemente vinculado aos tipos de serviço de nuvem prestados: **IaaS** (infrastructure as service), **PaaS** (platform as service) e **SaaS** (software as service).

- Em IaaS a maior responsabilidade é do consumidor, o provedor de nuvem é responsável pelas questões de infraestrutura básica (segurança física, energia e conectividade)
- A PaaS está entre IaaS e SaaS, distribuindo uniformemente a responsabilidade entre consumidor e provedor de nuvem.

<img alt="Modelo de responsabilidade" src="../../assets/shared-responsibility.svg" width="525px">

Sempre o consumidor sendo responsável por:

- Informações e dados armazenados na nuvem
- Dispositivos permitidos para se se conectarem à nuvem (celulares, computadores, etc)
- Contas e Identidades das pessoas, serviços e dispositivos da organização

Sendo o provedor da nuvem responsável por:

- Datacenter físico
- Rede física
- Hosts físicos

A escolha de serviço certa é fortemente importante, pois determina a responsabilidade e gastos de coisas como:

- Sistemas Operacionais
- Controles de Rede
- Aplicativos
- Identidade (controle de acesso) e Infraestrutura

# Modelos da nuvem

Define o tipo de implantação de recursos da nuvem em uma empresa

## Nuvem privada

**Evolução de um datacenter padrão**. É uma nuvem (que fornece serviços de TI pela Internet), usada por um único ponto (localizado dentro da infraestrutura - ou datacenter - local de uma empresa). Podendo ser hospedado também por datacenter de terceiros.

- Têm mais custos e menos benefícios em relação a nuvem pública
- Usado comumente em cenários no qual há regulamentos governamentais sobre onde os dados devem residir e onde a computação deve ocorrer

## Nuvem pública

A nuvem pública é um tipo de computação em que os recursos são oferecidos por um provedor terceirizado pela Internet e compartilhados por organizações e indivíduos que querem usá-los ou comprá-los.

As nuvens públicas contrastam com os modelos de nuvem privada, em que os recursos estão **disponíveis apenas para uma organização** e o data center é gerenciado no local ou fora do local por um fornecedor.

## Nuvem híbrida

É a combinação de ambos modelos de nuvem (pública e privada) em um ambiente interconectado. Permitindo que uma nuvem privada escale para atender a uma demanda maior temporária implantando recursos de nuvem pública.

## MultiCloud (Multi Nuvem)

É a utilização de serviços em nuvem de mais de um provedor/fornecedor cloud, como AWS, Azure, Google entre outros.

Há quando é utilizado os recursos de diferentes provedores, ou quando há a migração de um provedor de nuvem para o outro. Você gerencia recursos se segurança em ambos os ambientes cloud.

## Azure Arc

É um conjunto de tecnologias que ajuda no gerenciamento do ambiente da nuvem.

## Solução VMware No Azure

Usado quando o consumidor já está estabelecido com o VMware em um ambiente dde nuvem privada. Permitindo executar cargas de trabalho do VMware no Azure, com integração e escalabilidade total

# Modelo baseado em consumo

Ao comparar modelos de infraestrutura de TI, há dois tipos de despesas a serem consideradas. **CapEx** (despesas de capital) e **OpEx** (despesas operacionais).

- **CapEx**: despesa inicial única para comprar ou proteger recursos tangíveis. Por exemplo a construção de um datacenter
- **OpEx**: gasto de capital em serviços ou produtos ao longo do tempo. Por exemplo a assinatura de serviços de nuvem.

A computação em nuvem se enquadra na OpEx, pois opera em um modelo baseado em consumo. Você não paga pela infraestrutura física, mas pelos **recursos de TI que usa sob demanda**.

Você paga conforme consome (escalabilidade). Tendo vantagens como:

- Sem custos prévios
- Não há necessidade de comprar nem gerenciar uma infraestrutura que os usuários não usem sua capacidade máxima.
- Capacidade de pagar para obter mais recursos quando necessário.
- Capacidade de parar de pagar por recursos que não são mais necessários.

Com um datacenter tradicional, você tenta estimar as necessidades futuras de recursos:

- Se você superestimar, gastará mais do que o necessário no datacenter, podendo desperdiçar capital.
- Se você subestimar, o datacenter atingirá a capacidade rapidamente e os aplicativos e serviços poderão sofrer redução de desempenho.

## Comparar os modelos de preços de nuvem

Em um modelo baseado em nuvem, a infraestrutura de TI é **escalável** (paga conforme usa, sob demanda), se precisar de mais recursos, basta adicioná-las. Se a demanda cair, basta remover algumas, conforme a necessidade.

Computação em nuvem é a entrega de serviços de computação pela Internet, usando o **modelo de preço pago conforme o uso**. No que ajuda em:

- Planejar e gerenciar **custos operacionais**
- Executar a infraestrutura com mais **Eficiência**
- **Escalar** as operações de acordo com as necessidades de negócios

Em outras palavras, a computação em nuvem é uma forma de **alugar capacidade computacional e armazenamento do datacenter de terceiros**. Você trata os recursos de nuvem como faria com os recursos em seu próprio datacenter. Mas, ao contrário do seu próprio datacenter, ao terminar de usar os recursos de nuvem, basta devolvê-los. Você é cobrado apenas pelo que usa.

# Recursos adicionais

- [Modelo de responsabilidade compartilhada](https://learn.microsoft.com/pt-br/azure/security/fundamentals/shared-responsibility) – O modelo de responsabilidade compartilhada é o compartilhamento das responsabilidades de nuvem entre você e o provedor de nuvem.
- [Introdução à Solução VMware no Azure](https://learn.microsoft.com/pt-br/learn/modules/intro-azure-vmware-solution/) é um curso do Microsoft Learn que aprofunda o conhecimento sobre a Solução VMware no Azure.
- [Introdução aos serviços de nuvem híbrida do Azure](https://learn.microsoft.com/pt-br/learn/modules/intro-to-azure-hybrid-services/) é um curso do Microsoft Learn que explica a nuvem híbrida com mais detalhes.
