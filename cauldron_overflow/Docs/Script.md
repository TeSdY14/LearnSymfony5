# Charming Development in Symfony 5
## [Chapter 03 Route, Controllers & Responses!](https://symfonycasts.com/screencast/symfony/route-controller)

La page que nous regardons en ce moment... ce qui est super amusant... et elle change même de couleur ... est juste là pour dire 'Bonjour !'. 
Symfony le rend car, en réalité, notre application n'a pas encore de vraies pages. Changeons cela.

### Route + Controller = Page
Chaque framework Web... dans n'importe quelle langue... a le même objectif principal : offrir un système de **Routing** et de **Controller** : un système en 2 étapes pour créer des pages. 
Une route définit l'URL de la page et le contrôleur est l'endroit où nous écrivons le code PHP pour construire cette page, comme le **HTML** ou **JSON**.

Ouvrez `config/routes.yaml`:
```yaml
##config/routes.yaml
#index:
#    path: /
#    controller: App\Controller\DefaultController::index
```
Hey ! Nous avons déjà un exemple ! Ne commentez pas cela. 
Si vous n'êtes pas familier avec YAML, c'est super convivial : c'est un format de configuration clé-valeur qui est séparé par des deux-points. L'indentation est également importante.

Cela crée une seule route dont l'URL est `/`. Le contrôleur pointe vers une fonction qui construira cette page... vraiment, il pointe vers une méthode sur une classe. 
Dans l'ensemble, cet itinéraire dit :
- Lorsque l'utilisateur accède à la page d'accueil, veuillez exécuter la méthode d'index sur la classe **`DefaultController`**.

Oh, et vous pouvez ignorer cette clé d'index en haut du YAML : c'est un nom interne pour l'itinéraire... et ce n'est pas encore important.

### Notre appli
Le projet que nous construisons s'appelle 'Cauldron Overflow'. Nous voulions à l'origine créer un site où les développeurs pourraient poser des questions et d'autres développeurs y ont répondu, mais ... quelqu'un nous a battus ... par ... 10 ans environ. Donc, comme toutes les startups impressionnantes, nous pivotons! Nous avons remarqué que beaucoup de sorciers se faisaient exploser accidentellement ... ou conjuraient des dragons cracheurs de feu alors qu'ils voulaient créer un petit feu pour faire griller des guimauves. Et donc ... Cauldron Overflow est là pour devenir le lieu où les sorcières et les sorciers peuvent poser des questions sur les mésaventures magiques et y répondre.