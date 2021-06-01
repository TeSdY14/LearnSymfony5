# Charming Development in Symfony 5
## [Chapter 01 - Creating a new Symfony 5 Project](https://symfonycasts.com/screencast/symfony/setup)

Salut les copains ! Et bienvenue dans le monde de Symfony 5... qui se trouve être mon monde préféré ! 
Ok, peut-être que Disney World est mon monde préféré... mais la programmation dans Symfony 5 est juste après.

Symfony 5 est mince et méchant : il est rapide comme l'éclair, commence minuscule, mais grandit avec vous à mesure que votre application s'agrandit. 
Et ce n'est pas du jargon marketing ! Votre application Symfony se développera littéralement à mesure que vous aurez besoin de plus de fonctionnalités. 
Mais d'avantage là-dessus plus tard.

Symfony 5 est également le produit d'années de travail sur l'expérience des développeurs. 
Fondamentalement, les personnes derrière Symfony veulent que vous aimiez l'utiliser, mais sans sacrifier la qualité. 
Oui, vous pouvez écrire du code dont vous êtes fier, aimer le processus et créer rapidement des éléments.

Symfony est également le framework PHP majeur le plus rapide, ce qui n'est pas surprenant : - _son créateur a également créé le système de profilage PHP Blackfire_. 
Donc... la performance est toujours au centre des préoccupations.

> Go Deeper!
>
> Regardez notre [cours Blackfire.io: Révéler les secrets de performance avec profilage](https://symfonycasts.com/screencast/blackfire) pour en savoir plus sur Blackfire.

### Downloading the Symfony Installer
Alors ... faisons ça ! Commencez par aller sur [http://symfony.com](http://symfony.com) et cliquez sur 'Télécharger'. 
Ce que nous sommes sur le point de télécharger n'est pas en fait Symfony. C'est un outil exécutable qui aidera à faire du développement local avec Symfony... eh bien... génial.

Parce que je suis sur un Mac, je vais copier cette commande, puis ouvrir un terminal - _j'en ai déjà un en attente_. Peu importe où sur votre système de fichiers vous exécutez cela.
```shell
curl -sS https://get.symfony.com/cli/installer | bash
```
Cela télécharge un seul fichier exécutable et, pour moi, le place dans mon répertoire personnel. 
Pour faire en sorte que je puisse exécuter cet exécutable de n'importe où sur mon système, je vais suivre les conseils de la commande et déplacer le fichier ailleurs :
```shell
mv /Users/weaverryan/.symfony/bin/symfony /usr/local/bin/symfony
```
OK, essayons cela.
```shell
symfony
```
Il est vivant ! Dites bonjour à la CLI Symfony : un outil de ligne de commande qui nous aidera avec diverses choses sur notre chemin vers la gloire de la programmation.

### Démarrer une nouvelle application Symfony
Son premier travail sera de nous aider à créer un nouveau projet Symfony 5. Exécutez :
```shell
symfony new cauldron_overflow
```
Où _cauldron_overflow_ sera le répertoire dans lequel la nouvelle application vivra. 
Cela se trouve également être le nom du site que nous construisons... mais plus à ce sujet plus tard.

Dans les coulisses, cette commande ne fait rien de spécial : 
- Elle clone un référentiel Git appelé _symfony/skeleton_, puis utilise **Composer** pour installer les dépendances de ce projet. 
Nous parlerons plus en détail de ce référentiel et de **Composer** un peu plus tard.
Quand c'est fait, déplacez-vous dans le nouveau répertoire :
```shell
cd cauldron_overflow
```
Et puis ouvrez ce répertoire dans votre éditeur préféré. Je l'ai déjà ouvert dans mon favori : **PhpStorm**, ce que j'ai fait en allant dans 
**File** -> **Open Directory** et en **sélectionnant le nouveau dossier du projet**. 
Quoi qu'il en soit, dites bonjour à votre tout nouveau projet Symfony 5, brillant et plein de potentiel.

### Notre application est petite !
Avant de commencer à pirater les choses, créons un nouveau référentiel git et validons. Mais attendez ... exécutez :
```shell
git status 
```
> "On branch master, nothing to commit."

Surprise ! La commande `symfony new` a _déjà_ initialisé un dépôt git pour nous et effectué le premier commit. Vous pouvez le voir en exécutant :
```shell
git log
```
> "Add initial set of files"

Cool ! Cependant, j'aurais personnellement aimé un premier message de commit un peu plus épique... mais c'est bien.

Je vais frapper '`q`' pour quitter ce mode.

J'ai mentionné plus tôt que Symfony commence petit. Pour le prouver, nous pouvons voir une liste de tous les fichiers qui ont été validés en exécutant :
```shell
git show --name-only
```
Ouais ... c'est tout ! Notre projet - qui est entièrement configuré et prêt à exploiter Symfony - comprend moins de 15 fichiers... 
Si vous ne comptez pas des choses comme `.gitignore`. Maigre et méchant.
### Vérification des exigences
Connectons un serveur Web à notre application et voyons-le en action ! 
Tout d'abord, assurez-vous que votre ordinateur dispose de tout ce dont Symfony a besoin en exécutant :
```shell
symfony check:req
```
Pour vérifier les exigences.

### Démarrage du serveur Web PHP
Pour lancer réellement le projet, regardez en arrière dans PhpStorm. Nous parlerons plus en détail de chaque annuaire bientôt. 
Mais la première chose que vous devez savoir est que le répertoire public / est la 'racine du document'. 
Cela signifie que vous devez pointer votre serveur Web - comme Apache ou Nginx - vers ce répertoire. Symfony a des documents sur la façon de faire cela.

Mais ! Pour simplifier la vie, au lieu de configurer un vrai serveur sur notre machine locale, nous pouvons utiliser le serveur Web intégré de PHP. 
À la racine de votre projet, exécutez :
```shell
php -S 127.0.0.1:8000 -t public/
```
Dès que nous faisons cela, nous pouvons retourner à notre navigateur et aller à [`http://localhost:8000`](http://localhost:8000) pour trouver... Bienvenue dans Symfony 5 ! 
Ooh, Fantastique !!

Ensuite : aussi simple que cela ait été de faire fonctionner ce serveur Web PHP, je vais vous montrer une option encore meilleure pour le développement local. 
Ensuite, nous apprendrons à connaître la signification des répertoires dans notre nouvelle application et nous nous assurerons que quelques plugins sont installés dans PhpStorm... 
ce qui... fait de travailler avec Symfony **un plaisir absolu**.







