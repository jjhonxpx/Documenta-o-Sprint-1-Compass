
# Descrição das atividades solicitadas.

Uma breve descrição sobre o projeto.


## Instalação do Oracle Linux 8 no VirtualBox.

1. Download da ISO do Oracle Linux 8
1. Vá para o site oficial da Oracle para baixar a ISO: [https://www.oracle.com/linux/downloads.html](https://www.oracle.com/linux/downloads.html).
2. Escolhi a versão "Oracle Linux 8" e baixe a ISO correspondente
2. Instalação e Configuração do VirtualBox
1. Se você ainda não tem o VirtualBox instalado, vá para [https://www.virtualbox.org/](https://www.virtualbox.org/) e baixei a última versão disponível para o meu sistema operacional, no caso o Windows.
2. Instalei o VirtualBox seguindo as instruções na tela.
3. Após a instalação, abra o VirtualBox e cliquei em "Nova" para criar uma máquina virtual.
4. Nomeei minha máquina virtual, escolhi "Linux" como tipo e "Oracle (64-bit)" como versão.
5. Configurei a memória e o espaço em disco de acordo com o qual achei necessário com as necessidades e recursos disponíveis.

3. Instalação do Oracle Linux 8
1. Selecionei a VM e clique em "Iniciar".
2. O Oracle Linux iniciou a partir da ISO. Selecione "Install Oracle Linux 8.x" e pressionei Enter.
3. Escolhi o “idioma e o layout do teclado”, a “hora e data”.
4. Na tela de instalação, na aba “PROGRAMAS” fui em “Seleção de programas” e escolhi a opção “Servidores com GUI”.
5. Em "Destino da instalação”, selecionei o disco onde queria fazer a instalação.
6. Nas “CONFIGURAÇÕES DE USUÁRIOS” selecionei a “Senha do root”, logo em seguida criei a minha senha, repetindo a mesma no campo abaixo solicitado e cliquei em pronto. Na “Criação de usuário” Preenchi os dados solicitados nos campos correspondentes, como nome, nome de usuário, senha e finalizei.
6. Revisei as outras opções conforme necessárias e clique em "Iniciar a instalação".
8. Quando a instalação esteve completa, cliquei em "Reiniciar".
4. Pós-instalação

1. Após a reinicialização, siga as etapas pós-instalação na tela para configurar meu SO.
2. Instalei as "Guest Additions" do VirtualBox para melhorar a integração entre o host e a máquina virtual. Para isso, no menu da VM no VirtualBox, vá para "Dispositivos" > "Inserir imagem de CD das Adições de Convidado" e segui as instruções.

Pronto! Agora você tem uma instalação funcional do Oracle Linux 8 em sua máquina virtual no VirtualBox.

2. Instalação e Configuração do VirtualBox
1. Se você ainda não tem o VirtualBox instalado, vá para [https://www.virtualbox.org/](https://www.virtualbox.org/) e baixei a última versão disponível para o meu sistema operacional, no caso o Windows.
2. Instalei o VirtualBox seguindo as instruções na tela.
3. Após a instalação, abra o VirtualBox e cliquei em "Nova" para criar uma máquina virtual.
4. Nomeei minha máquina virtual, escolhi "Linux" como tipo e "Oracle (64-bit)" como versão.
5. Configurei a memória e o espaço em disco de acordo com o qual achei necessário com as necessidades e recursos disponíveis.

3. Instalação do Oracle Linux 8
1. Selecionei a VM e clique em "Iniciar".
2. O Oracle Linux iniciou a partir da ISO. Selecione "Install Oracle Linux 8.x" e pressionei Enter.
3. Escolhi o “idioma e o layout do teclado”, a “hora e data”.
4. Na tela de instalação, na aba “PROGRAMAS” fui em “Seleção de programas” e escolhi a opção “Servidores com GUI”.
5. Em "Destino da instalação”, selecionei o disco onde queria fazer a instalação.
6. Nas “CONFIGURAÇÕES DE USUÁRIOS” selecionei a “Senha do root”, logo em seguida criei a minha senha, repetindo a mesma no campo abaixo solicitado e cliquei em pronto. Na “Criação de usuário” Preenchi os dados solicitados nos campos correspondentes, como nome, nome de usuário, senha e finalizei.
6. Revisei as outras opções conforme necessárias e clique em "Iniciar a instalação".
8. Quando a instalação esteve completa, cliquei em "Reiniciar".
4. Pós-instalação

1. Após a reinicialização, siga as etapas pós-instalação na tela para configurar meu SO.
2. Instalei as "Guest Additions" do VirtualBox para melhorar a integração entre o host e a máquina virtual. Para isso, no menu da VM no VirtualBox, vá para "Dispositivos" > "Inserir imagem de CD das Adições de Convidado" e segui as instruções.

Pronto! Agora você tem uma instalação funcional do Oracle Linux 8 em sua máquina virtual no VirtualBox.



## Configuração dos IP fixo nos dois servidores
1.	Primeiro identifiquei o nome da minha interface de rede com o seguinte comando: nmcli device status, ao qual é enp0s3.
2.	Para localizar meu IP, digitei o seguinte comando: ifconfig, procurei por inet e localizei o meu IP.
3.	Entrei como usuário root digitando su, inseri minha senha e pronto.
4.	Nessa etapa, utilizei o seguinte comando para alterar meu IP
```bash
  nmcli con mod enp0s3 ipv4.addresses 192.168.1.100/24
```
o IP presente no comando é apenas um exemplo, tem que substituir pelo ip pesquisado no seu server, o “enp0s3” é o nome da minha interface, caso o seu seja outro nome, substitua pelo nome correspondente.
5.	Para alterar o gateway executei o comando
```bash
  nmcli con mod enp0s3 ipv4.gateway 192.168.1.1.
```
6.	Para alterar o meu DNS, executei o seguinte comando:
```bash
  nmcli con mod enp0s3 ipv4.dns "8.8.8.8 8.8.4.4"
```
7.	Para deixar o método do meu ipv4 como manual executei o comando
```bash
  nmcli con mod enp0s3 ipv4.method manual.
```
8.	Por fim para concluir as configurações, reiniciei minha rede com o comando
```bash
  nmcli con up enp0s3
```
9.	Executei o comando 
```bash
  nmcli con show enp0s3
```
busquei por “ipv4.method: ” e conferir se o método estava “manual”, além de verificar se o IP estava correto, conforme tinha configurado anteriormente.
10.	 Na segunda VM, refiz todos os comandos citados acima, alterando somente informações, como IP.

## Instalação do NFS no servidor.

1.	Instalei o NFS com o comando
```bash
  sudo dnf install -y nfs-utils
```
2.	Entrei no modo root e ativei o serviço com os comandos a seguir, nessa ordem:
```bash
  systemctl enable nfs-server.service
    systemctl start nfs-server.service
		systemctl status nfs-server.service

```
3.	Criei um diretório para conter meus arquivos compartilhados com o comando 
```bash
  mkdir /nfs-share
```
4.	Criei uma série de arquivos de teste, com os comandos
```bash
fallocate -l 10MB /nfs-share/file1
fallocate -l 10MB /nfs-share/file2
echo "This is a shared text file." | sudo tee /nfs-share/shared-text.txt > /dev/null
```
5.	Alterei as permissões nos arquivos com o comando
```bash
  chmod -R 777 /nfs-share
```
6.	Defini o compartilhamento em /etc/exports, com o comando 
```bash
  echo "/nfs-share  <CLIENT_IP_ADDRESS>(rw)" | sudo tee -a /etc/exports > /dev/null
```
(O <CLIENT_IP_ADDRESS> é o endereço IP da instância do cliente e (rw) indica que o compartilhamento é leitura-gravação para o endereço IP definido.)
7.	Defini o firewall para permitir tráfego NFS
```bash
firewall-cmd --permanent --zone=public --add-service=nfs
firewall-cmd --reload
firewall-cmd --list-all
```
## Configuração dos IP fixo nos dois servidores
1.	Primeiro identifiquei o nome da minha interface de rede com o seguinte comando: nmcli device status, ao qual é enp0s3.
2.	Para localizar meu IP, digitei o seguinte comando: ifconfig, procurei por inet e localizei o meu IP.
3.	Entrei como usuário root digitando su, inseri minha senha e pronto.
4.	Nessa etapa, utilizei o seguinte comando para alterar meu IP
```bash
  nmcli con mod enp0s3 ipv4.addresses 192.168.1.100/24
```
o IP presente no comando é apenas um exemplo, tem que substituir pelo ip pesquisado no seu server, o “enp0s3” é o nome da minha interface, caso o seu seja outro nome, substitua pelo nome correspondente.
5.	Para alterar o gateway executei o comando
```bash
  nmcli con mod enp0s3 ipv4.gateway 192.168.1.1.
```
6.	Para alterar o meu DNS, executei o seguinte comando:
```bash
  nmcli con mod enp0s3 ipv4.dns "8.8.8.8 8.8.4.4"
```
7.	Para deixar o método do meu ipv4 como manual executei o comando
```bash
  nmcli con mod enp0s3 ipv4.method manual.
```
8.	Por fim para concluir as configurações, reiniciei minha rede com o comando
```bash
  nmcli con up enp0s3
```
9.	Executei o comando 
```bash
  nmcli con show enp0s3
```
busquei por “ipv4.method: ” e conferir se o método estava “manual”, além de verificar se o IP estava correto, conforme tinha configurado anteriormente.
10.	 Na segunda VM, refiz todos os comandos citados acima, alterando somente informações, como IP.

## Instalação do NFS no segundo servidor.

1.	Instalei o NSF no segundo servidor, usando os mesmos comando da instalação anterior, até a etapa 2.
2.	Criei um diretório para o ponto de montagem 

```bash
  mkdir /nfs-mount 
```
3.	Montei o compartilhamento e obtive uma listagem de diretórios. 
```bash
mount <SERVER_IP_ADDRESS>:/nfs-share /nfs-mount
ls -lh /nfs-mount
```
4.	Testei o acesso ao compartilhamento NFS 
```bash
echo "Hello World!" >> /nfs-mount/shared-text.txt cat /nfs-share/shared-text.txt.
```
## Instalação do MariaDB

1.	Atualize o sistema
```bash
  sudo dnf update
```
2.	Adicione o repositório MariaDB ao meu Linux 
```bash
curl -LsS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version="mariadb-10.6".
```
3.	Instalei os pacotes do MariaDB 10.6 com os seguintes comandos 
```bash
sudo dnf module reset mariadb -y
sudo dnf -y install MariaDB-server MariaDB-client MariaDB-backup
```
4.	 Inicie e habilitei o serviço mariadb 
```bash
sudo systemctl enable --now mariadb
```
5.	Confirmei se o status do serviço está em estado de execução 
```bash
sudo mariadb-secure-installation
```
Segui o passo a passo e realizei a criação da senha, além de outras configuração presente no script.

7.	Fiz login como root use para verificar se a senha definida está funcionando:
```bash
mysql -u root -p
```
8.	Pra finalizar, realizei o comando para verificar a versão do MariaDB.
```bash
MariaDB [(none)]> SELECT VERSION();
```