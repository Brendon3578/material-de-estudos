# Papéis (roles) no IAM

Definem **quem** tem acesso a **o quê**. São uma coleção de **permissions** (permissões), pois é necessário mais de 1 permissão para se ter trabalho significativo.

Por exemplo se você for gerenciar uma VM, você deve ser capaz de Criar, Excluir, Deletar, Parar e Mudar VMs. Por isso as permissões são agrupadas em um **Role**, papel, para ser mais fácil de se gerenciar e ser entendido os acessos sobre os recursos.

Há 3 tipos de roles no Iam:

- **Basic roles:** **owner**, **editor** e **viewer**. Como boa prática, é usado **apenas** para testar recursos
- **Predefined roles:** um conjunto de roles do IAM que possuem manutenção constante do Google. Exemplo, no BigQuery: `admin, dataOwner, jobUser, dataEditor` que dentro há as permissões como: `bigquery.table.create` etc.
- **Custom roles:** são criados e gerenciados diretamente pelo usuário.

⚠ Os Basic Roles incluem milhares de permissões em todos os serviços do GCP. é recomendado usar **Predefined roles** ou **Custom Roles** no ambiente de produção.

## Limitações para custom roles

- Não pode ser criado no nível de **folder (pasta)**, Só consegue criar no nível de **organização ou projeto**
- Limite máximo de 300 por organização

## Casos de Usos

Em todos os cenários possíveis, deve-se avaliar primeiro quem tem acesso aos recursos certos. Por exemplo se você tem um usuário que queira apenas acessar as informações de uma VM, sem alterá-lo. Dentre as seguintes permissões: `compute.images.list`, `compute.images.get`, `compute.images.create`, `compute.images.setIAM` e `compute.images.update`, prefira atribuir APENAS as duas primeiras permissões citadas.

Em suma: se você é um **viewer** de um recurso, você deve ser capaz de visualizar um produto sem alterá-lo, se é um **editor**, você tem a função de um **viewer** e é capaz e poder alterar o recurso. Se você é um **owner** você é tem a função de um **editor** e gerencia os roles e permissões do recurso.
