# Contas de Faturamento (Billing Account)

Uma Cloud Billing Account paga pelo uso dos projetos do GCP e do Google Maps Platform. Mas para contas do Google Workspace é necessário uma Billing Account separada.

Você só pode usar recursos do GCP se tiver uma Billing Account ativa ligada ao projeto.

- Uma conta de faturamento pode ser ligada à um ou mais projetos
- Um projeto e seus recursos só podem ser ligados à uma conta de faturamento apenas

As permissões de acesso a uma **conta do Cloud Billing** é gerenciado por **roles do IAM**. As permissões da billing account podem ser configuradas para que os usuários possam:

- Abrir, encerrar e modificar uma conta do Cloud Billing.
- Visualizar relatórios e dados de custo.
- Visualizar documentos, como faturas e extratos.
- Analisar descontos por compromisso de uso (CUD) e comprar CUDs.
- Ativar e gerenciar a exportação de dados de faturamento.
- Configurar orçamentos e alertas.
- Gerenciar o faturamento por projeto.
- Gerenciar as permissões de usuário para faturamento.
- Entrar em contato com o suporte do faturamento.

É possível definir uma política no nível da organização para aplicá-la a todas as contas e projetos do Cloud Billing e recursos na organização

Para um usuário poder ver os custos de **todos os projetos** em uma Billing Account do cloud, conceda a ele a permissão de visualizar os custos de uma conta (`billing.accounts.getSpendingInformation`). Já para visualizar os custos de um projeto específico, conceda a ele a permissão  de visualizar custos de projetos individuais (`billing.resourceCosts.get`)
