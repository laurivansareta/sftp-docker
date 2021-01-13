# sftp-docker
Projeto para criação de um container docker para SFTP

As informações usadas neste projeto são informações para finalidade de testes e devem ser alteradas se usadas em produção.

## Configurações

Para definir o usuário e senha padrão do administrador basta alterar as informações que estão no arquivo *.env*

## Executar no terminal

`docker-compose up -d` - Sobe os containers. Se não tiver a imagem vai baixar.

## Depois de subir o container vai ser necessário acessar o bash do container ou via ssh.

**Conectar pelo container:**

primeiro identificar o nome do container: `docker ps`, neste caso 'sftpdocker_server_1'

para isso executar: `docker exec -it sftpdocker_server_1 /bin/bash`

**Conectar pelo SSH**

comando `ssh master@container-ip -p 22`

## Depois de conectado:

**Para acessar SFTP:**

`sftp inanzzz@container-ip`

Agora é só executar os [comandos](https://winscp.net/eng/docs/scripting#commands) de navegação e manipulação dos arquivos.

**Para criar novo usuário:**

`sudo mkdir /uploads/inanzzz`

`sudo mkdir /uploads/inanzzz/upload`

`sudo useradd -d /uploads/inanzzz -G sftp inanzzz -s /usr/sbin/nologin`

`echo "inanzzz:inanzzz" | sudo chpasswd`

`sudo chown inanzzz:sftp -R /uploads/inanzzz/upload`

## Conectar com filezilla

* Host: container-ip 
* Port: 2222
* Protocol: SFTP
* Logon Type: Ask for password
* Username: inanzzz
* Password: inanzzz


## Fonte
http://www.inanzzz.com/index.php/post/6fa7/creating-a-ssh-and-sftp-server-with-docker-compose
