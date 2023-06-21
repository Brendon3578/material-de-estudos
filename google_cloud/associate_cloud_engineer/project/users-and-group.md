# Gerenciar Usuários e grupos

Como boa prática, os usuários (contas) devem ser adicionadas à **grupos**. Pois permitem gerenciar usuários em escala. Todo membro do **Grupo** herda os papéis (roles) do IAM concedido a esse grupo.

Essa **herança** permite você usar uma associação de um grupo para gerenciar as **funções** dos usuários em vez de conceder **papéis** a usuários individuais.

Nota: **Roles/papéis** são combinações de **Permissões** **individuais**. Deve-se atribuir a um usuário um **role** em vez de uma **permission** separada.
