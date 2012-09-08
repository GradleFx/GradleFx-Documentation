==========
Tasks
==========

-------------
Overview
-------------
The GradleFx plugin adds the following tasks to your project:

+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| Task name                   | Depends on                                         | Description                                                   |
+=============================+====================================================+===============================================================+
| clean                       | n/a                                                | Deletes the build directory                                   |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| compile                     | copyresources                                      | Creates a swc or swf file from your code. The 'type' property |
|                             |                                                    | defines the type of file                                      |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| package                     | compile                                            | Packages the generated swf file into an .air package          |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| copyresources               | n/a                                                | Copies the resources from the source 'resources' directory    |
|                             |                                                    | to the build directory                                        |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| publish                     | n/a                                                | Copies the files from the build directory to the publish      |
|                             |                                                    | directory.                                                    |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| createHtmlWrapper           | n/a                                                | Creates an HTML wrapper for the project's swf                 |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| test                        | testCompile                                        | Runs the FlexUnit tests                                       |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| asdoc                       | testCompile                                        | Creates asdoc documentation for your sources                  |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+

The Flashbuilder plugin adds the following tasks to your project:

+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| Task name                   | Depends on                                         | Description                                                   |
+=============================+====================================================+===============================================================+
| flashbuilder                | n/a                                                | Creates the Adobe Flash Builder project files                 |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| flashbuilderClean           | n/a                                                | Deletes the Adobe Flash Builder project files                 |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+

The Scaffold plugin adds the following tasks to your project:

+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+
| Task name                   | Depends on                                         | Description                                                   |
+=============================+====================================================+===============================================================+
| scaffold                    | n/a                                                | Generates directory structure and main application class      |
|                             |                                                    |                                                               |
+-----------------------------+----------------------------------------------------+---------------------------------------------------------------+

-------------------------
Adding additional logic
-------------------------
Sometimes you may want to add custom logic right after or before a task has been executed. If you want to add some logging before or after the compile task, you can just do this: ::

    project.afterEvaluate {
       compile.doFirst {
          println "this gets printed before the compile task starts"
       }

       compile.doLast {
          println "this gets printed after the compile task has been completed"
       }
    }
The afterEvaluate statement is needed because most of the GradleFx tasks are added during this phase, so they won't be available during the beginning of the configuration phase. Most of the GradleFx tasks are added after the project's properties are evaluated because they depend on these properties to decide what to do, like for example the package task which is only added when you specified 'air' as the project's type.