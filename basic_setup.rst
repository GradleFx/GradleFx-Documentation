=============
Basic Setup
=============

--------------
Requirements
--------------
* Gradle v1.6
* Minimum Flex 4.x

----------------------------------
Using the plugin in your project
----------------------------------
To use the plugin in your project, you'll have to add the following to your build.gradle file: ::

    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath group: 'org.gradlefx', name: 'gradlefx', version: '0.8.2'
        }
    }

    apply plugin: 'gradlefx'

Make sure that the buildscript structure is at the top of your build file.

---------------------------
Setting up the Flex/Air SDK
---------------------------
GradleFx gives you several options to specify the Flex/AIR SDK:
	1. set the FLEX_HOME environment variable (convention), this should point to your Flex/AIR SDK installation.
	2. set the flexHome convention property to the location of your Flex/AIR SDK ::

		flexHome = "C:/my/path/to/the/flex/sdk"
	
	3. specify the Flex/AIR SDK as a dependency. See :doc:`sdk_auto_install`

-----------------------------
Defining the project type
-----------------------------
| Every project should define its type, this can be one of the following:
| **swc**: a library project of which the sources will be packaged into a swc file
| **swf**: a Flex web project of which the sources will be packaged into a swf file.
| **air**: a Flex web project of which the sources will be packaged into a air file.
| **mobile**: a Flex mobile project of which the sources will be packaged into an apk or ipa file.

example project type definition: ::

    type = 'swc'