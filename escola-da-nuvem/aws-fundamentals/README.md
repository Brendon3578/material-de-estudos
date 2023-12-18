# Fundamentos de AWS - Escola da Nuvem - AWS Cloud Practitioner

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)

Essas anotações me ajudaram muito a conseguir a certificação de 🏆 **AWS Cloud Practitioner** 🏆

Veja minha certificação [clicando aqui](https://www.credly.com/badges/19a56a8a-e2df-4a43-badf-2c439b1719e1)

Anotações sobre o curso de Fundamentos de AWS da Escola da Nuvem ☁ para a certificação de AWS Cloud Practitioner (CLF-C01) e para a versão atual do exame (CLF-C02). Essas anotações é uma união do conteúdo lecionado pela Escola da Nuvem com a documentação oficial de serviços da própria AWS com algumas anotações que eu achei importante anotar que pode ajudar aquele que estudar para a certificação de Cloud Practitioner

## 🔮 Aulas sobre a AWS - Hard skills

- [Introdução de Fundamentos de AWS](./hard-skills/aula01.md)
- [💰 Console Gerenciamento & Gerenciamento Custos](./hard-skills/aula02.md)
- [🔐 Identidade, Segurança & Computação](./hard-skills/aula03.md)
- [💻 EC2, AutoScaling, Lambda e Elastic Beanstalk](./hard-skills/aula04.md)
  - [💡 Containers na AWS e Serverless](./hard-skills/extra/containers.md)
- [💿 Armazenamento (S3) e website estático](./hard-skills/aula05.md)
  - [💡 Tipos de armazenamento na AWS](./hard-skills/extra/storage.md)
- [🚚 EBS, Snow Family, Glacier, VPC, DNS e Route 53](./hard-skills/aula06.md)
  -+ [💡 Armazenamento de arquivos com Amazon EFS](./hard-skills/extra/amazon-efs.md)
- [🌐 CloudFront, Elastic Load Balancer, CloudWatch](./hard-skills/aula07.md)
- [📝 Monitoria, Governança e Melhores Práticas AWS](./hard-skills/aula08.md)
  - [💡 Monitoramento de recursos na AWS](./hard-skills/extra/monitoring.md)
  - [💡 Faturamento consolidado](./hard-skills/extra/consolidated-billing.md)
- [📼 Banco de Dados SQL, NoSQL e nuvem como código](./hard-skills/aula09.md)
  - [💡 Boas práticas do Amazon RDS](./hard-skills/extra/rds.md)

## 💡 Aulas de preparo comportamental - Soft skills

- [O que são Softskills](./soft-skills/aula00.md)
- [Mercado de trabalho e Carreira na nuvem](./soft-skills/aula01.md)
- [Ser Protagonista da própria carreira](./soft-skills/aula02.md)
- [Síndrome do Impostor e Inteligência Emocional](./soft-skills/aula03.md)
- [Lifelong Learning e o Papel da Mentoria](./soft-skills/aula04.md)

### 💡 Aulas de preparo de carreira

- [Aulas - Como alavancar a sua carreira](./hard-skills/career/aula.md)

---

## 🎈 Anotações para o novo modelo de exame CLF-C02

- [🧠 AWS para Machine Learning de tradução](./others/language-ml.md)
- [🌱 Migrando para a a AWS](./others/lift-and-shift.md)

## ❔ O que é a AWS

> A Amazon Web Services fornece **serviços e computação em nuvem**. Recursos de TI que antes sua provisão era demorada e custosa, pode ser provisionada em segundos com a computação em nuvem moderna.

### Vantagens dos serviços de Cloud da AWS

- Provisionar uma infraestrutura **escalável** e **elástica**
- Criar aplicações altamente disponíveis utilizando de recursos como: **Load balancers** e **zonas de disponibilidade** (que estão em regiões), possibilitando a **redundância de dados** (replicação dos recursos em várias zonas distintas da mesma região), permitindo ser **tolerante a falhas**
- **Pay as-you-go:** Pagar apenas pela infraestrutura que utiliza, facilitando a implantação de novos recursos ou o desligamento de recursos que não estão sendo utilizados
- Gerenciar o controle do acesso aos recursos e administrar **quem** tem acesso a **quais** recursos através de políticas e permissões
- Monitorar o **desempenho de recursos** podendo criar alertas para quando haver aumento no acesso aos recursos ou quanto atingir métricas pré determinadas

<!-- Todas as imagens do serviços do AWS Foram tiradas desse site: https://awsicons.dev/ -->