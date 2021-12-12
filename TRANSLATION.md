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
- Cochez tous les projets puis cliquez sur "Finish".
- On obtient finalement une arborescence de projets.

## Configurer la plateforme cible

- trouver 'com.archimatetool.editor.product/archi.target' et ouvrir le fichier avec le Eclipse Target Editor 
- dans l'éditeur, dans le coin en haut à droite, cliquer sur le lien "Set as Active Plateform". Notez que dans certains cas, ce lien contient le texte "Reload Target Plateform". Enumeration bas à droite de la fenêtre, s'affiche "Load Target Plateform" et un pourcentage pendant que Eclipse télécharge toutes les dépendances et ça peut prendre un moment. A l'issue, le lien devient "Reload Target Plateform".
 
## Lancer Archi depuis Eclipse

- Dans le Package Explorer d'Eclipse, trouvez le fichier 'product file' "com.archimatetool.editor.product/archi.product" situé juste au-dessus du fichier précédent, puis ouvrez le fichier dans le Product Configurator Editor d'Eclipse.
- Dans l'éditeur, cliquez sur le lien "Launch an Eclipse Application in Debug mode" (en bas à gauche de l'éditeur).

Note: à chaque fois que vous lancez Archi via le lien "Launch an Eclipse Application in Debug mode" du fichier archi.product, cela réinitialisera tous les paramétrages que vous aurez fait dans la configuration Debug/Run. Si vous avez ajouté manuellement d'atres greffons ou des fragments à la configuration Debug/Run, ils seront supprimés. Pour corriger ceci, une fois que vous avez lancé Archi via le fichier archi.product, modifiez et personnalisez la coniiguration Debug/Run puis exécutez-le depuis la barre d'outils Eclipse ou depuis le menu Run.

## Autres réglages

Pour simuler un zoom de 200% sur un moniteur sans Hi-DPI, utilisez le paramètre de programme -Dswt.autoScale=200 sur Windows ou configurez la variable d'environnement GDK_SCALE=2 sous Linux.

Archi's default language is British English. It is possible to run Archi in non-English languages by producing language packs. A language pack is a collection of plug-ins that contain translated *.properties files. Every string that is used in Archi has been externalised into a number of *.properties files. The aim is to produce a mirror set of all of the *.properties files with translated values and bundle these together for redistribution.

As well as translating Archi's language strings remember that Archi is built upon the Eclipse platform which itself consists of a number of plug-ins. These plug-ins also need translating. Luckily this work has been done for some languages in the <a href="http://www.eclipse.org/babel/">Eclipse Babel Project</a>.

## Traduire les fichiers de propriétés, les packages et les caractères unicode

Ce qui suit est un exemple d'une partie du fichier 'messages.properties' du package 'com.archimatetool.editor.actions' dans le greffon 'com.archimatetool.editor':

```
ArchimateEditorActionFactory_0=&Delete
ArchimateEditorActionFactory_1=Delete
ArchimateEditorActionFactory_2=Rena&me
ArchimateEditorActionFactory_3=Rename
ArchimateEditorActionFactory_4=Open &View
ArchimateEditorActionFactory_5=Close Model
ArchimateEditorActionFactory_6=Duplicate
```

Si vous regardez le code Archi dans Eclipse, vous verrez que chaque greffon contient un fichier "plugin.properties" et la plupart des packages Java qui s'y trouvent contiennet un fichier "messages.properties". Chacun de ces fichiers de propriétés doit être copié dans un nouveau greffon de langue, renommé en "plugin_xx.properties" ou "messages_xx.properties" où "xx" est le code de la langue cible, "fr" pour nous.

Chaque ligne d'un fichier de propriétés comporte une clef, un signe égal (=) et une valeur. La clef et le signe égal (=) ne doivent pas être modifiés. Seule la valeur doit être traduite.

## Caractères Unicode

Certains caractères ne peuvent être enregistrés "tels quels" dans le fichier de propriétés. Prenez la phrase "Son père est allé à l'hôtel". Elle contient quatre caractères accentués qui ne font pas partie de l'encodage latin-1. Ces caractères doivent être écrits sous forme de caractères Unicode:


```
Son p\u00e8re est all\u00e9 \u00e0 h\u00f4tel
```
Heureusement, le traducteur n'a pas à se préoccuper de ça car il existe des outils qui permettent à l'utilisateur de saisir les chaînes de caractères des valeurs dans leur langue maternelle et l'outil enregistrera les valeurs sous forme de caractères Unicode.

## Outil de traduction

Nous avons écrit un outil de ce type qui peut être utilisé directement depuis Eclipse. C'est un greffon éditeur qui vous permet de modifier les fichiers de propriétés dans la langue maternelle de l'utilisateur.

L'outil peut être téléchargé ici:

<a href="https://www.archimatetool.com/downloads/plugins/com.dadabeatnik.properties.editor_1.0.0.201202091951.jar">com.dadabeatnik.properties.editor_1.0.0.201202091951.jar</a>

Placez ce fichier jar dans le dossier "dropins" dans le répertoire d'installation d'Eclipse puis redémarrez ce dernier. Nous utiliserons cet outil ultérieurement.

## Étapes pour la traduction

Les étapes indispensables pour réaliser une traduction sont:

1. Créer des projets de greffons cibles pour les greffons Archi
2. Traduisez les chaînes de caractères des valeurs dans les fichiers de propriétés
3. Exportez les projets de greffons
4. Téléchargez les pacls de langue Eclipse correspondants à la langue cible dans le projet Babel Eclipse
5. Packagez le tout sous forme d'un pack de langue cible et installez-le

## Créez des projets de greffon cible pour tous les greffons Archi

1. Lancez Eclipse
2. Ouvrez le projet "com.archimatetools.nls" dans l'explorateur de package, trouvez le fichier "create-nls.xml" et ouvrez-le.
3. Ce fichier est un script Ant qui va créer les projets du pack de langue à partir des projets source. Vous devrez modifier certaines valeurs avant de l'exécuter:

![edit-nls-ant](https://user-images.githubusercontent.com/600504/43652873-599db250-973e-11e8-9f68-e6bbfcf1c2a5.png)

Modifiez la première valeur de "en" en "fr" (le code de langue cible).

Modifiez la seconde valeur pour lui donner la version du pack de langue que vous allez créer.

4. Enregistrer le fichier "create-nls.xml"
5. Faites un clic droit sur le fichier "create-nls.xml" dans l'explorateur de packages d'Eclipse puis choisissez "Run As -> Ant Build". Les greffons de langue seront créés mais vous ne les verrez pas dans l'explorateur de packages tant que vous ne les aurez pas importés.
6. Dans le menu principal d'Eclipse, choisissez "File -> Import...". Dans l'assistant d'import, choisissez "General -> Existing Projects into Workspace".
7. Dans l'assistant, choisissez le dossier "nls" qui a désormais été créé dans votre dossier source Archi:

![import-nls](https://user-images.githubusercontent.com/600504/43652904-6e7efae4-973e-11e8-90c9-e8569b93464b.png)

8. Appuyez sur "Finish" dans l'assistant

## Sorties

Vous verrez maintenant les projets des greffons qui ont été générés par le script Ant dans l'explorateur de paquetages. Chaque projet aura le code de langue cible ajouté à son nom (par exemple, "fr" pour French"). Chaque fichier de propriétés qui doit être traduit aura aussi ce code de langue ajouté (par exemple "plugin_fr.properties", "messages_fr.properties" pour le français).

Il y a également un dossier "nl". Il peut être vide pour certains projets. Dans ce cas, ne vous inquiétez pas. S'il il y a des fichiers et des dossiers dans ce dossier "nl", ce sont des éléments qui doivent également être traduits. Par exemple, dans le greffon "com.archimatetools.help.xx" se trouvent des fichiers d'aide et de conseil qui doivent être traduits.

## Traduire les chaînes de caractères dans les fichiers de propriétés

Maintenant que vous avez créé les projets cibles, vous devez traduire toutes les valeurs (les chaînes de caractères à la droite du fichier égal ("=") dans les fichiers de propriétés cibles. Si vous traduisez dans une langue qui utilise les caractères ASCII de base (telle que l'anglais), vous pouvez modifier les fichiers de propriétés directement. Si ce n'est pas le cas, vous devez modifier les fichiers en utilisant un outil qui enregistre les caractères Unicode. Installez l'outil de traduction comme décrit ci-dessus.

1. Choisissez le fichier de propriétés à traduire et faites un clic droit sur lui puis choisissez l'entrée de menu "Open With -> Language Properties Editor":

![nls-properties-editor1](https://user-images.githubusercontent.com/600504/43653035-ccd99720-973e-11e8-8074-54dc301cc219.png)

2. Le fichier va s'ouvrir et vous pourrez modifier les valeurs:

![nls-properties-editor2](https://user-images.githubusercontent.com/600504/43653050-d8784ff4-973e-11e8-944d-5d58f5501879.png)

Faîtes ceci pour tous les fichiers de propriétés dans les projets cibles. Rappelez-vous que pour saisir des caractères non anglais, vous devez utiliser un ordinateur qui est configuré pour cette langue cible.

Note - vous n'avez pas à traduire une valeur de chaîne de caractères si vous souhaitez conserver la valeur par défaut (en anglai). En fait, vous pouvez même supprimer la ligne dans le fichier de propriétés cible. Archi reviendra par défaut à utiliser la version anglaise embarquée.

## Caractères spéciaus dans le fichier des propriétés

Certains caractères ne doivent pas être traduits. Le caractères "&" signale un raccourci clavier pour la lettre qui vient juste après. Par exemple:

```
&Empty Model
```

Ceci signifie que la touche "E" sera utilisée comme raccourci pour cette commande dans l'application. Le traducteur devra placer le "&" à l'endroit où il fera sens.

{0] et {1} sont des emplacements pour les valeurs qui seront insérées à l'exécution. Par exemple:

```
Le fichier ''{0}'' est déjà ouvert. Son nom est ''{1}''.
```

À l'exécution, ceci deviendre:

```
Le fichier 'c:\somefile.archimate' est déjà ouvert. Son est est 'Mon modèle'.
```

Le traducteur aura à déplacer les conteneurs {0} et {1} là où ils font sens dans la phrase traduite. Notez la double apostrophe (deux caractères '). Les apostrophes qui entourent les conteneurs doivent être doublées de façon à être affichées (et seulement dans ce cas).

## Tester les traductions

À tout moment, vous pouvez tester vos traductions en exécutant Archi depuis Eclipse. Voir "Exécuter et déboguer Archi" pour les instructions. Rappelez-vous d'ajouter les greffons cibles traduits à la liste des greffons sélectionnés dans l'onglet "Plug-ins" de la fenêtre de dialogue de configuration Run/Debug.

Si vous n'utilisez pas un ordinateur qui a été configuré pour utiliser la langue cible, vous pouvez remplacer le commutateur -nl ${target.nl} avec -nl fr dans Program Arguments dans l'onglet "Arguments" dans la fenêtre de dialogue de configuration Run/Debug. 

## Exporter les projets des greffons

Une fois que les traductions sont terminées, vous devez exporter les projets en tant que greffons.

1. Dans le menu, choisissez "File -> Export...". Dans l'assistant, choisissez "Deployavle plug-ins and fragments".
2. Choisissez tous les greffons cibles qui finissent en "fr".

![export-nls1](https://user-images.githubusercontent.com/600504/43653268-79302732-973f-11e8-9338-65c91e29e7ac.png)

3. Assurez vous que les options de l'onglet "options" sont définis comme suit:

![export-nls2](https://user-images.githubusercontent.com/600504/43653292-849db7d8-973f-11e8-9a72-13004613f0b4.png)

4. Appuyez sur Finish

Les greffons seront exportés sous forme de dossier dans le répertoire de destination dans le dossier "plugins":

![export-nls3](https://user-images.githubusercontent.com/600504/43653306-9044c2de-973f-11e8-9254-d118c41a94cc.png)

## Téléchargez les paquetages de langue Eclipse pour la langue cible

A ce stade, vous avez traduit les chaînes de caractères qui sont spécifiques à Archi. Cependant, rappelez-vous qu'Archi est construit sur la plateforme Eclipse qui elle-même consiste en un certain nombre de greffons. Ces greffons doivent également être traduits. Heureusement, ce travail a été fait pour certaines langues par le <a href="http://www.eclipse.org/babel/">projet Eclipse Babel</a>.

Choisissez les paquetages de langue nécessaires pour la version d'Eclipse. Vous aurez besoin de celui du workbench Eclipse.

Décompressez ceci quelque part. Le dossier "Eclipse" contient deux sous-dossiers, "features" et "plugins".

## Empaquetez le tout sous forme d'un paquetage de langue et installez

Combinez le dossier "plugins" de la langue cible que nous avons exporté plus tôt avec le dossier "plugins" du paquetage de langue Babel. Vous devriez finir avec un dossier "features" et un dossier "plugins".

Vous aurez besoin de les compresser ensemble dans un bundle si vous souhaitez le redistribuer.

Finalement, l'utilisateur final doit désarchiver le contenu de ce bundle et copier ou déplacer les dossier dans les dossiers "features" et "plugins" de leur installation d'Archi. Si l'ordinateur cible est configuré pour s'exécuter dans la langue cible, alors Archi se lancera en utilisant la langue cible.

# Contribuer à cette traduction

Clonez ce dépôt
Exécuter git tag dans ${ARCHI-NLS-DIR} pour vérifier la dernière version Archi appliquée et mémorisez la en tant que ${ARCHI-NLS-VERSION}, disons 4.2.0
Exécutez git tag dans ${ARCHI-DIR} pour vérifier la dernière livraison de code d'Archi disponible

Choisissez la version de livraison d'Archi suivant celle de ${ARCHI-NLS-VERSION}, disons 4.2.1 et mémorisez la en tant que ${ARCHI-VERSION}
Extrayez l'étiquette Archi sélectionnée dans l'IDE Eclipse conformément aux instructions d'Archi.
Supprimez tous les répertoires NLS d'Archi avec la commande rm -rf ${ARCHI-NLS-DIR}/com.*
Copiez les ressources NLS générées dans ${ARCHI-NLS-DIR} avec la commande cp -r ${ARCHI-DIR}/nls/* ${ARCHI-NLS-DIR}
Livrez et étiquetez la nouvelle version archi-nls avec la commande cd ${ARCHI-NLS-DIR} && git add . && git commit -am "${ARCHI-NLS-VERSION} -> ${ARCHI-VERSION}" && git tag ${ARCHI-VERSION}
Répetez les étapes 6 à 11 jusqu'à ce que ${ARCHI-NLS-VERSION} devienne la dernière version de livraison d'Archi.

# Sources

- https://github.com/smeagol74/archi-nls
- https://github.com/archimatetool/archi/wiki/Translating-Archi
