# oracledb Ambiente para teste de deploy de oracle database


Comandos Vagrant

- vagrant init
- vagrant up
- vagrant reload
- vagrant halt
- vagrant ssh
- vagrant suspend
- vagrant destroy


Para o caso do lab de oracle, o comando abaixo foi digitado para subir uma VM com base no oracle linux 7.9

vagrant init oraclelinux/7 https://oracle.github.io/vagrant-projects/boxes/oraclelinux/7.json


OBS: 
# 1- Rede
para evitar que o ip mude toda hora por usar a placa em modo bridge, use a placa de rede em modo host-only

Na linha 34 do arquivo foi adicionado uma rede: 

config.vm.network "private_network", ip: "192.168.56.190"

# 2- o local do arquivo

O arquivo Vagrantfile não deve ser movido e todos os comandos vagrant devem ser executados dentro do local do mesmo. Modificar o lugar do arquivo exige que você desligue e suba a máquina novamente

# Adicionar 2 discos de tamanho fixo na VM após ela ser criada e desligada

Entrar no OS utilizando o comando
- vagrant ssh

# Configurar o servidor de ssh para permitir conexões

cd /etc/ssh/
vi sshd_config

Tirar os comentários de: 
PermitRootLogin yes
PasswordAuthentication yes
PubkeyAuthentication yes

systemctl restart sshd
ip a  - conferir se pegou o IP 


# Configurações no Linux


yum upgrade

df -H

fdiks -l

 fdisk /dev/sdb   (- n, p enter 2x w)

 fdisk /dev/sdc

mkfs.ext4 /dev/sdb1

mkfs.ext4 /dev/sdc1

vi /etc/fstab

e2label /dev/sdb1 /u01

e2label /dev/sdc1 /u02

mkdir /u01 /u02

mount -a

df -H

yum install -y oracle-database-preinstall-19c

passwd oracle

chown -R oracle:oinstall /u01 /u02

su - oracle










Fontes: 

https://blogs.oracle.com/linux/post/oracle-linux-vagrant-boxes-now-include-catalog-data-and-add-support-for-libvirt-provider
https://yum.oracle.com/boxes/
