# Application Load Balancer

Os recursos principais do ALB são:

- **Rotear tráfego com base nos dados da solicitação**: ele toma decisões com base no protocolo HTTP, como o caminho URL e host, cabeçalhos e métodos HTTP. Permitindo o roteamento granular para *target groups*
- **Enviar respostas diretamente ao usuário**
- **Usar o descarregamento TLS**: Garantindo o tráfego criptografado, passando o tráfego HTTPS por meio de um certificado SSL provido por serviços IAM ou do AWS Certificate Manager (ACM)
- **Autenticação do usuário**: através do protocolo OpenID oferecendo suporte a protocolosConnect, SAML, LDAP, Microsoft Active Directory, etc
- **Proteção do tráfego**: através de security groups e intervalos de IPs especificados
- **Algoritmo de roteamento round-robin**: cada servidor receba o mesmo número de solicitações em geral.
- **Usa do algoritmo de roteamento de solicitações menos pendente**: Pode ser utilizado o **algoritmo de solicitação menos pendente** e **solicitação de roteamento certo** dependendo do tipo de solicitação recebida pelo back-end, para garantir um uso igual entre os destinos
- **Sticky sessions**: para aplicações com estado, que é utilizado um cookie HTTP para lembrar entre conexões, para qual servidor enviar o tráfego.

## Guias úteis

[Autenticar usuários usando um Application Load Balancer](https://docs.aws.amazon.com/pt_br/elasticloadbalancing/latest/application/listener-authenticate-users.html)
[AWS WAF para proteção de solicitações HTTP(S) sobre o ALB](https://docs.aws.amazon.com/pt_br/waf/latest/developerguide/how-aws-waf-works.html)
