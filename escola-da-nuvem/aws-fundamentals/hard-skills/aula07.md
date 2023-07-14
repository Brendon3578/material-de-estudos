# CloudFront, Elastic Load Balancer, CloudWatch

## CloudFront

![CloudFront](images/svg/network_content-delivery/cloudfront.svg)

É um serviço de **entrega e conteúdo** (CDN) que entrega dos, vídeos, aplicativos e APIs a clientes e forma mundial, com **segurança, baixa latência** e alta velocidade.

Utiliza-se POPs que são pontos de presença (**Points of presence**) para acelerar a distribuição do conteúdo estático e dinâmico da web, como arquivos `.html`, `.css`, `jss` e arquivos de imagens através da rede global de datacenters. Operando do seguinte modo:

- O usuário pede a solicitação através de uma URL
- O DNS roteia a solicitação para o POP mais próximo do usuário
- O CloudFront retorna a requisição enviando para o ponto de presença solicitado (funcionando como uma memória cache)

### Segurança

Para ser utilizado com segurança, utiliza-se junto a outros recursos como o **AWS WAF Web Application Firewall**, **Amazon Route 53**, **AWS Shield (contra DDoS)** e **AWS Certificate Manager SSL/TSL e HTTPS** que cria um certificado SSL customizado para entregar o conteúdo com criptografia e https

## Elastic Load Balancer

![Elastic Load Balancer](images/svg/network_content-delivery/elb.svg)

É um serviço que distribui automaticamente o **tráfego de entrada** de aplicativos, como instâncias do 3C2, containers, IPs address e funções Lambda

Há 3 tipos de load balancer principais

- Application Load Balancer
- Network Load Balancer
- Gateway Loada Balancer
- (descontinuado) Classic Load Balancer

![Tipos de Load Balancers](./images/load-balancer.PNG)

## CloudWatch

![Cloud Watch](images/svg/management_governance/cloudwatch.svg)

É uma ferramenta de **monitoramento de desempenho dos recursos** e dos aplicativos que voce executa no seu ambiente

### Coletar

- É uma ferramenta que monitoria por meios de métricas e logs de recursos e serviços
- Recursos e serviços na Nuvem e on-premises
- Métrica padrão 5 minutos / detalhada ($$$) por minuto
- Exemplo de métricas
  - **EC2**: Utilização CPU, Status check, Rede
  - **EBS**: Leitura e Gravação do disco
  - **S3**: tamanho do bucket, número de objetos
  - **Lambda**: tempo de execução e duração

### Monitorar / Visualizar

- Visualizar as aplicações e sua infraestrutura em um único local
- Acessar um dashboard automático ou personalizado, com os serviços e métricas customizadas
- Configurar alarmes visuais do ambiente

### Atuar

- Criar alarmes para atuar como **gatilho**, baseado nas métricas de uso e desempenho
- Opções do gatilho: amostra, %, valor máximo, mínimo etc
- Alarm Action
  - **Auto Scaling Group**: Aumentar ou diminuir o número de instâncias no Amazon EC2
  - **EC2**: Parar, terminar, reiniciar ou recuperar uma instância
  - **SNS**: Enviar **notificações** para um **SNS Topic**, para que os assinantes recebam um e-mail

### Analisar

Analisar em tempo real o ambiente, em segundos ou posterior com até 15 meses de armazenamento dos logs

Análise de alarmes:

- `ok`: tudo está ocorrendo normalmente
- `insufficient_data`: ainda está coletando dados
- `alarm`: algo ruim aconteceu ou **indicar** que uma métrica foi atingida
