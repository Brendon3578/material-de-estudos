# Identidade, Segurança & Computação

## User Groups & Roles

para se ter maior controle e gerenciamento sobre os grupos

## Autorizar

Políticas e Permissões
usa-se o Documento JSON que é utilizado para definir as permissões de acesso

Autenticação é você existir no IAM

Autorização é a permissão à acessar ou alterar um recurso atrelado à uma Autenticação

- **Usuários** possuem credenciais **permanentes**
- **Funções** possuem credenciais **temporárias**
- Usuários root **Não** devem ser compartilhados
- Use o `least privilege principle` nos usuários
- **Documentos JSON** definem as permissões dde acesso
- **Grupos** contém outros usuários, mas **Não** poem conter outros grupos

## EC2

Usa-se EC2 juntamente à EBS (opcional) para ter maior controle sobre o armazenamento, no qual se a instância EC2 for interrompida, o armazenamento não será perdido (bloco de volume `/root`), como se fosse um HD externo
