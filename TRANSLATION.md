# Translating

This little guide for those willing helping translating Archi in French.

# Préparer son environnement

Première chose à faire: installer Eclipse. Archi est construit à partir de Eclipse Rich Client Platform (RCP) et est développé en utilisant l'environnement de développement intégré Eclipse (Eclipse IDE).

## JDK 11

Vous aurez besoin au préalable d'installer un kit de développement Java (JDK) version 11, celui de votre distribution Linux ou [Temurin](https://adoptium.net/?variant=openjdk11&jvmVariant=hotspot).

Pour vérifier que tout va bien:

```
$ java -version
openjdk version "11.0.12" 2021-07-20
OpenJDK Runtime Environment (build 11.0.12+7-post-Debian-2)
OpenJDK 64-Bit Server VM (build 11.0.12+7-post-Debian-2, mixed mode, sharing)
```

## IDE Eclipse

Installez [Eclipse for RCP and RAP developpers](https://www.eclipse.org/downloads/packages/release/2021-09/r/eclipse-ide-rcp-and-rap-developers).

- désarchivez l'archive récupérée
- lancez Eclipse
- sélectionnez l'emplacement du Workplace
- faites disparaître l'écran de bienvenue
- allez dans le menu Windows->Preferences
- dans la section `java`, sélectionnez le jdk11

## Ajouter des greffons

Vous pouvez ajouter des greffons et notamment l'intégration de git.
- menu Help -> install New Software ... pour invoquer l'assistant
- Dans la combo "Work with", sélectionner '2019-09 - 2019-09 - http://download.eclipse.org/releases/2019-09
- Attendre que la liste se remplisse (ça peut direr)
- Dans la liste sous "Collaboration", choisir "Git integration for Eclipse"
- Cliquer sur "Next" et accepter les termes de licence pour terminer l'assistant
- Laisser Eclipse redémarrer

## Importer le code

- Menu "File -> Import ..."
- Dans l'assistant, sélectionner "Git -> Projects from Git" et cliquer sur "Next"
- Selectionner "Clone URI" puis cliquez sur "Next"
- Saisir les informations du dépôt:
  - URI: https://github.com/archimatetool/archi.git
  - Host: github.com
  - Repository Path: /archimatetool/archi.git
- Cliquer sur "Next"
- Cocher la branche "master" et décochez toutes les autres puis cliquez sur "Next"
- Choisissez le répertoire de destination du code ('~/Dev/archì' par exemple) et cliquez sur "Next"
- Patientez ...
- Cliquez sur "Import existing Eclipse projets" puis sur "Next"
- Cochez tous les projets **sauf** archi et archi/tests (ce sont des répertoires et pas des projets) puis cliquez sur "Finish"
- On obtient finalement une arborescence de projets dont certains ont une croix rouge, problème que nous allons régler ensuite.


