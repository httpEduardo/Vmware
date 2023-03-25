📖 Instruções

Este repositório ajuda a criar máquinas virtuais usando o Packer em hosts VMware ESXi.

[x] Construir VMs em uma rede simples com apenas DHCP e DNS
[x] Não usar servidor TFTP para inicialização pela rede
[x] Não usar um servidor HTTP separado
[x] Servidor de modelos HTTP integrado
[x] Manipular o CTRL+C adequadamente
[x] Construir VMs em paralelo, por exemplo xargs -P4 ...
Requisitos

Host ESXi vSphere 7.0U3 com acesso SSH habilitado.
Uma máquina de controle com binários go, ansible, hashicorp/packer e openssl.
Construções de VM suportadas

status	os	versão	especificações da máquina
👍	centos	8-stream	4 vCPU, 4 GiB vRAM, 100 GiB NVMe vDisk
👍	debian	bullseye	4 vCPU, 4 GiB vRAM, 100 GiB NVMe vDisk
👍	ubuntu	focal	4 vCPU, 6 GiB vRAM, 100 GiB NVMe vDisk
👍	ubuntu	jammy	4 vCPU, 6 GiB vRAM, 100 GiB NVMe vDisk
👍	photon	4	4 vCPU, 4 GiB vRAM, 100 GiB NVMe vDisk
👍	coreos	stable-stream	4 vCPU, 4 GiB vRAM, 100 GiB NVMe vDisk

🌱 Começando

Execute o playbook Ansible prepare_installers.yaml.
Crie um arquivo installers/overrides.pkrvars.hcl. Este arquivo contém variáveis ​​do Packer que substituem os valores padrão.
Execute o make, o binário builder será colocado na raiz da pasta do repositório.
Execute o binário builder. Use a flag -h para ver os argumentos necessários.
⚙️ overrides.pkrvars.hcl
O arquivo installers/overrides.pkrvars.hcl é usado pelo construtor para passar valores de variáveis ​​do Packer que substituem os valores padrão.

init

#
# Variáveis ESX
#
esx_server    = "" # host ESX
esx_username  = "" # usuário ESX com acesso admin e SSH
esx_password  = "" # senha do usuário ESX
esx_network   = "" # nome da rede virtual ESX para a VM
esx_datastore = "" # nome do datastore ESX para colocar os arquivos VMDK da VM

#
# Variáveis da VM
#
vm_username       = "" # usuário a ser criado na VM
vm_password       = "" # senha do usuário da VM
vm_ssh_public_key = "" # chave pública SSH para colocar no arquivo authorized_keys do usuário SSH da VM
⭐️ Uso
lua

Usage of ./builder:
  -c string
        O caminho para um arquivo de variáveis ​​do Packer que pode substituir os valores de variáveis ​​do Packer padrão. (padrão "/root/vmware-builder/installers/overrides.pkrvars.hcl")
  -e string
