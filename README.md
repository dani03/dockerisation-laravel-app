# dockerisation-laravel-app
dockeriser une app laravel 

pour lancer le projet cloner le projet avec un la commande `git clone`
lorsque le projet est telechargé, entrez dans le dossier contenant le projet et lancer la commande `docker-compose up -d`
lorsque l'execution est terminée lancer le commande `docker ps` afin de voir les containers qui sont lancés.. vous verrez 4 containers en cours d'execution
le container nginx, mysql, phpmyadmin, et dockersation-laravel-app.

## phpmyadmin
dans votre navigateur allez sur le port `localhost:1183` c'est le port que nous avons ouvert pour utilisez phpmyadmin. 
l'interface de phpmyadmin s'affiche renseigner l'utilisateur `homestead` et le mot de passe `secret`
vous permettant de vous connectez et ensuite manuellement créer une base de données nommée `homestead`

## instalation des dependences
tapez la commande `docker-compose run --rm composer install` afin d'installer les  differentes dependances et de shut down le container juste avec car nous
n'en avons pas besoin.

## fichier d'environement

ouvrez le projet dans un editer de code (vs code, phpstorm etc...) allez dans le dossier `src/`et créer un fichier `.env` et ajouter y le code suivant 

``` 
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"

```
cette partie vous permet de spécifier les informations de la base de données car par securité laravel ne pousse pas les informations confidentielles
sur le hub.
NB: sur la ligne `DB_HOST=mysql` mysql ici est le nom du service (container) de mysql definie dans mon fichier docker-compose.yml enregister et revenez sur le terminal.

lancer la commande `docker-compose run --rm artisan migrate` cette commande permettra de migrer toute les tables vers votre base de données. 
lancer ensuite la commande `docker-compose run --rm artisan key:generate`qui va permettre de definir une clé unique a notre application 

## npm 
ensuite nous allons installer les dependances frontend en lancant la commande `docker-compose run --rm npm install` npm ici est le nom du container qui
defini un entrypoint `npm` ce qui nous permet facilement de faire un npm install

et pour finir lancer la commande `docker-compose run -d --rm npm run dev`afin de compliler tout ca.. et vous pouez acceder au site sur le `port 8000`.

et voila le projet est fonctionnel vous pouvez vous enregistrez et créer des chirp mdrr.

