# SGCE

Procedimentos aplicados durante instalação do SGCE

Repositório Oficial: https://softwarepublico.gov.br/social/sgce

## Pós-instalação Ubuntu Server

Entre com o comando $sudo passwd root, ele irá solicitar a senha que você cadastrou na instalação e depois pedirá para você inserir uma senha para o usuário root.

## Instalação Apache, PHP 5 e PostgreSQL

```bash
sudo add-apt-repository ppa:ondrej/php 
sudo apt-get update 
sudo apt-get install apache2 php5.6 libapache2-mod-php5.6 postgresql php5.6-pgsql phppgadmin php-gettext php5.6-gd php5.6-mcrypt php5.6-intl php5.6-cli php5.6-soap php5.6-curl php5.6-mbstring php5.6-xml php5.6-fpm
```

## Selecionar a versão padrão do PHP

```bash
sudo update-alternatives --set php /usr/bin/php5.6
```

## Alternar versão do PHP 7.3 para 5.6

```bash
sudo a2dismod php7.3
sudo a2enmod php5.6
sudo service apache2 restart
```

## Habilitar short_open_tag

A partir do PHP 5.3 foi depreciado, por isso a justificativa de ativar.

```bash
sudo nano /etc/php/5.6/php.ini
```

```apacheconf
short_open_tag = on
```

## Ativar a biblioteca GD2

Por padrão a biblioteca vem desativada. Para ativar, remova o comentário abaixo.

```bash
sudo nano /etc/php/5.6/php.ini
```

```apacheconf
extension=php_gd2.dll 
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

altere o endereço informado na chave *URL_certificado*.

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

[Apresentação V Workshop de TIC das IFES - Unipampa 2011](docs/Apresentacao-VWTICIFES-2011.pdf)

[Artigo Sistema de Gestão de Certificado Eletrônicos 2011](docs/Artigo-VWTICIFES-2011.pdf)

[Manual de Instalação Oficial - Unipampa 2016](docs/instalacao-sgce.pdf)

[Manual do Usuário Oficial - Unipampa 2016 ](docs/manual-sgce.pdf)

[Manual SGCE IFRS 2014](docs/manual-sgce-ifrs.pdf)

[Manual Organizador UTFPR 2017](docs/sgce_utfpr_organizador.pdf)
