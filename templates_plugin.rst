==================
Templates Plugin
==================

------------------
Overview
------------------
The Templates plugin is a feature similar to `gradle-templates <https://launchpad.net/gradle-templates>`_ that can generate default directory structures and/or classes. As of GradleFx v0.5 this plugin has only very partially been implemented. Actually only the automatic generation of directory structure and the main application file (+ the descriptor file for AIR projects) is currently available, as it is a dependency required by the :doc:`ide_plugin`. Further development is not on our priority list for the time being.

Load the plugin like so: ::

    apply plugin: 'templates'

----------------
Sub-plugins
----------------
As of GradleFx v0.5 only one sub-plugin exists:

* Scaffold plugin: generates directory structure and main application class

This means that at the moment `apply plugin: 'templates'` and `apply plugin: 'scaffold'` will both result in the same tasks being available.

--------------------
Scaffold plugin
--------------------
Load the plugin: ::

    apply plugin: 'scaffold'

The ``scaffold`` task is now available to you. It is the only available task for now. To use it execute ``gradle scaffold`` at the command line.

With all conventions this will result in the following output for a ``swf`` project: ::

    $ gradle scaffold
    :my-first-app:scaffold
    Creating directory structure
            src/main/actionscript
            src/main/resources
            src/test/actionscript
            src/test/resources
    Creating main class
            src/main/actionscript/Main.mxml

    BUILD SUCCESSFUL

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Application descriptor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In an ``air`` or ``mobile`` project an application descriptor file will also be created: ::

    src/main/actionscript/Main-app.xml

^^^^^^^^^^^^^^^^
Localization
^^^^^^^^^^^^^^^^

If you've defined some locales in your build script (say ``locales = ['nl_BE', 'fr_BE']``), directories for these locales will also be created: ::

    src/main/locale/nl_BE
    src/main/locale/fr_BE