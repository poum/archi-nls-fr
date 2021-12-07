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

## Outputs

You will now see the plug-in projects that were generated by the Ant script in the Package Explorer. Each project will have the target language code appended to its name (for example, "ru" for Russian). Each properties file that needs translating will also have the language code appended (for example, "plugin_ru.properties", "messages_ru.properties" for Russian).

There is also a "nl" folder. This may be empty for some projects. Don't worry if it is empty. If there are files and folders in the "nl" folder, these are assets that will also need to be translated. For example in the "com.archimatetool.help.xx" plug-in there are help files and hints files that will need to be translated.

## Translate the strings in the properties files

Now that you have created the target projects you need to translate all the values (the strings to the right of the equals sign ("=") in the target properties files. If you are translating to a language that uses basic ASCII characters (like English) you can edit the properties files directly. If not then you have to edit the files using a tool that saves Unicode characters. Install the translation tool as described above.

1. Select the properties file to be translated and right-click on it and select the menu item "Open With -> Language Properties Editor":

![nls-properties-editor1](https://user-images.githubusercontent.com/600504/43653035-ccd99720-973e-11e8-8074-54dc301cc219.png)

2. The file will open so you can edit the values:

![nls-properties-editor2](https://user-images.githubusercontent.com/600504/43653050-d8784ff4-973e-11e8-944d-5d58f5501879.png)

Do this for all properties files in the target projects. Remember that in order to enter non-English characters you have to using a computer that is set to the target language.

Note - you do not have to translate a string value if you wish to retain the default (English) value. In fact you can even delete the line in the target properties file. Archi will default to use the in-built English version.

## Special Characters in the properties file

Some characters should not be translated. The "&" character denotes a key shortcut for the letter that follows it. For example:

```
&Empty Model
```

This means that the "E" key will be used as the short-cut for this command in the application. The translator will have to position the "&" to where it makes sense.

{0} and {1} are placeholders for values that will be inserted at runtime. For example:

```
File ''{0}'' is already open. Its name is ''{1}''.
```

At run-time this will become:

```
File 'c:\somefile.archimate' is already open. Its name is 'My Model'.
```

The translator will have to move the {0} and {1} placeholders to where they make sense in the translated sentence. Note the double apostrophe (two ' characters). Apostrophes that surround place-holders have to be doubled in order to show up.

## Testing the translations

At any time you can test your translations by Running Archi from Eclipse. See Running and Debugging Archi for instructions. Remember to add the translated target plug-ins to the list of selected plug-ins on the "Plug-ins" tab of the Run/Debug Configuration dialog.

If you are not using a computer that has been set up to use the target language you can replace the switch -nl ${target.nl} with -nl xx in the Program Arguments on the "Arguments" tab of the Run/Debug Configuration dialog. "xx" should be replaced with the target language code (ru, fr, de, nl, etc).

## Export the plug-in projects

Once the translations are completed you need to export the projects as plug-ins.

1. From the menu select "File -> Export..." In the wizard select "Deployable plug-ins and fragments".
2. Select all the target plug-ins that end in "xx", where "xx" is the target language code (ru, fr, de, nl, etc):

![export-nls1](https://user-images.githubusercontent.com/600504/43653268-79302732-973f-11e8-9338-65c91e29e7ac.png)

3. Ensure the options on the "Options" tab are set as follows:

![export-nls2](https://user-images.githubusercontent.com/600504/43653292-849db7d8-973f-11e8-9a72-13004613f0b4.png)

4. Press Finish

The plug-ins will be exported as folders to the destination directory in a "plugins" folder:

![export-nls3](https://user-images.githubusercontent.com/600504/43653306-9044c2de-973f-11e8-9254-d118c41a94cc.png)

## Download the Eclipse language packs for the target language

By this stage you have translated the language strings that are specific to Archi. However, remember that Archi is built upon the Eclipse platform which itself consists of a number of plug-ins. These plug-ins also need translating. Luckily this work has been done for some languages in the <a href="http://www.eclipse.org/babel/">Eclipse Babel Project</a>.

Pick the language packs necessary for the Eclipse release. You will need one for the Eclipse workbench.

Unzip this somewhere. The "eclipse" folder contains two sub-folders, "features" and "plugins".

## Package everything as a target language pack and install

Combine the target language "plugins" folder that we exported earlier with the "plugins" folder from the Babel language pack. You should end up with a "features" folder and a "plugins" folder

You will need to zip them up altogether into one bundle if you wish to re-distribute them.

Finally the end user must unzip the contents of the bundle and copy or move the folders to the "features" and "plugins" folders of their Archi installation. If the target computer is set to run in the target language then Archi will launch using the target language.

# Contribuer à cette traduction

Clone this repository
Execute git tag in ${ARCHI-NLS-DIR} to check the latest Archi version applied and remember it as ${ARCHI-NLS-VERSION} say 4.2.0
Execute git tag in ${ARCHI-DIR} to check the latest Archi release code available
Select the Archi release version next to ${ARCHI-NLS-VERSION} say 4.2.1 and remember it as ${ARCHI-VERSION}
Checkout the selected Archi tag with command cd ${ARCHI-DIR} && git checkout release_${ARCHI-VERSION} && git clean -d -f
Generate Archi NLS resources in Eclipse IDE according to Archi instruction
Delete all archi-nls directories with command rm -rf ${ARCHI-NLS-DIR}/com.*
Copy generated NLS resources to ${ARCHI-NLS-DIR} with command cp -r ${ARCHI-DIR}/nls/* ${ARCHI-NLS-DIR}
Commit and tag new archi-nls version with command cd ${ARCHI-NLS-DIR} && git add . && git commit -am "${ARCHI-NLS-VERSION} -> ${ARCHI-VERSION}" && git tag ${ARCHI-VERSION}
Repeat steps 6-11 until ${ARCHI-NLS-VERSION} become the latest Archi release version.

# Sources

- https://github.com/smeagol74/archi-nls
- https://github.com/archimatetool/archi/wiki/Translating-Archi
