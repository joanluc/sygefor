SYGEFOR3
========================

Qué Sygefor3 ?
-----------------

Sygefor3 qu'ei ua solucion de gestion de formacions concebut per l'Associacion deu Hialat deus URFIST, puish enriquida per l'adCRFCB atau com lo CNRS. Qu'ei estada realizada per [Conjecto](http://www.conjecto.com/).
L'aplicacion que's presenta en ua interfàcia de gestion privada . Ua version publica de la solucion que permet aus estagiaris de s'inscríver a las formacions.
Ua API publica qu'ei egaument disponibla . Los tipes d'autentificacion OAuth2 e Shibboleth que son integrats a la solucion .

Demostracion
-----------------

Un version de demostracion de la solucion qu'ei disponibla a l'adreça : http://sygefor.conjecto.com.


Capturas d'ecran
-----------------

<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-dashboard.png?raw=true" title="Captura d'ecran deu dashboard" width="30%"/>
<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-list-searchbar.png?raw=true" title="Captura d'ecran de la vista que lista filtrada per la barra de recèrca" width="30%"/>
<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-trainee.png?raw=true" title="Captura d'ecran de la vista d'un estagiari" width="30%"/>
<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-mailing.png?raw=true" title="Captura d'ecran d'un qu'envia d'emails" width="30%"/>
<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-summary.png?raw=true" title="Captura d'ecran de la generacion deus bilanç" width="30%"/>
<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-front-home.png?raw=true" title="Captura d'ecran de la pagina d'arcuelh deu site public" width="30%"/>
<img src="https://raw.githubusercontent.com/conjecto/sygefor/master/assets/screen-front-profile.png?raw=true" title="Captura d'ecran de la partida que compta site public" width="30%"/>

Configuracion requerida
------------

### PHP

* version 5.3.9 minimum (lhevat 5.3.16). Php7 n'ei pas compatible per ara .
* extensions :
    * json
    * xml
	* zip
    * ctype
* modules :
    * pdo_mysql
	* openssl
    * apc
	* mbstring
    * curl
	* fileinfo

### Symfony2

Sygefor3 que s'apièja sus Symfony 2.8.

### MySQL

version 5.0 minimum

### ElasticSearch

Sygefor3 que s'apièja sus un servidor [ElasticSearch](http://www.elasticsearch.org/) qui gereish l'indexacion de l'ensemble
deus elements.

* version 1.4
 - Ajustar lo fichèr [elasticsearch.repo](https://github.com/sygefor/sygefor/blob/master/external_conf/elasticsearch.repo) dens lo repertòri /etc/yum.repaus.d/ entà CentOS
 - Ajustar "deb http://packages.elasticsearch.org/elasticsearch/1.4/debian establa man" dens /etc/apt/honts.list entà Debian
 - Installar lo paquet elasticsearch

### Unoconv

La generacion deus PDF pendent un publipostage qu'ei hèita possibla gràcias a la libreria [Unoconv](https://github.com/dagwieers/unoconv)
qui deu donc èste installada suu servidor.

* version 0.7

### Shibboleth

Sygefor3 qu'utiliza la Federacion d'identitat Educacion-Recèrca de Renater entà perméter aus estagiaris de s'inscríver, peu
 protocòle Shibboleth. Que cau donc installar un Servici Provider suu servidor e ac declarar auprés de Renater :

[Installacion d'un SP Shibboleth](https://services.renater.fr/federation/docs/installation/sp#test_dans_la_federation_de_test)

### Docker
------------
 Un còp lo depaus clonat, rendètz-vos dens lo dossièr sygefor e qu'actualizatz los sòus-que modulas dab la comanda : 
 git submodule update --init

Que podetz puish utilizar docker entà lançar los servicis necessaris a Sygefor3. 
Lo docker-compose.yml que contien los cabeders dejà configurats .

Associar los drets a l'utilizator www-que datè entà entaus dossièrs : app/cache e app/logs :
 - sudo chown -R www-data. app/cache/
 - sudo chown -R www-data. app/logs/

Atencion a assabentar los bons paramètres dens app/config/parameters.yml. Que podetz remplaçar :
 - database_host per mysql
 - elasticsearch_host per elasticsearch
 - mailer_host per mailcatcher 

Que podetz associar los drets d'escritura a l'utilizator www-data entaus repertòris seguents :
 - var/Material
 - var/Publipost
 - /tmp/sygefor dens lo cabeder
 
Que podetz puish executar la comanda "docker-compose up -d" entà lançar los cabeders

[Installar docker](https://docs.docker.com/install/)

[Installar docker-compose](https://docs.docker.com/compose/install/#prerequisites)

Un còp los cabeders lançats, qu'executatz las comandas seguentas entà finalizar l'installacion :

 - docker exec -it sygefor_shibboleth compose install
 - docker exec -it sygefor_shibboleth yarn install
 - docker exec -it sygefor_shibboleth bower install --allow-root
 - docker exec -it sygefor_shibboleth php app/console doctrine:schema:create
 - docker exec -it sygefor_shibboleth php app/console doctrine:fixtures:load
 - docker exec -it sygefor_shibboleth php app/console fos:js-routing:dump
 - docker exec -it sygefor_shibboleth gulp build:dist
 - docker exec -it sygefor_shibboleth php app/console fos:elastica:populate

Que sufigó alavetz de s'anar sus localhost dab lo vòste navigator entà accedir au BO

Installacion de Sygefor3
------------

### Pre-requesit

- *Composer* installat : http://www.coolcoyote.net/php-mysql/installation-de-composer-sous-linux-et-windows
- *Openssl* installat
- *npm* installat
 - curl -sL https://deb.nodesource.com/setup_6.x | bash -
 - apt-get install npm
- *yarn*, *bower*, *gulp* e *n* installats (sudo npm install yarn bower gulp@3.9.1 n -g)
- *Node* dab la version 6.8 (sudo n 6.8.0)
- *Visual Studio Redistributables* installat entà Windows
- *libssl-dev* installat entà linux
- *Rewrite module* activat 

### Lo projècte

- git clone https ://github.com/sygefor/sygefor.git
- cd sygefor
- git submodule update --init
- composer install
 - Assabentar los paramètres symfony
- yarn install
- bower install
- php app/console doctrine:database:create
- php app/console doctrine:schema:create
- php app/console doctrine:fixtures:load (entà generar quauquas dadas iniciaus)
- php app/console fos:js-routing:dump
- gulp build:dist
- php app/console fos:elastica:populate
- php app/console server:run 127.0.0.1:8000
- S'anar sus localhost:8000 dab lo vòste navigator entà accedir au BO
- Se connectar dab los identificants admin/admin
- Ajustar ua entrada dens lo vòste fichèr host entà har puntar sygefor.com cap a 127.0.0.1
- S'anar sus sygefor.com:8000 dab lo vòste navigator entà accedir au FO

### API

Sygefor3 qu'intègra ua API disponibla dens ApiBundle. Qu'ei possible de reservar daubuas partidas de l'API aus utilizators connectats en OAuth2 o per Shibboleth.
L'API que permet sustot d'exportar [las formacions](http://sygefor.com:8000/api/training) e [las sessions de formacions](http://sygefor.com:8000/api/training/session).

### Export [LHEO](http://lheo.gouv.fr/description)

Sygefor3 qu'intègra un [export LHEO](http://sygefor.com:8000/api/lheo/sygefor) de las formacions.

### Espandir

Lo còr de Sygefor3 qu'ei integrat dens los sòus-modulas projècte . Aqueth còr que declara classas e de las controlleurs abstrèits. Que devetz espandir
aqueras classas e controlleurs entà har foncionar l'aplicacion.
L'AppBundle qu'intègra aqueths extentions . Que poiratz compréner com espandir Sygefor3 en espiant aqueth bundle.

Que podetz egaument adaptar l'interfàcia privada de gestion en modificant los modèles AngularJS contenguts dens lo repertòri app/Resources/public/ng.
Lo module FrontBundle qu'intègra ua version publica e aleugerida de Sygefor permetent aus estagiaris de s'inscríver aus diferents estagis.
Que poiratz tanben retrobar un module Bilan basat sus ElasticSearch.
