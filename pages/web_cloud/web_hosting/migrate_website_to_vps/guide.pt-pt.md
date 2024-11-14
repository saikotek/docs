---
title: "Como migrar um website a partir de um alojamento web partilhado para um VPS"
excerpt: "Saiba como migrar o seu website de um alojamento partilhado para um VPS OVHcloud"
updated: 2024-11-06
---

## Objetivo

O seu website evolui e o seu consumo de recursos é tal que o seu alojamento web já não corresponde às suas necessidades em termos de performance ou em termos de capacidade para tratar tarefas mais complexas. Migrar para um VPS permite melhorar a rapidez e a reatividade do seu website, aumentar os recursos de cálculo disponíveis (CPU, RAM, etc.) e ter mais controlo sobre o ambiente do servidor. Este guia centra-se nas etapas essenciais para migrar eficazmente para um VPS, garantindo a continuidade do serviço.

**Saiba como migrar o seu website de um alojamento partilhado para um VPS.**

## Requisitos

- Ter um [plano de alojamento web](/links/web/hosting) ativo.
- Ter subscrito um [VPS](/links/bare-metal/vps) presente na sua conta OVHcloud.
- Ter acesso à [Área de Cliente OVHcloud](/links/manager).

## Instruções

> [!warning]
>
> A OVHcloud oferece-lhe serviços cuja configuração, gestão e responsabilidade é da sua responsabilidade. Assim, deverá assegurar o seu bom funcionamento.
>
> Este guia fornece as instruções necessárias para realizar as operações mais habituais. Se encontrar dificuldades, recomendamos que recorra a um [fornecedor especializado](/links/partner). Não poderemos proporcionar-lhe assistência técnica. Para mais informações, consulte a secção ["Quer saber mais?"](#go-further) deste guia.
>

### Etapa 1 - Efetuar o backup dos ficheiros e da base de dados do seu website <a name="step1"></a>

O primeiro passo consiste em guardar o conjunto dos ficheiros do seu website, geralmente via o **F**ile **T**ransfer **P**rotocol (**FTP**), bem como a sua base de dados.

Se utilizar o WordPress, siga o nosso guia "[Faça o backup do seu site WordPress](/pages/web_cloud/web_hosting/how_to_backup_your_wordpress)" para saber como efetuar a cópia de segurança de ficheiros e da base de dados do seu website WordPress e, em seguida, prossiga para [etapa 2](#step2).

#### Etapa 1.1 - Ligar-se ao espaço de armazenamento FTP do seu alojamento web

Siga as etapas do nosso guia "[Aceder ao espaço de armazenamento FTP do alojamento web](/pages/web_cloud/web_hosting/ftp_connection)" para se ligar ao espaço de armazenamento FTP do seu alojamento web.

#### Etapa 1.2 - Efetuar o backup dos ficheiros via FTP <a name="step1.2"></a>

Se não utiliza um CMS (WordPress, Joomla!, Drupal, PrestaShop, etc.), descarregue uma cópia de segurança completa do conjunto dos ficheiros presentes no seu espaço FTP para o seu dispositivo localmente. Inclui todos os ficheiros HTML, CSS, JavaScript, imagens e ficheiros de configuração (`config.php`, `.env`, etc.) que constituem o seu website. Certifique-se de que recupera completamente as pastas e ficheiros do diretório raiz (frequentemente nomeado `public_html` ou `www`) para que o conjunto do conteúdo necessário ao funcionamento do seu website seja guardado para a migração.

Se utilizar um CMS e pretender efetuar a cópia de segurança dos ficheiros, clique no respetivo separador para selecionar o método de cópia de segurança mais adequado.

> [!tabs]
> PrestaShop
>>
>> Para PrestaShop, guarde os diretórios críticos tais como:
>>
>> - `/admin` : para os ficheiros relativos ao back-office.
>> - `/modules` : para os módulos instalados.
>> - `/img` : para todas as imagens e ícones.
>> - `/themes` : para os ficheiros do tema do seu site.
>>
>> Para mais pormenores sobre a estrutura dos ficheiros PrestaShop, consulte a sua [documentação técnica oficial](https://docs.prestashop-project.org/welcome).
>>
> Joomla!
>>
>> Para o Joomla!, os ficheiros de backup importantes incluem diretórios:
>>
>> - `/administrator` : para a interface de administração.
>> - `/components`, `/plugins` : para as extensões instaladas.
>> - `/images` : para os ficheiros mediáticos do seu site.
>>
>> Encontre mais informações sobre a estrutura dos ficheiros Joomla! na [documentação oficial do Joomla!](https://docs.joomla.org/).
>>
> Drupal
>>
>> Para Drupal, as pastas importantes para fazer backup são:
>>
>> - `/sites` : que contém os ficheiros específicos ao seu site.
>> - `/modules` : et `/themes` : para os módulos e temas personalizados.
>>
>> Para obter mais informações, consulte a [documentação oficial do Drupal]((https://www.drupal.org/docs).

> [!primary]
>
> Após descarregar o conjunto dos ficheiros do seu website, certifique-se de que os armazena numa pasta local facilmente identificável para facilitar a sua posterior transferência para o VPS.

#### Etapa 1.3 - Fazer backup da base de dados

> [!primary]
>
> Se já utiliza uma base de dados Web Cloud Database para o seu website, pode continuar a utilizá-la sem a migrar. O seu VPS será ligado à base de dados Web Cloud Database para gerir os dados.

Se pretender migrar a base de dados para o VPS, siga as etapas do nosso guia "[Recuperar a cópia de segurança da base de dados de um alojamento web](/pages/web_cloud/web_hosting/sql_database_export)" para salvaguardar a sua base de dados.

### Etapa 2 - Configurar o seu VPS <a name="step2"></a>

> [!primary]
>
> Se ainda não tiver VPS, aceda a [página do produto VPS OVHcloud](/links/bare-metal/vps) para adquirir um VPS. Certifique-se de que escolhe um VPS que corresponde às necessidades do seu website em termos de recursos (RAM, CPU, armazenamento, etc.) e às especificações técnicas do seu CMS. Se não está familiarizado com os VPS, consulte o guia "[Primeiros passos com um VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)".

#### Etapa 2.1 - Aceder ao VPS

Consulte a secção "Ligar-se ao seu VPS" do guia "[Primeiros passos com um VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)" para se ligar ao seu VPS.

#### Etapa 2.2 - Instalar e configurar um servidor web no seu VPS <a name="step2.2"></a>

Depois de aceder ao VPS, instale e configure um ambiente de desenvolvimento web no VPS. Esta etapa é essencial para garantir que o seu servidor esteja pronto para acolher o seu website depois de transferir os ficheiros e a base de dados.

Para instalar este ambiente web, consulte o guia "[Instalar um ambiente de desenvolvimento web num VPS ou num servidor dedicado](/pages/bare_metal_cloud/virtual_private_servers/install_env_web_dev_on_vps)".

### Etapa 3 - Transferir os ficheiros do seu website através de SFTP

Utilizar o **S**ecure **F**ile **T**ransfer **P**rotocol (**SFTP**) é o método recomendado para a transferência de ficheiros do seu website para o seu VPS. Este serviço oferece um nível de segurança superior ao FTP, graças à utilização da encriptação fornecida pelo serviço SSH, que já se encontra ativado por predefinição no VPS da OVHcloud.

#### Etapa 3.1 - Ligar-se ao seu VPS em SFTP

Siga a etapa "Lançar a ligação SFTP" do nosso guia "[Utilizar o FileZilla com o seu alojamento OVHcloud](/pages/web_cloud/web_hosting/ftp_filezilla_user_guide)" utilizando a seguinte configuração:

- **Host** : utilize o endereço IP do seu VPS.
- **Identificador** e **palavra-passe** : os da sua conta de utilizador SSH no VPS.
- **Porta** : utilize a porta 22 (porta predefinida para SFTP).

#### Etapa 3.2 - Transferir os ficheiros do seu website para o VPS

Depois de aceder ao VPS, a árvore de ficheiros locais aparece à esquerda da interface FileZilla e a árvore de ficheiros do VPS à direita.

Selecione os ficheiros do seu website e a base de dados que descarregou durante a [etapa 1.2](#step1.2). Arraste-os para o diretório web do seu VPS à direita da interface. O diretório web é o local onde os ficheiros do seu website serão armazenados para poderem ser acedidos na Internet. Por predefinição, pode ser uma pasta chamada `/var/www/html` ou outra pasta configurada durante a instalação do servidor web no [etapa 2.2](#step2.2). Certifique-se de colocar os seus ficheiros na pasta configurada como raiz web para que o seu website funcione corretamente.

### Etapa 4 - Importar a base de dados para o seu VPS (facultativo)

> [!warning]
>
> Se a base de dados já estiver alojada num serviço Web Cloud Databases, não é necessário migrá-la para o VPS. Pode conservar a base de dados no serviço Web Cloud Databases e configurar o seu VPS para aceder à base de dados ([etapa 5](#step5)).

Se pretender importar a base de dados para o seu VPS, siga os passos abaixo.

Aceda ao VPS em SSH. Consulte a secção "Ligar-se ao VPS" do guia "[Primeiros passos com um VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)".

Quando estiver conectado ao VPS por SSH, utilize a linha de comandos abaixo para realizar a importação da base de dados.

No exemplo abaixo, utilizamos MySQL como **S**istema de **G**estão de **B**ase de dados **D**ados (**SGBD**). Utilize a documentação oficial do SGBD que instalou durante a [etapa 2.2](#step2.2) para utilizar a linha de comandos adequada para importar a base de dados para o seu VPS.

```php
<?php
system("mysql -u user_name -p db_name < root/to/file.sql
");
?>
```

Substitua `user_name` pelo seu nome de utilizador MySQL, `db_name` pelo nome da base de dados a importar, e `root/to/file.sql` pelo caminho do ficheiro SQL guardado.

### Etapa 5 - Configurar os ficheiros de configuração do seu website <a name="step5"></a>

Depois de ter transferido os ficheiros do seu website e, se for caso disso, importado a base de dados para o seu VPS, é importante que atualize os ficheiros de configuração do seu website para garantir o seu bom funcionamento. As variáveis principais a ajustar são muitas vezes as informações de conexão ao banco de dados, bem como os caminhos para as pastas. Estas são as configurações específicas a serem atualizadas para os principais CMS.

> [!tabs]
> WordPress
>>
>> Modifique as seguintes variáveis no ficheiro `wp-config.php`:
>>
>> - **DB_NAME** : o nome da base de dados.
>> - **DB_USER** : o utilizador da base de dados.
>> - **DB_PASSWORD** : a palavra-passe do utilizador.
>> - **DB_HOST** : o host da base de dados (geralmente localhost num VPS).
>>
>> Para mais pormenores, consulte a [documentação oficial do WordPress](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/).
>>
>> Para evitar problemas de segurança, consulte a documentação oficial sobre [permissões de ficheiros para WordPress](https://wordpress.org/support/article/changing-file-permissions/)
>>
> PrestaShop
>>
>> Modifique as seguintes variáveis no ficheiro `parameters.php`:
>>
>> - **database_host** : o host da base de dados.
>> - **database_name** : o nome da base de dados.
>> - **database_user** : o utilizador da base de dados.
>> - **database_password** : a palavra-passe da base de dados.
>>
>> Para mais informações, consulte a [documentação oficial do PrestaShop](https://devdocs.prestashop-project.org/8/development/configuration/configuring-prestashop/).
>>
>> Para evitar problemas de segurança, consulte a [documentação oficial](https://devdocs.prestashop-project.org/) sobre as permissões dos ficheiros para PrestaShop.
>>
> Joomla!
>>
>> Modifique as seguintes variáveis no ficheiro `configuration.php`:
>>
>> - **public $host** : o host da base de dados (por vezes, localhost).
>> - **public $db** : o nome da base de dados.
>> - **public $user** : o utilizador da base de dados.
>> - **public $password** : a palavra-passe da base de dados.
>>
>> Para mais pormenores, consulte a [documentação oficial do Joomla!](https://docs.joomla.org/).
>>
>> Para evitar problemas de segurança, consulte a documentação oficial das [permissões dos ficheiros para Joomla!](https://docs.joomla.org/What_are_the_recommended_file_and_directory_permissions%3F)
>>
> Drupal
>>
>> Modifique as seguintes variáveis no ficheiro `settings.php`:
>>
>> - **host** : o host da base de dados (com frequência, localhost).
>> - **database** : o nome da base de dados.
>> - **username** : o utilizador da base de dados.
>> - **password** : a palavra-passe da base de dados.
>>
>> Para mais informações, consulte a [documentação oficial do Drupal](https://www.drupal.org/documentation).
>>
>> Para evitar problemas de segurança, consulte a documentação oficial das [permissões dos ficheiros para Drupal](https://www.drupal.org/docs/administering-a-drupal-site/security-in-drupal/securing-file-permissions-and-ownership)
>>
> Sem CMS
>>
>> **1. Atualizar as informações de início de sessão da base de dados**
>>
>> Identifique os ficheiros de configuração (como `config.php` ou `.env`). Algumas podem estar situadas em subpastas. Nesses ficheiros, procure os parâmetros de ligação à base de dados e modifique-os em função dos novos valores de ligação do VPS:
>>
>> - **DB_HOST** : endereço do servidor de base de dados.
>> - **DB_NAME** : nome da base de dados.
>> - **DB_USER** : utilizador da base de dados.
>> - **DB_PASSWORD** : password.
>>
>> **2. Configurar os caminhos para os ficheiros**
>>
>> Alguns websites utilizam caminhos absolutos (por exemplo: `/home/user/public_html/`) para ficheiros ou recursos específicos, tais como imagens, ficheiros CSS, etc. Verifique se estes caminhos são adequados à estrutura do servidor no VPS, por exemplo, `/var/www/html/`.
>>
>> Para evitar erros de carregamento de ficheiros ou links quebrados, certifique-se de que os ajusta em todos os ficheiros de configuração, `.htaccess`, ou outros scripts que contenham ligações para estes recursos. Isto assegura que o Web site encontra corretamente todos os itens que necessita para funcionar corretamente, mesmo após a migração.
>>
>> **3. Alterar o ficheiro .htaccess** (facultativo)
>>
>> Assegure-se de que o ficheiro `.htaccess` está corretamente configurado para o novo ambiente. Se utilizar regras de reescrita (`RewriteRule`) para personalizar os URLs, verifique se os caminhos são adaptados à estrutura do seu VPS (por exemplo: `/var/www/html/` em vez de `/public_html/`). Isto garante o bom funcionamento dos reencaminhamentos e dos acessos.
>>
>> Se o ficheiro `.htaccess` incluir restrições de acesso ou parâmetros de segurança, como a desativação da lista de diretórios ou a configuração da colocação em cache, modifique estas definições para que correspondam às configurações e condições de segurança do seu novo servidor.
>>
>> **4. Configurar as permissões dos ficheiros e das pastas**
>>
>> Certifique-se de que as permissões (exemplo: `chmod`) dos ficheiros e pastas estão configuradas corretamente para evitar erros de acesso. Num VPS, as permissões recomendadas são frequentemente `755` para as pastas e `644` para os ficheiros, mas isso pode variar em função das suas necessidades de segurança.

Se utilizar uma base de dados Web Cloud Databases, certifique-se de que o seu VPS está autorizado a ligar-se a ela. Para isso, adicione o endereço IP do VPS à lista dos endereços IP autorizados. Esta configuração permite proteger o acesso à base de dados e evitar problemas de ligação. Consulte a secção "Autorizar um endereço IP" do nosso guia "[Web Cloud Databases - primeira utilização](/pages/web_cloud/web_cloud_databases/starting_with_clouddb)".

### Etapa 6 - Associar o seu domínio ao endereço IP do VPS

> [!primary]
>
> Antes de alterar os registos da sua zona DNS para apontar para o endereço IP do VPS, recomenda-se que reduza o **T**ime **T**o **L**ive (**TTL**). Isto permite uma rápida propagação das alterações, uma vez que os servidores DNS irão atualizar as informações mais rapidamente. Siga a etapa "O tempo de propagação" do nosso guia "[Editar uma zona DNS da OVHcloud](/pages/web_cloud/domains/dns_zone_edit)" para ajustar o TTL e configurar os registos a fim de apontar o domínio para o VPS.

Para apontar o nome de domínio do seu website para o seu VPS, configure os registos DNS do nome de domínio para que direcionem o tráfego para o endereço IP público do seu VPS. Para o orientar, consulte o guia "[Editar uma zona DNS da OVHcloud](/pages/web_cloud/domains/dns_zone_edit)".

### Etapa 7 - Verifique o bom funcionamento do seu website

Quando a migração estiver concluída, teste o seu website para saber que está a funcionar como esperado. Verifique todas as funcionalidades essenciais (formulários, ligações do utilizador, pagamento online, etc.) e certifique-se de que todas as páginas são apresentadas corretamente.

### Etapa 8 - Proteger o seu VPS

Após ter migrado o seu website para o seu VPS, é crucial proteger o seu servidor de forma a proteger os dados e garantir o bom funcionamento dos seus serviços. Para reforçar a segurança do seu VPS, pode tomar as seguintes medidas:

- Alterar a palavra-passe SSH e a porta de acesso SSH predefinidas, fornecidas pela OVHcloud.
- Configurar uma firewall.
- Configurar a autenticação com dois fatores (2FA).
- Monitorizar os logs.
- etc.

Para uma lista completa das boas práticas de segurança, consulte o guia "[Proteger um VPS](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps)".

## Quer saber mais? <a name="go-further"></a>
 
Para serviços especializados (referenciamento, desenvolvimento, etc), contacte os [parceiros OVHcloud](/links/partner).
 
Fale com nossa [comunidade de utilizadores](/links/community).