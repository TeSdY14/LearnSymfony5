# Charming Development in Symfony 5
## [Chapter 02 Meet our Tiny App + PhpStorm Setup](https://symfonycasts.com/screencast/symfony/dirs-server)

L'un de mes principaux objectifs dans ces didacticiels sera de vous aider à vraiment comprendre comment Symfony - comment votre application - fonctionne.

Pour commencer, jetons un coup d'œil à la structure des répertoires.

### Le répertoire `public/`
Il n'y a que trois répertoires auxquels vous devez penser. Tout d'abord, `public/` est la racine du projet : 
Il contiendra donc tous les fichiers qui doivent être accessibles par un navigateur. Et ... il n'y en a qu'un pour le moment : `index.php`:

```php
<?php
// public/index.php
use App\Kernel;
use Symfony\Component\ErrorHandler\Debug;
use Symfony\Component\HttpFoundation\Request;
require dirname(__DIR__).'/config/bootstrap.php';
if ($_SERVER['APP_DEBUG']) {
    umask(0000);
    Debug::enable();
}
if ($trustedProxies = $_SERVER['TRUSTED_PROXIES'] ?? $_ENV['TRUSTED_PROXIES'] ?? false) {
    Request::setTrustedProxies(explode(',', $trustedProxies), Request::HEADER_X_FORWARDED_ALL ^ Request::HEADER_X_FORWARDED_HOST);
}
if ($trustedHosts = $_SERVER['TRUSTED_HOSTS'] ?? $_ENV['TRUSTED_HOSTS'] ?? false) {
    Request::setTrustedHosts([$trustedHosts]);
}
$kernel = new Kernel($_SERVER['APP_ENV'], (bool) $_SERVER['APP_DEBUG']);
$request = Request::createFromGlobals();
$response = $kernel->handle($request);
$response->send();
$kernel->terminate($request, $response);
```

On l'appelle le "contrôleur frontal" : un mot sophistiqué que les programmeurs ont inventé pour signifier que c'est le fichier qui est exécuté par votre serveur Web.

Mais, vraiment, à part mettre des fichiers CSS ou image dans `public/`, vous n'aurez presque jamais besoin d'y penser.

### `src/` et `config/`
Alors... j'ai un peu menti. Il n'y a vraiment que deux répertoires auxquels vous devez penser : `config/` et `src/`. `config/` détient... euh... chiots ? 
Non, `config/` **contient les fichiers de configuration** et `src/` **est l'endroit où tout votre code PHP ira**. C'est aussi simple que cela !

Où est Symfony ? Notre projet a commencé avec un `composer.json` :
```json
{
    "type": "project",
    "license": "proprietary",
    "require": {
        "php": "^7.2.5",
        "ext-ctype": "*",
        "ext-iconv": "*",
        "symfony/console": "5.0.*",
        "symfony/dotenv": "5.0.*",
        "symfony/flex": "^1.3.1",
        "symfony/framework-bundle": "5.0.*",
        "symfony/yaml": "5.0.*"
    },
    "require-dev": {
    },
    "config": {
        "preferred-install": {
            "*": "dist"
        },
        "sort-packages": true,
        "platform": {
            "php": "7.2.5"
        }
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    },
    "autoload-dev": {
        "psr-4": {
            "App\\Tests\\": "tests/"
        }
    },
    "replace": {
        "paragonie/random_compat": "2.*",
        "symfony/polyfill-ctype": "*",
        "symfony/polyfill-iconv": "*",
        "symfony/polyfill-php72": "*",
        "symfony/polyfill-php71": "*",
        "symfony/polyfill-php70": "*",
        "symfony/polyfill-php56": "*"
    },
    "scripts": {
        "auto-scripts": {
            "cache:clear": "symfony-cmd",
            "assets:install %PUBLIC_DIR%": "symfony-cmd"
        },
        "post-install-cmd": [
            "@auto-scripts"
        ],
        "post-update-cmd": [
            "@auto-scripts"
        ]
    },
    "conflict": {
        "symfony/symfony": "*"
    },
    "extra": {
        "symfony": {
            "allow-contrib": false,
            "require": "5.0.*"
        }
    }
}
```
`composer.json` Est le fichier qui répertorie toutes les bibliothèques tierces dont notre application a besoin. 
Dans les coulisses, cette nouvelle commande de symfony a utilisé **composer** pour les installer... 
Ce qui est une façon élégante de dire que **Composer** a téléchargé un tas de bibliothèques dans le répertoire `vendor/`... y compris Symfony lui-même.

Nous parlerons plus en détail des autres fichiers et répertoires en cours de route... mais ils ne sont pas encore importants.

### Utilisation du serveur Web local Symfony
Il y a quelques minutes, nous avons utilisé PHP lui-même pour démarrer un serveur Web local. 
Mais appuyez sur `Ctrl+C` pour quitter cela. 
Pourquoi ? 
Parce que l'outil binaire symfony pratique que nous avons installé est livré avec un serveur local plus puissant. Exécutez :
```shell
symfony serve 
```
C'est ça. La première fois que vous exécutez ceci, il peut vous demander d'installer un certificat. C'est facultatif. 
Si vous l'installez - _je l'ai fait_ - il démarrera le serveur Web avec **https**. Oui, _vous obtenez https localement avec zéro config_.

Une fois qu'il est en cours d'exécution, accédez à votre navigateur et actualisez-le. Ça marche ! Et la petite icône de verrouillage prouve que nous utilisons maintenant `https`.

Pour arrêter le serveur Web, appuyez simplement sur `Ctrl+C`. Vous pouvez voir toutes les options de cette commande en exécutant :  
```shell
symfony serve --help
```
Comme les solutions afin de contrôler le numéro de port. Lorsque j'utilise cette commande, j'exécute généralement :
```shell
symfony serve -d
```
Le `-d` signifie s'exécuter en tant que "daemon" (détaché / arrière-plan). 
Il fait exactement la même chose sauf que maintenant il fonctionne en arrière-plan... ce qui signifie que je peux toujours utiliser ce terminal.
```shell
symfony server:status
```
Me montre que le serveur est en cours d'exécution et :
```shell
symfony server:stop
```
Va l'arrêter. 

Recommençons : 
```shell
symfony serve -d
```

### Installer les plugins PhpStorm
Ok : nous sommes sur le point de commencer à coder beaucoup... donc je veux m'assurer que votre éditeur est prêt à fonctionner. 
Et, oui, vous pouvez utiliser l'éditeur de votre choix. Mais je recommande vivement **PhpStorm** ! 
Sérieusement, cela fait du développement avec Symfony un rêve ! 
Et non, les gens de PhpStorm ne me paient pas pour dire ça... mais... ils sponsorisent en fait plusieurs développeurs PHP open source... ce qui est un peu mieux.

Pour vraiment rendre **PhpStorm** génial, vous devez faire deux choses. 
Tout d'abord, ouvrez les *Préférences**, sélectionnez '**Plugins**' et cliquez sur '**Marketplace**'. Recherchez « **Symfony** ».

Ce plugin est incroyable... prouvé par près de 4 millions de téléchargements. Cela nous donnera toutes sortes d'auto-complétion et d'intelligence supplémentaire pour Symfony. 
Si vous ne l'avez pas déjà, **installez-le**. Vous devez également installer les plugins '**Annotations PHP**' et '**Toolbox PHP**'. 
Si vous recherchez '**php toolbox**' ... vous pouvez les voir tous les trois. 
**Installez-les** et **redémarrez PhpStorm**.

Une fois que vous avez redémarré, retournez dans **Préférences** et recherchez "**Symfony**". 
En plus d'installer le plugin, vous devez également l'activer projet par projet. 
Cochez **Activer** puis Validez. _Cela dit que vous devez redémarrer PhpStorm ... mais je ne pense pas que ce soit vrai_.

La deuxième chose que vous devez faire dans PhpStorm est de rechercher **Composer** et de trouver la section '**Langages et Frameworks**', '**PHP**', '**Composer**'. 
Assurez-vous que la case '**_Synchroniser les paramètres IDE avec composer.json_' est cochée** ... ce qui configure automatiquement plusieurs choses utiles.

Appuyez sur 'Ok' et... nous sommes prêts ! Créons notre toute première page et voyons en quoi consiste Symfony.
