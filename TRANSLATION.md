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

## Cpnfigurer la plateforme cible

- trouver 'com.archimatetool.editor.product/archi.target' et ouvrir le fichier avec le Eclipse Target Editor 
- dans l'éditeur, dans le coin en haut à droite, cliquer sur le lien "Set as Active Plateform". Notez que dans certains cas, ce lien contient le texte "Reload Target Plateform". Enumeration bas à droite de la fenêtre, s'affiche "Load Target Plateform" et un pourcentage pendant que Eclipse télécharge toutes les dépendances et ça peut prendre un moment. A l'issue, le lien devient "Reload Target Plateform".
 
# Lancer Archi depuis Eclipse

- Dans le Package Explorer d'Eclipse, trouvez le fichier 'product file' "com.archimatetool.editor.product/archi.product" situé juste au-dessus du fichier précédent, puis ouvrez le fichier dans le Product Configurator Editor d'Eclipse.
- Dans l'éditeur, cliquez sur le lien "Launch an Eclipse Application in Debug mode" (en bas à gauche de l'éditeur).

Note: à chaque fois que vous lancez Archi via le lien "Launch an Eclipse Application in Debug mode" du fichier archi.product, cela réinitialisera tous les paramétrages que vous aurez fait dans la configuration Debug/Run. Si vous avez ajouté manuellement d'atres greffons ou des fragments à la configuration Debug/Run, ils seront supprimés. Pour corriger ceci, une fois que vous avez lancé Archi via le fichier archi.product, modifiez et personnalisez la coniiguration Debug/Run puis exécutez-le depuis la barre d'outils Eclipse ou depuis le menu Run.

## Autres réglages

Pour simuler un zoom de 200% sur un moniteur sans Hi-DPI, utilisez le paramètre de programme -Dswt.autoScale=200 sur Windows ou configurez la variable d'environnement GDK_SCALE=2 sous Linux.

##

> Please note that these instructions may now be out of date or incorrect. Please feel free to update any errors.

> 14 February 2018 - Konstantin Borisov has created a Git repository that contains the English language pack that you may find easier to work with. For more information see https://github.com/smeagol74/archi-nls

## Pre-requisites

In order to make Archi Language Packs you need to install Eclipse and the Archi code. Please read the following sections before proceeding:

* [[Setting up the Eclipse Environment|Setting-up-the-Eclipse-Environment]]
* [[Importing the Code|Importing-the-Code]]
* [[Running and Debugging Archi|Running-and-Debugging-Archi]]

## Background

Archi's default language is British English. It is possible to run Archi in non-English languages by producing language packs. A language pack is a collection of plug-ins that contain translated *.properties files. Every string that is used in Archi has been externalised into a number of *.properties files. The aim is to produce a mirror set of all of the *.properties files with translated values and bundle these together for redistribution.

As well as translating Archi's language strings remember that Archi is built upon the Eclipse platform which itself consists of a number of plug-ins. These plug-ins also need translating. Luckily this work has been done for some languages in the <a href="http://www.eclipse.org/babel/">Eclipse Babel Project</a>.

## Translating Properties Files, Packages and Unicode Characters

The following is an example of part of a `messages.properties` file taken from the `com.archimatetool.editor.actions` package in the `com.archimatetool.editor` plug-in:

```
ArchimateEditorActionFactory_0=&Delete
ArchimateEditorActionFactory_1=Delete
ArchimateEditorActionFactory_2=Rena&me
ArchimateEditorActionFactory_3=Rename
ArchimateEditorActionFactory_4=Open &View
ArchimateEditorActionFactory_5=Close Model
ArchimateEditorActionFactory_6=Duplicate
```

If you look at the Archi code in Eclipse you will see that each plug-in contains a "plugin.properties" file and most Java packages within the plug-in contain one "messages.properties" file. Each of these properties files need to be copied to a new language plug-in, renamed to "plugin_xx.properties" and "messages_xx.properties" where "xx" is the target language code, and the values translated into the target language.

Each line in a properties file consists of a key, an equals sign (=), and a value. The key and equals sign (=) must not be changed. It is only the value that must be translated.

## Unicode characters

Some characters cannot be saved "as is" to the properties file. Consider the French phrase "Son père est allé à l'hôtel". This contains four accented characters that are not part of the Latin-1 codepage. These characters have to be written as Unicode characters:

```
Son p\u00e8re est all\u00e9 \u00e0 h\u00f4tel
```

This is the case for all the characters in languages such as Russian and Bulgarian. For example, the following is an example taken from the Russian Eclipse Babel language pack:

```
NewEditorAction_text=\u0421\u043e\u0437\u0434\u0430\u0442\u044c &\u0440\u0435\u0434\u0430\u043a\u0442\u043e\u0440
NewEditorAction_tooltip=\u0421\u043e\u0437\u0434\u0430\u0442\u044c \u0440\u0435\u0434\u0430\u043a\u0442\u043e\u0440
SaveAction_text=\u0421\u043e\u0445\u0440\u0430\u043d\u0438\u0442\u044c@Ctrl+S
SaveAction_toolTip=\u0421\u043e\u0445\u0440\u0430\u043d\u0438\u0442\u044c
SaveAs_text=\u0421\u043e\u0445\u0440\u0430\u043d\u0438\u0442\u044c &\u043a\u0430\u043a...
SaveAs_toolTip=\u0421\u043e\u0445\u0440\u0430\u043d\u0438\u0442\u044c \u043a\u0430\u043a
SaveAll_text=\u0421\u043e&\u0445\u0440\u0430\u043d\u0438\u0442\u044c \u0432\u0441\u0435
SaveAll_toolTip=\u0421\u043e\u0445\u0440\u0430\u043d\u0438\u0442\u044c \u0432\u0441\u0435
```
Fortunately, the Russian translator does not have to worry about this, as there are tools that allow the user to type the string values in the native language and the tool will save the values as Unicode characters.

## Translation Tool
We have written such a tool that can be used within Eclipse itself. It is an editor plug-in that allows you to edit the properties files in the user's native language.

The tool can be downloaded here:

<a href="https://www.archimatetool.com/downloads/plugins/com.dadabeatnik.properties.editor_1.0.0.201202091951.jar">com.dadabeatnik.properties.editor_1.0.0.201202091951.jar</a>

Place this jar file in the "dropins" folder of your Eclipse installation and restart Eclipse. We will use this tool later.

## Steps for Translation

The necessary steps for translation are:

1. Create target plug-in projects for the Archi plug-ins
2. Translate the strings in the properties files
3. Export the plug-in projects
4. Download the Eclipse language packs for the target language from the Eclipse Babel Project
5. Package everything as a target language pack and install

## Create target plug-in projects for the Archi plug-ins

1. Launch Eclipse
2. Open the "com.archimatetool.nls" project in the Package Explorer and find the "create-nls.xml" file and open it.
3. This file is an Ant script that will create the language pack projects from source projects. You will need to edit some values before you run it:

![edit-nls-ant](https://user-images.githubusercontent.com/600504/43652873-599db250-973e-11e8-9f68-e6bbfcf1c2a5.png)

Change the first value from "en" to the language code of the target language (for example, "ru" for Russian, "de" for German).

Change the second value to the version of the language pack you are creating.

4. Save the file "create-nls.xml"
5. Right-click on the file "create-nls.xml" in the Package Explorer in Eclipse and select "Run As -> Ant Build". The language plug-ins will be created but you won't see them yet in the Package Explorer until you import them.
6. From the main Eclipse menu select "File -> Import...". In the Import wizard select "General -> Existing Projects into Workspace".
7. In the wizard select the "nls" folder that has now been created in your Archi source folder:

![import-nls](https://user-images.githubusercontent.com/600504/43652904-6e7efae4-973e-11e8-90c9-e8569b93464b.png)

8. Press "Finish" in the wizard

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
