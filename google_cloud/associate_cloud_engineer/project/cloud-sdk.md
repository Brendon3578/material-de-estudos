# SDK do Cloud

- Há 4 **meios** principais de interagir com o GCP: o Google Cloud Console, Cloud SDK e o Cloud Shell, o Cloud Mobile App e as APIs.
- O **Console** é uma interface gráfica (graphical interface)
- **Command Line Interface** usando os comandos `gcloud`
  - **Cloud Shell** fornece um ambiente na nuvem (através do navegador/browser-based) CLI
  - O **Cloud SDK** fornece um ambiente local CLI para o Google Cloud, além de também oferecer bibliotecas (client libraries) para várias linguagens (Java, Go, Ruby, Node, PHP).
- **Cloud Mobile App** permite interagir com os recursos cloud em dispositivo mobile.
- **As APIs REST** permite o acesso baseado em CURL ou SDKs baseados nos clientes

Ele oferece ferramentas e bibliotecas pra interagir com o Google Cloud. Por exemplo os comandos: `gcloud` (comandos padrões do gcloud CLI), `gsutil` (interagir com o cloud storage) e `bq` (submit de queries do big query).

As bibliotecas fornecem APIs para acessar os serviços (application APIs e Admin API's) que permite automatizar a gerência de tarefa de recursos

- Usa-se o comando do cloud SDK `gsutil`, Para interagir com o **Cloud Storage**
- Há duas interfaces que provê um CLI para o Google Cloud: **Cloud Shell** e o **Cloud SDK**

## Cloud Shell

- Fornece um VM do Compute Engine temporário, rodando em um SO baseado em Debian (Linux)
- Você gerencia os recursos através de uma CLI pelo navegador
- 5 GB de memória persistente, montada no diretório `$HOME`
- Têm o Cloud SDK pré-instalado
- Suporte à linguagens, como SDKs, libs, runtime environments, e compiladores para Java, Python, Node, etc.
- Visualização web que permite visualizar aplicações web rodando no Cloud Shell

Com o **Cloudd Shell** você consegue:

- Criar e gerenciar instâncias do Compute Engine
- Criar e acessar banco de dados SQL do Cloud
- Gerenciar data do Cloud Storage
- Interagir com repositórios Git (como Cloud Source Repos)
- Build e deploy de aplicações do App Engine
