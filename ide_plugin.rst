=======================
IDE Plugin
=======================
This feature mimics the behavior of the 'eclipse', 'idea', etc. Gradle plugins for Flex projects. It generates IDE configuration files and puts the dependencies from the Gradle/Maven cache on the IDE's build path. It consists of subplugins for both FlashBuilder and Intellij which can be applied separately.

If you want support for all supported IDE's load the plugin like this: ::

    apply plugin: 'ide'

In any other case just apply the required subplugins.

--------------
Sub-plugins
--------------
There is a plugin for each of the following IDE's; each plugin has its matching task:

IDE	load plugin	execute task

+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| IDE                         | Load plugin                                        | Execute task                                                  |
+=============================+====================================================+===============================================================+
| FlashBuilder                | apply plugin: 'flashbuilder'                       | gradle flashbuilder                                           |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| IntelliJ IDEA               | apply plugin: 'ideafx'                             | gradle idea                                                   |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+


The IDEA plugin was named ``ideafx`` to avoid conflicts with the existing 'java' ``idea`` plugin.

Every IDE plugin depends on the Scaffold plugin (cf. :doc:`templates_plugin`) that generates the directory structure and the main application file.

Each of these plugins also has a matching **clean** task; for instance you could remove all the FlashBuilder configuration files from a project by executing ``gradle flashbuilderClean``.

---------------------
FlashBuilder plugin
---------------------
Load the plugin: ::

    apply plugin: 'flashbuilder'

Run the associated task: ::

    gradle flashbuilder

With all conventions the output for a ``swf`` application might be something like this: ::

    :my-first-app:scaffold
    Creating directory structure
        src/main/actionscript
        src/main/resources
        src/test/actionscript
        src/test/resources
    Creating main class
        src/main/actionscript/Main.mxml
    ::my-first-app:flashbuilder
    Verifying project properties compatibility with FlashBuilder
        OK
    Creating FlashBuilder project files
        .project
        .actionScriptProperties
        .flexProperties

    BUILD SUCCESSFULL

To clean the project, i.e. remove all FlashBuilder configuration files: ::

    gradle flashbuilderClean
	
---------------------
IDEA Intellij plugin
---------------------
Load the plugin: ::

    apply plugin: 'ideafx'

Run the associated task: ::

    gradle idea

With all conventions the output for a ``swf`` application might be something like this: ::

	:my-first-app:scaffold
	Creating directory structure
			src/main/actionscript
			src/main/resources
			src/test/actionscript
			src/test/resources
	Creating main class
			src/main/actionscript/Main.mxml
	:my-first-app:idea
	Verifying project properties compatibility with IntelliJ IDEA
	Creating IntelliJ IDEA project files

	BUILD SUCCESSFUL

To clean the project, i.e. remove all IDEA configuration files: ::

    gradle ideaClean