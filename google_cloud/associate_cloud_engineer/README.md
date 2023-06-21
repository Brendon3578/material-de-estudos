# Certificação Associate Cloud Engineer

Anotações sobre a certificação de Associate Cloud Engineer do Google Cloud. Cada seção abaixo foi extraído da página oficial da certificação do cloud. As anotações que estão nos links abaixo foram de autoria própria (baseado no conteúdo do Google Cloud Skill Boost)

## Seção 1: configurar um ambiente de solução de nuvem

1.1 Configurar [projetos de nuvem](./project/project.md) e contas. As atividades incluem:

- Criar uma [hierarquia de recursos](./project/resource_hierarchy.md)
- Aplicar [políticas organizacionais à hierarquia de recursos](./project/organization-policy.md)
- Conceder [papéis do IAM](./project/iam-roles.md) de membros em um projeto
- [Gerenciar usuários e grupos](./project/users-and-group.md) no Cloud Identity (manual e automaticamente)
- Ativar APIs nos projetos
- Provisionar e configurar produtos no pacote de operações do Google Cloud

1.2 Gerenciar as configurações de faturamento. As atividades incluem:

- Criar uma ou mais [contas de faturamento](./biling/billing-account.md);
- Vincular projetos a uma conta de faturamento;
- Estabelecer orçamentos e [alertas de faturamento](./biling/budget-alert.md)
- Configurar exportações de faturamento

1.3 Instalar e configurar a interface de linha de comando (CLI), especificamente o [SDK do Cloud](./project/cloud-sdk.md) (por exemplo, configurar o projeto padrão).

## Seção 2: planejar e configurar uma solução de nuvem

2.1 Planejar e estimar o uso dos produtos do Google Cloud usando a calculadora de preços.

2.2 Planejar e configurar recursos de computação. As considerações incluem:

- Selecionar as opções de computação apropriadas para uma determinada carga de trabalho (por exemplo, Compute Engine, Google Kubernetes Engine, Cloud Run, Cloud Functions)
- Usar VMs preemptivas e tipos de máquina personalizados, conforme apropriado.

2.3 Planejar e configurar as opções de armazenamento de dados. As considerações incluem:

- Escolher produtos (por exemplo, Cloud SQL, BigQuery, Firestore, Cloud Spanner e Cloud Bigtable)
- Como escolher as opções de armazenamento (por exemplo, Disco permanente por zona, Disco permanente equilibrado regional, Standard, Nearline, Coldline, Archive)

2.4 Planejar e configurar os recursos de rede. As tarefas desta seção incluem:

- Diferenciar as opções de balanceamento de carga;
- Identificar a localização de recursos em uma rede para disponibilidade;
- Configurar o Cloud DNS.

## Seção 3: implementar uma solução de nuvem

3.1 Implantar e implementar recursos do Compute Engine Inclui as seguintes tarefas:

- Inicializar uma instância de computação usando o Console do Cloud e o SDK do Cloud (gcloud) (por exemplo, atribuir discos, política de disponibilidade e chaves SSH)
- Criar um grupo de instâncias gerenciadas com escalonamento automático usando um modelo de instância;
- Gerar/fazer upload de uma chave SSH personalizada para as instâncias
- Como instalar e configurar o Cloud Monitoring e o Cloud Monitoring
- Avaliar as cotas de computação e solicitar aumentos

3.2 Implantar e implementar recursos do Google Kubernetes Engine Inclui as seguintes tarefas:

- Instalar e configurar a interface de linha de comando (CLI) para Kubernetes (kubectl)
- Implantar um cluster do Google Kubernetes Engine com diferentes configurações, incluindo Autopilot, clusters regionais, clusters particulares etc.
- Implantar um aplicativo em contêiner no Google Kubernetes Engine
- Como configurar o monitoramento e a geração de registros do Google Kubernetes Engine

3.3 Implantar e implementar recursos do Cloud Run e do Cloud Functions Quando aplicável, inclui as seguintes tarefas:

- Como implantar um aplicativo, atualizar configurações de escalonamento, versões e divisão de tráfego
- Implantar um aplicativo que recebe eventos do Google Cloud (por exemplo, eventos do Pub/Sub e de notificação de alteração nos objetos do Cloud Storage)

3.4 Implantar e implementar soluções de dados. As tarefas desta seção incluem:

- Inicializar sistemas de dados com produtos (por exemplo, Cloud SQL, Firestore, BigQuery, Cloud Spanner, Pub/Sub, Cloud Bigtable, Dataproc, Dataflow e Cloud Storage)
- Carregar dados (por exemplo, upload de linha de comando, transferência de API, importação/exportação, carregamento de dados do Cloud Storage, streaming de dados para o Pub/Sub)

3.5 Implantar e implementar recursos de rede. Inclui as seguintes tarefas:

- Criar uma VPC com sub-redes (por exemplo, VPC de modo personalizado, VPC compartilhada)
- Inicializar uma instância do Compute Engine com configuração de rede personalizada (por exemplo, endereço IP somente interno, acesso particular ao Google, endereço IP particular e externo estático, tags de rede)
- Criar regras de firewall de entrada e saída para uma VPC (por exemplo, sub-redes IP, tags de rede e contas de serviço)
- Criar uma VPN entre uma Google VPC e uma rede externa usando o Cloud VPN;
- Criar um balanceador de carga para distribuir o tráfego de rede para um aplicativo (por exemplo, balanceadores de carga HTTP(S) global, de proxy SSL global, de proxy TCP global, de rede regional e regional interno)

3.6 Implantar uma solução usando o Cloud Marketplace. As tarefas desta seção incluem:

- Navegar no catálogo do Cloud Marketplace e visualizar os detalhes da solução
- Implantar uma solução do Cloud Marketplace

3.7 Implementar recursos com a infraestrutura como código. Inclui as seguintes tarefas:

- Como criar infraestrutura usando modelos do Cloud Foundation Toolkit e implementar práticas recomendadas
- Instalar e configurar o Config Connector no Google Kubernetes Engine para criar, atualizar, excluir e proteger recursos

## Seção 4: garantir a operação de uma solução de nuvem

4.1 Gerenciar recursos do Compute Engine. Inclui as seguintes tarefas:

- Gerenciar uma única instância de VM (por exemplo, iniciar, parar, editar, configurar ou excluir uma instância)
- Conectar-se remotamente à instância
- Anexar uma GPU a uma nova instância e instalar as dependências necessárias
- Ver o inventário de VMs em execução (IDs de instância e detalhes)
- Trabalhar com snapshots (por exemplo, criar snapshots em uma VM, visualizá-los e excluí-los)
- Trabalhar com imagens (por exemplo, criar uma imagem em uma VM ou um snapshot, visualizá-la e excluí-la)
- Trabalhar com grupos de instâncias (por exemplo, definir parâmetros de escalonamento automático, criar e atribuir um modelo de instância e remover um grupo de instâncias)
- Trabalhar com interfaces de gerenciamento (por exemplo, Console do Cloud, Cloud Shell e SDK do Cloud)

4.2 Gerenciar recursos do Google Kubernetes Engine. As tarefas desta seção incluem:

- Visualizar o inventário de clusters em execução (nós, pods e serviços)
- Navegar pelas imagens do Docker e visualizar os detalhes no Artifact Registry
- Trabalhar com pools de nós (por exemplo, adicionar, editar ou remover um pool de nós)
- Trabalhar com pods (por exemplo, adicionar, editar ou remover pods)
- Trabalhar com serviços (por exemplo, adicionar, editar ou remover um serviço)
- Trabalhar com aplicativos com estado (por exemplo, volumes permanentes e conjuntos com estado)
- Gerenciar configurações de escalonamento automático horizontal e vertical
- Trabalhar com interfaces de gerenciamento (por exemplo, Console do Cloud, Cloud Shell, SDK Cloud e kubectl)

4.3 Gerenciar recursos do Cloud Run. Inclui as seguintes tarefas:

- Ajustar os parâmetros de divisão de tráfego do aplicativo
- Definir os parâmetros de escalonamento para instâncias de escalonamento automático
- Determinar se o Cloud Run (totalmente gerenciado) ou o Cloud Run for Anthos será executado

4.4 Gerenciar soluções de armazenamento e banco de dados. As tarefas desta seção incluem:

- Gerenciar e proteger objetos dentro e entre buckets do Cloud Storage
- Definir políticas de gerenciamento do ciclo de vida de objetos para buckets do Cloud Storage
- Executar consultas para recuperar dados de instâncias de dados (por exemplo, Cloud SQL, BigQuery, Cloud Spanner, Cloud Datastore e Cloud Bigtable)
- Estimar custos de recursos de armazenamento de dados
- Fazer backup e restaurar instâncias de dados (por exemplo, Cloud SQL e Datastore)
- Analisar o status do job no Dataproc, Dataflow ou BigQuery

4.5 Gerenciar recursos de rede. Inclui as seguintes tarefas:

- Adicionar uma sub-rede a uma VPC
- Expandir uma sub-rede para ter mais endereços IP
- Reservar endereços IP estáticos internos ou externos
- Trabalhar com CloudDNS, CloudNAT, balanceadores de carga e regras de firewall

4.6 Monitorar e registrar. Inclui as seguintes tarefas:

- Criar alertas do Cloud Monitoring com base em métricas de recursos
- Criar e ingerir métricas personalizadas do Cloud Monitoring (por exemplo, de aplicativos ou registros)
- Configurar coletores de registros com o objetivo de exportar registros para sistemas externos (por exemplo, infraestrutura no local ou no BigQuery)
- Configurar roteadores de registro
- Visualizar e filtrar registros no Cloud Logging
- Visualizar detalhes específicos da mensagem de registro no Cloud Logging
- Usar o diagnóstico de nuvem para pesquisar um problema do aplicativo (por exemplo, visualizar dados do Cloud Trace e usar o Cloud Debug para visualizar um ponto no tempo do aplicativo)
- Visualizar o status do Google Cloud

## Seção 5: configurar o acesso e a segurança

5.1 Gerenciar o Identity and Access Management (IAM). Inclui as seguintes tarefas:

- Visualizar as políticas do IAM
- Criar políticas do IAM
- Gerenciar os vários tipos de papel e definir papéis personalizados do IAM (por exemplo, primitivos, predefinidos e personalizados)

5.2 Gerenciar contas de serviço. Inclui as seguintes tarefas:

- Como criar contas de serviço
- Usar contas de serviço em políticas do IAM com permissões mínimas
- Atribuir contas de serviço a recursos
- Gerenciar o IAM de uma conta de serviço
- Gerenciar a representação de uma conta de serviço
- Criar e gerenciar credenciais de conta de serviço de curta duração

5.3 Ver registros de auditoria.
