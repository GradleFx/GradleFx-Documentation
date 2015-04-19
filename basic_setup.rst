=============
Basic Setup
=============

--------------
Requirements
--------------
* Gradle v2.0
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
            classpath group: 'org.gradlefx', name: 'gradlefx', version: '1.2.0'
        }
    }

    apply plugin: 'gradlefx'

Make sure that the buildscript structure is at the top of your build file.

---------------------------
Setting up the Flex/Air SDK
---------------------------
Depending on your project, you'll need the Flex and/or AIR SDK. GradleFx gives you several options to specify the Flex/AIR SDK:
	1. set the FLEX_HOME environment variable (convention), this should point to your Flex/AIR SDK installation.
	2. set the flexHome convention property to the location of your Flex/AIR SDK ::

		flexHome = "C:/my/path/to/the/flex/sdk"
	
	3. specify the Flex/AIR SDK as a dependency. See :doc:`sdk_auto_install`

-----------------------------
Defining the project type
-----------------------------
| Every project should define its type, this can be one of the following:
| **swc**: a library project of which the sources will be packaged into a swc file
| **swcAir**: similar to the 'swc' type, but this automatically adds the air libraries (by using the air-config.xml file provided in the SDK)
| **swf**: a Flex web project of which the sources will be packaged into a swf file.
| **air**: a Flex web project of which the sources will be packaged into a air file.
| **mobile**: a Flex mobile project of which the sources will be packaged into an apk or ipa file.

example project type definition: ::

    type = 'swc'

-----------------------------
Flex or pure Actionscript?
-----------------------------
GradleFx also needs to know whether you want to use the Flex framework, since you can also create an Actionscript-only project. Several situations are possible here: 

* When you only use the AIR SDK it's easy, you don't have to do anything special. It will be an Actionscript-only project by default and no Flex framework linkage will happen. GradleFx will also use the ASC 2.0 compiler provided in the new AIR SDKs by default.
* When using the Flex SDK (with or without the AIR SDK), by default GradleFx (and the compiler) will assume you'll use the Flex framework. However, when you want to build an Actionscript-only project that just uses the Flex SDK compilers, then you have to set framework linkage to 'none' as follows: ::
 
    frameworkLinkage = 'none'