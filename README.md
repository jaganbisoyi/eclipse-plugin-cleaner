Eclipse Plugin Cleaner [![Build Status](https://travis-ci.org/azachar/eclipse-plugin-cleaner.png)](https://travis-ci.org/azachar/eclipse-plugin-cleaner)
======================

Helps to clean up your Eclipse installation from duplicated plugins and features. The duplicated plugins and features are move into a separate folder.
So you can decide later whether to delete them.

To find duplicated bundles this program checks manifests or filenames. The newest version is preserved.
By default the cleaner tries to removes duplicates from the dropins (sub)folder. 

Usage
=====

1. Install a brand new Eclipse into your new location, for example ``eclipse-new``
2. Copy into the folder ``eclipse-new/dropins``  your old Eclipse installation, 
   e.g. copy ``ecipse-old/plugins`` and ``eclipse-old/features`` into ``eclipse-new/dropins/eclipse``,
   so you will have the following file structure:
 ```
    |-- eclipse-new
    |   |-- features (new)
    |   |-- plugins (new)
    |   |-- dropins
    |       |-- eclipse
    |           |-- features (old)
    |           |-- plugins (old)
 ``` 

3. Build ``eclipse-plugin-cleaner`` or download from https://github.com/azachar/eclipse-plugin-cleaner/releases compiled jar with Java 7.
4. Copy ``plugin-cleaner-x.x.x-jar-with-dependencies.jar`` into the folder ``eclipse-new`` and execute this command
 ```
  java -jar plugin-cleaner-x.x.x.-jar-with-dependencies.jar
 ```
 * You can specify the option ``-test`` to run the dry mode that simulates changes without any modifications!
 * For more options please use the option ``-help``
 * **Duplicates are moved into the folder ``<source-folder>\duplicates_<timestamp>``**, e.g. in ``eclipse-new\duplicates_<timestamp>``
5. Run your new Eclipse
6. Delete ``eclipse-new\duplicates_<timestamp>`` if everything works.
7. Now you have the brand new installation of Eclipse with your custom plugins!

Known Limitations
=================

The bundle duplications resolving is based on a fast version duplication analysis.

In the Eclipse (and in any other OSGI enabled) application you can have a bundle that depends on multiple versions of a different bundle.
Typically Eclipse doesn't contains multiple versions of the same bundle, but if your installation contains such a setup than additional actions are required.

After you do the clean up by this tool go to Eclipse, choose ``Window -> Show View -> Error Log`` 
and check if there is any missing required bundle since you have done the clean up. If so simply move missing required features and bundles from the duplicated folder back to your ``eclipse-new/features`` and/or ``eclipse-new/plugins`` or ``eclipse-new/dropins`` folders.


Contribution
============ 
 To provide any improvement or fix please fork the ``master`` branch of this repository via GitHub and then clone your repo by the following command
  ``
    git clone -b master https://github.com/<your-username>/eclipse-plugin-cleaner.git
  ``
 * create your modifications including **tests**
 * document all public interfaces and public + protected methods. 
 * format the source code with the built-in Eclipse formatter that has the line width set to 120 characters
 * organize imports
 * push it back via a pull request in GitHub