=============
Basic Setup
=============

--------------
Requirements
--------------
* Gradle v1.0

----------------------------------
Using the plugin in your project
----------------------------------
To use the plugin in your project, you'll have to add the following to your build.gradle file: ::

    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath group: 'org.gradlefx', name: 'gradlefx', version: '0.5'
        }
    }

    apply plugin: 'gradlefx'

Make sure that the buildscript structure is at the top of your build file.

--------------------------
Setting up the Flex SDK
--------------------------
You'll need the Flex SDK installed on your computer. GradleFx uses the FLEX_HOME environment variable by convention, this should point to your Flex SDK installation. If you don't want to use this convention you can just override this default by doing this:::

    flexHome = C:\my\path\to\the\flex\sdk

-----------------------------
Defining the project type
-----------------------------
| Every project should define its type, this can be one of the following:
| **swc**: a library project of which the sources will be packaged into a swc file
| **swf**: a Flex web project of which the sources will be packaged into a swf file.
| **air**: a Flex web project of which the sources will be packaged into a air file.

example project type definition: ::

    type = 'swc'