# SGCE

Procedimentos aplicados durante instalação do SGCE

Repositório Oficial: https://softwarepublico.gov.br/social/sgce

## Pós-instalação Ubuntu Server

Entre com o comando $sudo passwd root, ele irá solicitar a senha que você cadastrou na instalação e depois pedirá para você inserir uma senha para o usuário root.

## Instalação Apache, PHP 5 e PostgreSQL

```bash
sudo add-apt-repository ppa:ondrej/php 
sudo apt-get update 
sudo apt-get install apache2 php5.6 libapache2-mod-php5.6 postgresql php5.6-pgsql phppgadmin php-gettext php5.6-gd php5.6-mcrypt
```

## Selecionar a versão padrão do PHP

```bash
sudo update-alternatives --set php /usr/bin/php5.6
```

## Alternar versão do PHP 7.3 para 5.6

```bash
sudo a2dismod php7.3
sudo a2enmod php5.6
sudo service apache2 restart
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



## Arquivo Modelo de CSV

[Modelo CSV](modelo_csv.csv)



## Referências

[Apresentação VWTICIFES 2011](docs/Apresentacao-VWTICIFES-2011.pdf)

[Artigo VWTICIFES 2011](docs/Artigo-VWTICIFES-2011.pdf)

[Instalação](docs/instalacao-sgce.pdf)

[Manual](docs/manual-sgce.pdf)

[Manual UTFPR](docs/sgce_utfpr_organizador.pdf)


