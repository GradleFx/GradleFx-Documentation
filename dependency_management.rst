========================
Dependency Management
========================

----------------
Overview
----------------
The GradleFx plugin adds the following configurations to your project:

* **merged**: This configuration can be used for dependencies that should be merged in the SWC/SWF. Same as -compiler.library-path
* **internal**: The dependency content will be merged in the SWC/SWF. Same as -compiler.include-libraries
* **external**: The dependency won't be included in the SWC/SWF. Same as -compiler.external-library-path
* **rsl**: The SWF will have a reference to load the dependency at runtime. Same as -runtime-shared-library-path
* **test**: This is for dependencies used in unit tests
* **theme**: The theme that will be used by the application. Same as -theme

You can specify your dependencies like this: ::

    dependencies {
       external group: 'org.springextensions.actionscript', name: 'spring-actionscript-core', version: '1.2-SNAPSHOT', ext: 'swc'
       external group: 'org.as3commons', name: 'as3commons-collections', version: '1.1', ext: 'swc'
       external group: 'org.as3commons', name: 'as3commons-eventbus', version: '1.1', ext: 'swc'

       merged group: 'org.graniteds', name: 'granite-swc', version: '2.2.0.SP1', ext: 'swc'
       merged group: 'org.graniteds', name: 'granite-essentials-swc', version: '2.2.0.SP1', ext: 'swc'

       theme group: 'my.organization', name: 'fancy-theme', version: '1.0', ext: 'swc'
    }

--------------------------
Project Lib Dependencies
--------------------------
| You can also add dependencies to other projects, as described here in the Gradle documentation:
| https://docs.gradle.org/2.4/userguide/multi_project_builds.html#sec:project_jar_dependencies
