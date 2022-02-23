# SGCE

<!-- TOC -->

- [SGCE](#sgce)
    - [Configuração para Desenvolvimento](#configura%C3%A7%C3%A3o-para-desenvolvimento)
        - [Pós-instalação Ubuntu Server](#p%C3%B3s-instala%C3%A7%C3%A3o-ubuntu-server)
            - [Instalação Apache, PHP 5 e PostgreSQL](#instala%C3%A7%C3%A3o-apache-php-5-e-postgresql)
            - [Selecionar a versão padrão do PHP](#selecionar-a-vers%C3%A3o-padr%C3%A3o-do-php)
            - [Alternar versão do PHP 7.3 para 5.6](#alternar-vers%C3%A3o-do-php-73-para-56)
            - [Habilitar short_open_tag](#habilitar-short_open_tag)
            - [Ativar a biblioteca GD2](#ativar-a-biblioteca-gd2)
            - [Habilitar  PHP 5.6 FPM](#habilitar--php-56-fpm)
            - [Remover limitação pgpgadmin de executar apenas localmente](#remover-limita%C3%A7%C3%A3o-pgpgadmin-de-executar-apenas-localmente)
            - [Cadastrar usuário do Banco Postgres](#cadastrar-usu%C3%A1rio-do-banco-postgres)
            - [Configurar o endereço da aplicação](#configurar-o-endere%C3%A7o-da-aplica%C3%A7%C3%A3o)
            - [Contantes utilizadas](#contantes-utilizadas)
            - [Permissões de arquivos](#permiss%C3%B5es-de-arquivos)
            - [Refresh do apache](#refresh-do-apache)
            - [Imagem de Cabeçalho](#imagem-de-cabe%C3%A7alho)
            - [Configurar envio de email](#configurar-envio-de-email)
            - [Alterar método de envio para o sendmail](#alterar-m%C3%A9todo-de-envio-para-o-sendmail)
                - [Passo 1: Instalar o sendmail](#passo-1-instalar-o-sendmail)
                - [Passo 2: Configure o sendmail](#passo-2-configure-o-sendmail)
                - [Passo 3 Opicional: Edite o arquivo hosts](#passo-3-opicional-edite-o-arquivo-hosts)
                - [Passo 4: Reinicie o servidor Web](#passo-4-reinicie-o-servidor-web)
            - [SSH](#ssh)
            - [Ativar o log no Codeigniter](#ativar-o-log-no-codeigniter)
    - [DOMPDF](#dompdf)
    - [Constantes](#constantes)
    - [Programa Editor CSV para windows](#programa-editor-csv-para-windows)
    - [Arquivo Modelo de CSV](#arquivo-modelo-de-csv)
    - [Contributing](#contributing)
    - [Referências](#refer%C3%AAncias)

<!-- /TOC -->

[![Product Name Screen Shot][product-screenshot]](https://dtic.unipampa.edu.br/sgce)

Procedimentos aplicados durante instalação do SGCE 1.0.3 utilizando o framework [Codeigniter](https://codeigniter.com/) versão 1.7.3 no Ubuntu.

Página Oficial: [https://dtic.unipampa.edu.br/sgce](https://dtic.unipampa.edu.br/sgce) - Fora do ar. Visitada dia 23/02/2022.

Repositório Oficial: [https://softwarepublico.gov.br/social/sgce](https://softwarepublico.gov.br/social/sgce)

Projeto no Gitlab: [https://softwarepublico.gov.br/gitlab/sgce/sgce](https://softwarepublico.gov.br/gitlab/sgce/sgce)

---

## Configuração para Desenvolvimento

### Pós-instalação Ubuntu Server

Entre com o comando abaixo , ele irá solicitar a senha que você cadastrou na instalação e depois pedirá para você inserir uma senha para o usuário root.

 ```
 $sudo passwd root
 ```

---

#### Instalação Apache, PHP 5 e PostgreSQL

```bash
sudo add-apt-repository ppa:ondrej/php 
sudo apt-get update 
sudo apt-get install apache2 php5.6 libapache2-mod-php5.6 postgresql php5.6-pgsql phppgadmin php-gettext php5.6-gd php5.6-mcrypt php5.6-intl php5.6-cli php5.6-soap php5.6-curl php5.6-mbstring php5.6-xml php5.6-fpm
```
---

#### Selecionar a versão padrão do PHP

```bash
sudo update-alternatives --set php /usr/bin/php5.6
```

---

#### Alternar versão do PHP 7.3 para 5.6

```bash
sudo a2dismod php7.3
sudo a2enmod php5.6
sudo service apache2 restart
```

---

#### Habilitar short_open_tag

A partir do PHP 5.3 foi depreciado, por isso a justificativa de ativar.

```bash
sudo nano /etc/php/5.6/apache2/php.ini
```

```apacheconf
short_open_tag = on
```

---

#### Ativar a biblioteca GD2

Por padrão a biblioteca vem desativada. Para ativar, remova o comentário abaixo.

```bash
sudo nano /etc/php/5.6/apache2/php.ini
```

```apacheconf
extension=php_gd2.dll 
```

---

#### Habilitar  PHP 5.6 FPM

```bash
a2enmod proxy_fcgi setenvif
a2enconf php5.6-fpm
```

---

#### Remover limitação pgpgadmin de executar apenas localmente

```bash
sudo nano /etc/apache2/conf-enabled/phppgadmin.conf
```

comentar a linha:

```ini
#Require local
```

---

#### Cadastrar usuário do Banco Postgres

```bash
sudo -u postgres psql
```

```
CREATE USER sgce SUPERUSER INHERIT CREATEDB CREATEROLE;
ALTER USER sgce PASSWORD '12345678';
```

---

#### Configurar o endereço da aplicação

```bash
sudo nano /var/www/html/sgce/system/application/config/config.php
```

edite a chave $config['base_url'] e coloque o endereço raiz do sistema

edite a chave $config['encryptiuon_key'] e coloque uma chave válida de 32 caracteres alfanumericos

---

#### Contantes utilizadas

```bash
sudo nano /var/www/html/sgce/system/application/config/constants.php
```

altere o endereço informado na chave *URL_certificado*.

---

#### Permissões de arquivos

```bash
 sudo chown www-data:www-data /var/www/html/sgce/ 
 sudo chown www-data:www-data /var/www/html/sgce/* -R 
 sudo chmod 775 /var/www/html/sgce 
 sudo chmod 775 /var/www/html/sgce/* -R
```

---

#### Refresh do apache

```html
<meta http-equiv="refresh" content="0; url=./sgce">
```

---

#### Imagem de Cabeçalho

/sgce/system/application/views/includes/images/topo-certificados.jpg


#### Configurar envio de email

Caso seja configurado com um email do gmail, deve-se ativar o envio por plataformas menos seguras:

[https://myaccount.google.com/lesssecureapps?pli=1](https://myaccount.google.com/lesssecureapps?pli=1)

/system/application/config/email.php

```php
    $config['protocol']  = 'smtp';
    $config['smtp_host'] = 'smtp.unipampa.edu.br';
    $config['smtp_user'] = ''; 
    $config['smtp_pass'] = ''; 
    $config['smtp_port'] = 25;
    $config['charset']   = 'utf-8';
    $config['wordwrap']  = TRUE;
    $config['mailtype']  = 'html';

    //campos adicionais
    $config['mail_from_address'] = 'nao.responder@unipampa.edu.br';
    $config['mail_from_name']    = 'Nao Responder';
    $config['errors_to_address'] = 'erro@unipampa.edu.br';
```
/sgce/system/libraries/Email.php


Depois preencher a configuração dentro do menu Sistema, (inclusive o DNS) para que ele possa testar o envio de e-mails antes de enviá-los adequadamente.

#### Alterar método de envio para o sendmail

##### Passo 1: Instalar o sendmail

```
$ sudo apt-get install sendmail
```

##### Passo 2: Configure o sendmail

```
$ sudo sendmailconfig
```

##### Passo 3 (Opicional): Edite o arquivo hosts

```
$ sudo vim /etc/hosts
```

##### Passo 4: Reinicie o servidor Web 

Para servidores Apache:

```
$ sudo service apache2 restart
```

Para servidores Nginx:

```
$ sudo service nginx restart
```

Pronto!

---

#### SSH

Instalar

```bash
sudo apt-get install openssh-server
```

Ativar

```bash
sudo service ssh status
```

---

#### Ativar o log no Codeigniter

* torna a pasta /application/logs com permissões de escrita

* Edite o arquivo  /application/config/config.php de 1 a 4, com o numero mais alto mais detalho o log

```php
    $config['log_threshold'] = 1;
```

* use log_message('error', 'Some variable did not contain a value.');

* Para enviar email, você precisa extender o  core CI_Exceptions class method log_exceptions(). 

---

## DOMPDF

Visão Geral: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/) - [PDF](docs/dompdf_overview.pdf)

Install: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/install.php) - [PDF](docs/dompdf_install.pdf)

Usage: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/usage.php) - [PDF](docs/dompdf_usage.pdf)

FAQ: [link](http://www.kassas.nl/webshopkeeper/config/dompdf/www/faq.php) - [PDF](docs/dompdf_faq.pdf)

[Versão 0.6.2 no Github](https://github.com/dompdf/dompdf/tree/0.6.2-hotfix)

[Conver HTML to PDF with Dompdf - Sitepoint](https://www.sitepoint.com/convert-html-to-pdf-with-dompdf/)

---

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

---

## Programa Editor CSV para windows

CSVed - [https://csved.sjfrancke.nl/](https://csved.sjfrancke.nl/)

Visual Studio Code Extension Edit CSV - [https://marketplace.visualstudio.com/items?itemName=janisdd.vscode-edit-csv](https://marketplace.visualstudio.com/items?itemName=janisdd.vscode-edit-csv)

---

## Arquivo Modelo de CSV

[Modelo CSV](modelo_csv.csv)

---

## Contributing

1. Faça o _fork_ do projeto (<https://github.com/yourname/yourproject/fork>)
2. Crie uma _branch_ para sua modificação (`git checkout -b feature/fooBar`)
3. Faça o _commit_ (`git commit -am 'Add some fooBar'`)
4. _Push_ (`git push origin feature/fooBar`)
5. Crie um novo _Pull Request_

---


## Referências

[Apresentação V Workshop de TIC das IFES - Unipampa 2011](docs/Apresentacao-VWTICIFES-2011.pdf)

[Artigo Sistema de Gestão de Certificado Eletrônicos 2011](docs/Artigo-VWTICIFES-2011.pdf)

[Manual de Instalação Oficial - Unipampa 2016](docs/instalacao-sgce.pdf)

[Manual do Usuário Oficial - Unipampa 2016 ](docs/manual-sgce.pdf)

[Manual SGCE IFRS 2014](docs/manual-sgce-ifrs.pdf)

[Manual Organizador UTFPR 2017](docs/sgce_utfpr_organizador.pdf)

[CodeIgniter User Guide Version 1.7.2](docs/CodeIgniter_User_Guide_Version_1.7.2.pdf)

[Enable PHP mail() function on Ubuntu](http://researchhubs.com/post/computing/linux-basic/enable-php-mail-function-to-work-on-ubuntu.html)

<!-- MARKDOWN LINKS & IMAGES -->
[product-screenshot]: img/indice.png