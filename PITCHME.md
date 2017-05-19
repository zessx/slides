---

![Composer](assets/images/logo-composer.png)

### Ça c'est vraiment Schubert !

---

## À quoi ça sert ?

Gérer les dépendances à des librairies PHP.

Charger toutes les classes automatiquement.

Maintenir les dépendances à jour.

---

## Exemple de projet Composer

Un projet est définit par un fichier `composer.json` :

```json
{
    "name": "schubert/symfony-11",
    "description": "Symfony #11",
    "type": "project",
    "license": "GPLv3",
    "authors": [{
        "name": "Frantz Schubert",
        "email": "bebert1797@hotmail.at"
    }],
    "require": {
        "php": ">=5.6.0",
        "diatem-net/jin": "~2.0"
    }
}
```

+++

## Le nom du projet

Le nom d'un projet Composer  
est toujours préfixé d'un namespace.  
Ce namespace est l'identifiant  
de l'utilisateur qui a créé le projet,  
et généralement aussi son identifiant GitHub :

`username/project`

Ce système permet d'éviter les conflits entre projets.

+++

## Le type de projet

Les types de base sont `library`, `project`, `metapackage` et `composer-plugin`.

Certains CMS, comme Drupal, définissent des types personnalisés, pour lesquels une procédure d'installation est prédéfinie.  
Par exemple, les packages du type `drupal-module` seront installés dans le dossier `web/modules/contrib` plutôt que dans `vendor`.

+++

## Les auteurs du projet

Il est possible et fortement recommandé  
de spécifier les auteurs du projet.  
Pour chaque auteur, on peut définir  
un certain nombre de données :

```json
{
    "name": "Frantz Schubert Adermann",
    "email": "bebert1791@hotmail.at",
    "homepage": "https://schubert.at",
    "role": "Composer"
}
```

+++

## Les dépendances du projet

La clé la plus importante du  
fichier `composer.json` est la clé `require`.

Elle définit les librairies PHP dont a besoin votre projet.

Il est possible d'utiliser une seconde clé `require-dev`,  
pour les librairies nécessaires aux tests par exemple.

--- 

## Gérer votre projet avec Composer

Avec un nouveau projet, il faut créer le fichier `composer.json`.

Vous pouvez le faire à la main, ou directement avec la commande suivante :

```bash
composer init
```

+++

## Installer les dépendances

L'initialisation de Composer ne crée  
que le fichier `composer.json`.

Pour installer les dépendances,  
il faudra utiliser la commande install :

```bash
composer install --no-dev
```

Par défaut, Composer installe les dépendances de  
développement. Il faut donc préciser `--no-dev`  
si vous n'en avez pas besoin.

+++

## Ajouter une dépendance

L'ajout d'une nouvelle dépendance se fait via la commande require

```bash
composer require diatem-net/jin:^2.0
```

Si aucune contrainte de version n'est spécifiée, Composer choisira la plus récente.  
La librairie est immédiatement installée.

+++

## Mettre à jour une dépendance

La mise à jour se fait simplement  
via la commande update.  
Elle respectera la restriction de version  
que vous avez définie.

```bash
composer update diatem-net/jin
```

Pour tout mettre à jour, lancer simplement :

```bash
composer update
```

---

## Autoload

Une fois vos dépendances installées, il ne vous reste plus qu'à charger les classes PHP dans votre projet. Composer s'occupe de tout et vous a déjà créé un fichier `autoload.php` !

```php
require __DIR__ . '/vendor/autoload.php';

use Jin2\Log\Debug;

Debug::dump('Hello world !');
```

+++

## Et pour vos classes ?

Composer vous donne la possibilité de charger votre propre code via son autoloader.

Pour cela, précisez l'emplacement du code et son namespace dans le `composer.json` :

```json
{
    "autoload": {
        "psr-4": {
            "Symfony10\\": "app/src/"
        }
    }
}
```

--- 

## Les versions

Composer n'est pas un système de versioning de code, ce n'est donc pas lui qui va gérer les versions, mais votre VCS (Git, Mercurial).

Tous les tags et toutes les branches que vous allez crééer seront accessibles via Composer :
- `2.0` (tag `2.0`)
- `dev-develop` (branche `develop`)
- `v2.x-dev` (branche `v2`)

**Important : Composer utilise des versions `x.y.z`**

+++ 

## Les contraintes de versions

Plus que des versions, vous allez surtout utiliser des contraintes de version pour définir ce dont a besoin votre projet :
- `1.0.2` : version exacte
- `>=1.0 <1.6` : plage de versions
- `1.0 - 1.5` : identique à `>=1.0 <1.6`
- `1.0.*` : identique à `>=1.0.0 <1.1.0`
- `~1.0.2` : identique à `>=1.0.2 <1.1.0`
- `^1.0.2` : identique à `>=1.0.2 <2.0.0`

+++ 

## Zoom sur l'opérateur `~`

L'opérateur `~` permet d'accepter toutes les versions jusqu'à la prochaine version non significative :
- `~1.2` : identique à `>=1.2 <2.0.0`
- `~1.2.3` : identique à `>=1.2.3 <1.3.0`
- `~0.3` : identique à `>=0.3.0 <1.0.0`

+++

## Zoom sur l'opérateur `^`

L'opérateur `^` permet d'accepter toutes les versions jusqu'à la prochaine version majeure :
- `^1.2` : identique à `>=1.2 <2.0.0`
- `^1.2.3` : identique à `>=1.2.3 <2.0.0`
- `^0.3` : identique à `>=0.3.0 <0.4.0`

---

## Quelques commandes à connaître

Pour installer une dépendance sans tenir compte des prérequis de plateforme :

```bash
composer require <library> --ignore-platform-reqs
```

Pour vider le cache de composer :

```bash
composer clear-cache
```

Pour ne pas (re)générer l'autoloader :

```bash
composer require <library> --no-autoloader
```

+++

## Quelques commandes à connaître

Pour supprimer une dépendance :

```bash
composer remove <library>
```

Pour rechercher une dépendance :

```bash
composer search <library>
```

Pour afficher les dépendances :

```bash
composer show
```

+++

## Quelques commandes à connaître

Pour afficher les dépendances dépassées :

```bash
composer outdated
```

Pour vérifier votre fichier `composer.json` :

```bash
composer validate
```

Pour mettre Composer à jour :

```bash
composer self-update
```

---

## Ressources utiles

Documentation : <a href="https://getcomposer.org/doc/" target="_blank">getcomposer.org/doc</a>

Dépôt principal de Composer : <a href="https://packagist.org/" target="_blank">packagist.org</a>

---

cimer.

<a href="https://twitter.com/zessx" target="_blank">@zessx</a>