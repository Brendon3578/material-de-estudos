<h1> Descrever os benefícios do uso de serviços de nuvem  </h1>

Cada tipo de serviço determina a **flexibilidade** no gerenciamento e na configuração de recursos na nuvem. O modelo de responsabilidade compartilhada (provedor e consumidor) se aplica a todos os tipos de serviços de nuvem.

<img alt="Modelo de responsabilidade" src="../../assets/shared-responsibility.svg" width="525px">

# Infraestrutura como Serviço (IaaS)

O hardware é "alugado" em um datacenter da nuvem.

- Responsabilidades do provedor de nuvem
  - Manter o Hardware, conectividade de rede (com a Internet) e a segurança física
- Responsabilidades do Consumidor
  - Instalação, Atualização, Configuração e Manutenção do Sistema Operacional
  - Configuração de Rede
  - Configuração de Banco de Dados e Armazenamento

Cenários comuns:

- **Migração lift-and-shift:** Usando os recursos da nuvem semelhantes aos de um datacenter local, apenas migrando os recursos do datacenter local para o ambiente cloud de IaaS.
- **Teste de Desenvolvimento:** Estabelecendo configurações para ambientes de desenvolvimento e teste que precisa replicar rapidamente. Podendo ativar ou desativar os diferentes ambientes rapidamente, mantendo o controle completo com IaaS.

# Plataforma como Serviço (PaaS)

É o meio termo entre alugar espaço em um datacenter (IaaS) e pagar uma solução completa e implantada (PaaS), fornecendo um ambiente de desenvolvimento completo sem a preocupação de manter toda a infraestrutura de desenvolvimento

- Responsabilidades do provedor de nuvem
  - Infraestrutura física, segurança física, e conexão com a Internet
  - Sistemas Operacionais (licenças e aplicação de patch), Middleware, ferramentas de desenvolvimento
  - Serviços de BI e uso de Banco de Dados

Cenários comuns:

- **Estrutura de Desenvolvimento:** Fornecendo uma estrutura que os desenvolvedores podem usar como base para desenvolver ou personalizar aplicativos baseados em nuvem.
  - Permite aos desenvolvedores criar **aplciações** usando componentes de software interno (recursos de nuvem, escalabilidade, alta disponibilidade, funcionalidade de multi locatário, etc).
- **Análise ou Business Intelligence:** Permitindo que as organizações analisem e minerem dados, encontrando insights e padrões e prevendo resultados para aprimorar a previsão, as decisões de design de um produto, os retornos sobre investimentos e outras decisões de negócios

# Software como Serviço (SaaS)

É o mais completo, você aluga ou usa um aplicativo totalmente desenvolvido. Sendo o mais fácil de colocar em funcionamento.Sendo o que mais coloca a responsabilidade sobre o provedor e tem você sendo responsável apenas pelos dados que coloca no sistema e os usuários que têm acesso à esses dados.

- Responsabilidades do provedor de nuvem: segurança física dos datacenters, energia, conectividade de rede, e desenvolvimento e aplicação de patch dos aplicativos.

Cenários comuns:

- Email e aplicativos de mensagens, software financeiro e empresarial, e controle de finanças e despesas.
