# SGCE

Procedimentos aplicados durante instalação do SGCE

Repositório Oficial: https://softwarepublico.gov.br/social/sgce



## Pós-instalação Ubuntu Server

Entre com o comando $sudo passwd root, ele irá solicitar a senha que você cadastrou na instalação e depois pedirá para você inserir uma senha para o usuário root.



## Instalação Apache, PHP 5 e PostgreSQL

```bash
sudo add-apt-repository ppa:ondrej/php 
sudo apt-get update 
sudo apt-get install apache2 php5 libapache2-mod-php5 postgresql php5-pgsql phppgadmin php-gettext php5-gd
```



## Remover limitação pgpgadmin de executar apenas localmente

```bash
sudo nano /etc/apache2/conf-enabled/phppgadmin.conf
```

comentar a linha:

```ini
#Require local
```

## Configurar o endereço da aplicação

```bash
sudo nano /var/www/html/sgce/system/application/config/config.php
```

edite a chave $config['base_url'] e coloque o endereço raiz do sistema

edite a chave $config['encryptiuon_key'] e coloque uma chave válida de 32 caracteres alfanumericos


## Contantes utilizadas

```bash
sudo nano /var/www/html/sgce/system/application/config/constants.php
```



## Permissões de arquivos

```bash
 sudo chown www-data:www-data /var/www/html/sgce/ 
 sudo chown www-data:www-data /var/www/html/sgce/* -R 
 sudo chmod 775 /var/www/html/sgce 
 sudo chmod 775 /var/www/html/sgce/* -R
```



## Imagem de Cabeçalho

/sgce/system/application/views/includes/images/topo-certificados.jpg



## Programa Editor CSV para windows

CSVed - https://csved.sjfrancke.nl/
