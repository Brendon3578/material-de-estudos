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

É a entrega em serviços de computação pela Internet (Infraestrutura de TI, máquinas virtuais, armazenamento, banco de dados, rede, etc).

- Os serviços de nuvem expande para outras áreas como **Internet of Things** (IoT), **Machine Learning** (ML), e **Artificial Intelligence** (AI ou IA)
- Não fica restrita pela infraestrutura física (**On Premisses**), ou seja, há um escalonamento da infraestrutura de TI conforme o uso

# Modelo de responsabilidade compartilhada

No modelo tradicional o setor de TI de uma empresa é responsável por gerenciar toda a segurança, gerência e manutenção da infraestrutura de um datacenter.

Com o **Modelo de Responsabilidade Compartilhada**, essas responsabilidades são compartilhadas entre o **Cloud Provider** (fornecedor da nuvem) e o **Consumidor**.

- Fatores como segurança, energia, resfriamento são responsabilidades do **provedor de nuvem**.
- A única responsabilidade do consumidor são os **dados** que são armazenados na nuvem, e a **segurança** de acesso à elas.

Por exemplo em um database SQL, você é responsável pelos dados que são ingeridos no banco de dados. Enquanto o provedor da nuvem é responsável pela infraestrutura física do DB.

## Tipos de Serviço de Nuvem

O modelo de responsabilidade compartilhada está fortemente vinculado aos tipos de serviço de nuvem prestados: **IaaS** (infrastructure as service), **PaaS** (platform as service) e **SaaS** (software as service).

- Em IaaS a maior responsabilidade é do consumidor, como provedor o responsável pelas questões de infraestrutura básica.
- A PaaS está entre IaaS e SaaS

<img alt="Modelo de responsabilidade" src="../../assets/shared-responsibility.svg" width="525px">

Sempre o consumidor sendo responsável por:

- Informações e dados armazenados na nuvem
- Dispositivos permitidos para se se conectarem à nuvem
- **Contas e Identidades** das pessoas, serviços e dispositivos da organização (No Azure: **Azure Active Directory** ou Azure AD)

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

**Evolução de um datacenter padrão**. Refer-se aos serviços de computação em nuvem oferecidos pela Internet ou por uma rede interna privada somente a usuários selecionados e não ao público geral (dentro de uma corporação ou empresa). Também podendo ser hospedado por datacenter de terceiros.

- Têm mais custos e menos benefícios em rel
- ação a nuvem pública
- Usado comumente em cenários no qual há regulamentos governamentais sobre **onde** os dados devem residir e **onde** a computação deve ocorrer

## Nuvem pública

Uma **nuvem privada** fica dentro da infraestrutura de uma empresa, como a intranet ou um data center. Já a **nuvem pública** vai além das paredes de uma empresa. Ela pertence e é operada por um terceiro que a fornece pela internet. Com a nuvem pública, as empresas compartilham hardware, armazenamento e dispositivos de rede.

## Nuvem híbrida

É a combinação de ambos modelos de nuvem (pública e privada) em um ambiente interconectado. Permitindo que uma nuvem privada escale para atender a uma demanda maior temporária implantando recursos de nuvem pública.

## MultiCloud (Multi Nuvem)

É a utilização de serviços cloud por mais de um provedor cloud.

Há quando é utilizado os recursos de diferentes provedores, ou quando há a migração de um provedor de nuvem para o outro. Com você gerenciando recursos se segurança em ambos os ambientes cloud.

## Azure Arc

É um conjunto de tecnologias que ajuda no gerenciamento do ambiente da nuvem.

## Solução VMware No Azure

Usado quando o consumidor já está estabelecido com o VMware em um ambiente de nuvem privada. Permitindo executar cargas de trabalho do VMware no Azure, com integração e escalabilidade total

# Modelo baseado em consumo

Ao comparar modelos de infraestrutura de TI, há dois tipos de despesas a serem consideradas. **CapEx** (despesas de capital) e **OpEx** (despesas operacionais).

- **CapEx:** despesa inicial única para comprar ou proteger recursos tangíveis. Por exemplo a construção de um datacenter
- **OpEx:** gasto de capital em serviços ou produtos ao longo do tempo. Por exemplo a assinatura de serviços de nuvem.

A computação em nuvem se enquadra na **OpEx**, pois opera em um modelo baseado em consumo. Você não paga pela infraestrutura física, mas pelos **recursos de TI que usa sob demanda**.

Você paga conforme consome (escalabilidade). Tendo vantagens como:

- Sem custos prévios
- Não há necessidade de comprar nem gerenciar uma infraestrutura no qual os usuários não usem sua capacidade máxima.
  - Capacidade de pagar ou parar de pagar pelos recursos cloud, dependendo da necessidade atual.
- Já no modelo de datacenter tradicional, você estima as necessidades futuras de recursos:
  - Se você **superestimar**, gastará mais do que o necessário no datacenter, podendo desperdiçar capital.
  - Se você **subestimar**, o datacenter atingirá a capacidade rapidamente e os aplicativos e serviços poderão sofrer redução de desempenho.

## Comparar os modelos de preços de nuvem

Em um modelo baseado em nuvem, a infraestrutura de TI é **escalonável** (paga conforme usa, sob demanda), se precisar de mais recursos, basta adicioná-las. Se a demanda cair, basta remover algumas, conforme a necessidade.

**Computação em nuvem** é a entrega de serviços de computação pela Internet, usando o **modelo de preço pago conforme o uso**. No que ajuda em:

- Planejar e gerenciar **custos operacionais**
- Executar a infraestrutura com mais **Eficiência**
- **Escalar** as operações de acordo com as necessidades de negócios

Você **aluga** capacidade computacional e armazenamento do datacenter de terceiros

Você trata os recursos de nuvem como faria com os recursos em seu próprio datacenter. Mas, ao contrário do seu próprio datacenter, ao terminar de usar os recursos de nuvem, basta devolvê-los. Você é cobrado apenas pelo que usa.

# Recursos adicionais

- [Modelo de responsabilidade compartilhada](https://learn.microsoft.com/pt-br/azure/security/fundamentals/shared-responsibility) – O modelo de responsabilidade compartilhada é o compartilhamento das responsabilidades de nuvem entre você e o provedor de nuvem.
- [Introdução à Solução VMware no Azure](https://learn.microsoft.com/pt-br/learn/modules/intro-azure-vmware-solution/) é um curso do Microsoft Learn que aprofunda o conhecimento sobre a Solução VMware no Azure.
- [Introdução aos serviços de nuvem híbrida do Azure](https://learn.microsoft.com/pt-br/learn/modules/intro-to-azure-hybrid-services/) é um curso do Microsoft Learn que explica a nuvem híbrida com mais detalhes.
