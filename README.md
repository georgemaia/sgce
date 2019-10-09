# SGCE

Procedimentos aplicados durante instalação do SGCE 1.0.3 utilizando o framework Codeigniter versão 1.7.3.

Página Oficial: [https://dtic.unipampa.edu.br/sgce](https://dtic.unipampa.edu.br/sgce)

Repositório Oficial: [https://softwarepublico.gov.br/social/sgce](https://softwarepublico.gov.br/social/sgce)

Projeto no Gitlab: [https://softwarepublico.gov.br/gitlab/sgce/sgce](https://softwarepublico.gov.br/gitlab/sgce/sgce)

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
sudo nano /etc/php/5.6/apache2/php.ini
```

```apacheconf
short_open_tag = on
```

## Ativar a biblioteca GD2

Por padrão a biblioteca vem desativada. Para ativar, remova o comentário abaixo.

```bash
sudo nano /etc/php/5.6/apache2/php.ini
```

```apacheconf
extension=php_gd2.dll 
```

## Habilitar  PHP 5.6 FPM

```bash
a2enmod proxy_fcgi setenvif
a2enconf php5.6-fpm
```

## Remover limitação pgpgadmin de executar apenas localmente

```bash
sudo nano /etc/apache2/conf-enabled/phppgadmin.conf
```

comentar a linha:

```ini
#Require local
```
## Cadastrar usuário do Banco Postgres

```bash
sudo -u postgres psql
```

```
CREATE USER sgce SUPERUSER INHERIT CREATEDB CREATEROLE;
ALTER USER sgce PASSWORD '12345678';
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

## DOMPDF

Visão Geral: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/) - [PDF](docs/dompdf_overview.pdf)

Install: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/install.php) - [PDF](docs/dompdf_install.pdf)

Usage: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/usage.php) - [PDF](docs/dompdf_usage.pdf)

FAQ: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/faq.php) - [PDF](docs/dompdf_faq.pdf)

[Versão 0.6.2 no Github](https://github.com/dompdf/dompdf/tree/0.6.2-hotfix)

[Conver HTML to PDF with Dompdf - Sitepoint](https://www.sitepoint.com/convert-html-to-pdf-with-dompdf/)

## Constantes 

Para configurar as mensagens, utilize as seguintes constantes:

**NOME_PARTICIPANTE** - Especifica que nesta posição do texto será escrito o nome do participante que receberá o certificado.

**NOME_EVENTO** - Especifica o nome do evento que emitiu a notificação.

**EMAIL_EVENTO** - Especifica o e-mail de contato dos organizadores do evento.

**LINK_CERTIFICADO** - Imprime o link que será utilizado para emissão do certificado.

**IDENTIFICACAO_CERTIFICADO** - Escreve o código de validação do certificado. 

**DESCRICAO_STATUS** - Informa o status do certificado (se validado ou revogado).

**DESCRICAO_JUSTIFICATIVA** - Informa a justificativa do Avaliador. 

**NOTA**: Os campos NOME_PARTICIPANTE, NOME_EVENTO e EMAIL_EVENTO podem ser utilizados na configuração de todas as mensagens, pois referem-se à pessoa que receberá o e-mail. das duas mensagens. O campo LINK_CERTIFICADO é específico para a notificação de Emissão e os campos
IDENTIFICAÇÃO_CERTIFICADO, DESCRICAO_STATUS e DESCRICAO_JUSTIFICATIVA são usados apenas na notificação de validação/revogação de certificados.

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
