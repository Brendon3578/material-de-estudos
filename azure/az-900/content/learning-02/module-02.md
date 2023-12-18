<h1> Descrever os serviços de computação e rede do Azure </h1>

# Máquinas Virtuais do Azure

As VMs fornecem IaaS na forma de um servidor virtualizado.

- Você pode personalizar todos os programas de software em execução na VM. As VMs são úteis quando você precisa:
  - Controle Total sobre o SO
  - Capacidade para executar um software personalizado.
  - Usar configurações personalizadas de hospedagem
- Com uma VM você precisa configurar, atualizar e manter o software executado na VM
- Você pode criar ou usar uma imagem já criada para provisionar VMs, podendo provisionar uma VM em minutos quando seleciona uma imagem VM pré-configurada (modelo usado para criar VMs que já incluem um SO e outros softwares, como ferramentas de desenvolvimentos ou ambientes de hospedagem na Web)

## Dimensionar VMs

Você usar VMs individualmente ou agrupar VMs para fornecer alta disponibilidade, escalabilidade e redundância, para a segunda opção pode se usar recursos como **conjuntos de dimensionamentos** (scale sets) e **conjuntos de disponibilidade** (availability sets).

## Conjuntos de Dimensionamento (Scale Sets) de VMs

Permite criar e gerenciar um grupo de VMs **idênticas** com um **balanceamento de carga** em vez de fazer todo processo manual de criação e monitoramento de VMs idênticas e a configuração de roteamento de rede.

- Com os VMs scale sets, o Azure automatiza esse trabalho centralizando o processo de gerência e configuração de um grande número de VMs.
- A quantidade de VMs aumenta ou diminuir conforme à demanda, ou você pode definir uma escala bom base em uma agenda definida
- Os scale sets implantam um balanceador de carga, para permitir que os recursos sejam usados com eficiência
- Usado para criar serviços em grande escala, como computação, big data e caragas de trabalho em contêiner.

## Conjunto de Disponibilidade (availability sets) de VMs

Projetado para garantir que as VMs escalonem atualizações e tenham conectividade de rede e energia variadas, impedindo a perca de todas as VMs com uma só falha de rede ou energia.

- Os conjuntos de disponibilidade agrupam as VMs de duas maneiras:
  - **Domínio de atualização (update domain):** essas VMs podem ser reinicializadas ao mesmo tempo. Permitindo que você aplique atualizações sabendo que apenas um grupo de domínio de atualização estará offline por vez.
    - Um grupo de atualizações que passa pelo processo de atualização recebe um tempo de 30 minutos para se recuperar antes que a manutenção no próximo domínio de atualização seja iniciada.
  - **Domínio de falha (fault domain):** agrupa as VMs por origem de energia comum e computador de rede. Por padrão, um conjunto de disponibilidade divide as VMs em até 3 domínios de falha, ajudando a proteger contra uma falha de energia física ou de rede, tendo VMs em diferentes domínios de falha.

## Casos comuns de se usar usar VMs

- **Durante o teste e o desenvolvimento:** fornecendo um meio rápido de criar diferentes configurações de SOs e aplicativos
- **Executando aplicativos na nuvem:** a capacidade de usar capacidade computacional de VMs apenas conforme o uso, e não em uma infraestrutura on premisse.
- **Estender o datacenter para a nuvem:** uma organização pode estender os recursos de sua própria rede local criando uma rede virtual no Azure e adicionando VMs a ela.
- **Durante a recuperação de desastre:** Se um datacenter primário (local) falhar, você poderá criar VMs em execução no Azure para executar seus aplicativos críticos e desligá-los quando o datacenter primário ficar operacional novamente.

## Migrar para nuvem com Vms

As VMs são excelentes opções em uma migração **lift-and-shift** (físico para a nuvem). Assim como um servidor local físico, você deve manter a VM: você é responsável por manter o SO e o software instalado.

## Recursos da VMs

Ao provisionar uma VM, você escolhe os recursos associados a ela, como:

- **Tamanho** (finalidade, número de núcleos de processador e quantidade de RAM)
- **Discos de armazenamento** (unidades de disco rígido, unidades de estado sólido etc.)
- **Rede** (rede virtual, endereço IP público e configuração de porta)

# Exercício - Criando uma VM dod Azure

Criar uma VM do Azure e instalar o Nginx (servidor web popular)

```bash
# criar uma VM do Linux
az vm create \
  --resource-group learn-d6e8e744-6d9d-45ca-b78d-d1d462dc510d \
  --name my-vm \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

```bash
# configurar o Nginx na VM
az vm extension set \
  --resource-group learn-d6e8e744-6d9d-45ca-b78d-d1d462dc510d \
  --vm-name my-vm \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --version 2.1 \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```
