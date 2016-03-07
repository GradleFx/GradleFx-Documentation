===========
FlexUnit
===========

GradleFx supports automatically running tests written with FlexUnit 4.1.

--------------------------------
Setting up testing in GradleFx
--------------------------------
First you need to specify the FlexUnit dependencies. You can download the required FlexUnit libraries from their site and then deploy them on your repository (recommended) or use file-based dependencies. Once you've done that you have to define them as dependencies in your build file.

1. When you have deployed the artifacts on your own repository: ::

    dependencies {
        test group: 'org.flexunit', name: 'flexunit-tasks', version: '4.1.0-8', ext: 'swc'
        test group: 'org.flexunit', name: 'flexunit', version: '4.1.0-8', ext: 'swc'
        test group: 'org.flexunit', name: 'flexunit-cilistener', version: '4.1.0-8', ext: 'swc'
        test group: 'org.flexunit', name: 'flexunit-uilistener', version: '4.1.0-8', ext: 'swc'
    }
2. When you have FlexUnit installed on your machine: ::

    def flexunitHome = System.getenv()['FLEXUNIT_HOME']  //FLEXUNIT_HOME is an environment variable referencing the FlexUnit install location
    dependencies {
        test files("${flexunitHome}/flexunit-4.1.0-8-flex_4.1.0.16076.swc",
                   "${flexunitHome}/flexUnitTasks-4.1.0-8.jar",
                   "${flexunitHome}/flexunit-cilistener-4.1.0-8-4.1.0.16076.swc",
                   "${flexunitHome}/flexunit-uilistener-4.1.0-8-4.1.0.16076.swc")
    }
	
Then you'll need to specify the location of the Flash Player executable. GradleFx uses the FLASH_PLAYER_EXE environment variable by convention which should contain the path to the executable. If you don't want to use this environment variable you can override this with the 'flexUnit.command' property. You can download the executable from here (these links may get out of date, look for the Flash Player standalone/projector builds on the Adobe site):

* `For Windows <http://download.macromedia.com/pub/flashplayer/updaters/10/flashplayer_10_sa_debug.exe>`_
* `For Mac <http://download.macromedia.com/pub/flashplayer/updaters/10/flashplayer_10_sa_debug.app.zip>`_
* `For Linux <http://download.macromedia.com/pub/flashplayer/updaters/10/flashplayer_10_sa_debug.tar.gz>`_

And that's basically it in terms of setup when you follow the following conventions:

* Use src/test/actionscript as the source directory for your test classes.
* Use src/test/resources as the directory for your test resources.
* You end all your test class names with "Test.as"

GradleFx will by convention execute all the *Test.as classes in the test source directory when running the tests.

-------------------
Running the tests
-------------------
You can run the FlexUnit tests by executing the "gradle test" command on the command-line.

-------------------
Skipping the tests
-------------------
In case you want to execute a task which depends on the test task, but you don't want to execute the tests, then you can skip the test execution by excluding the test task with the '-x test' parameter. Like this: ::

    > gradle build -x test

---------------
Customization
---------------
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changing the source/resource directories
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can change these directories by specifying the following properties like this: ::

    testDirs = ['src/testflex']
    testResourceDirs = ['src/testresources']

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Include/Exclude test classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can include or exclude test classes which are being run by specifying a pattern to some GradleFx properties.
To specify the includes you can use the flexUnit.includes property: ::

    flexUnit {
        includes = ['**/Test*.as'] //will include all actionscript classes which start with 'Test'
    }

To specify the excludes you can use the flexUnit.excludes property: ::

    flexUnit {
        excludes = ['**/*IntegrationTest.as']
    }
	
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Use a custom test runner template
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you want to customize the test application which runs your unit tests, you can create a custom template for this.
An example of such a template can be found here `<https://github.com/GradleFx/GradleFx-Examples/blob/master/flexunit-single-project/src/test/resources/CustomFlexUnitRunner.mxml>`_   

This template accepts two parameters:

* *fullyQualifiedNames:* These are the fully qualified names of the test classes (e.g. 'org.gradlefx.SomeTest')
* *testClasses:* These are the test class names (e.g. 'SomeTest')

Once you've created your template, you can specify it in your build script: ::

    flexUnit {
        template = 'src/test/resources/CustomFlexUnitRunner.mxml'
    }	
	
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Add custom compiler options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In some cases you want to specify custom compiler options to your test application, for example for keeping certain metadata.
You can do this by using the flexUnit.additionalCompilerOptions property: ::

    flexUnit {
        additionalCompilerOptions = [
            '-incremental=true',
        ]
    }
	
^^^^^^^^^^^^^^^^^^^^^^^
Ignoring test failures
^^^^^^^^^^^^^^^^^^^^^^^
By default, when a test fails the build will fail. If you want to ignore test failures, then you can do this with the following property: ::

    flexUnit {
        ignoreFailures = true
    }    

^^^^^^^^^^^^^^^^^^^^^^^
Other customizations
^^^^^^^^^^^^^^^^^^^^^^^

There are a lot more properties available on flexUnit.*, all these can be found on the properties description page.

---------------
FAQ
---------------
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
My unit tests hang and then end with a SocketTimeoutException, what is wrong?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This generally means some kind of incompatibility between the AIR, Flash and SWF version you're using. By default, Flex and AIR target a certain Flash Player version by compiling against a certain SWF version. To find out what is wrong, we need to gather some info first.

First we need to find out against which SWF version your TestRunner SWF has been compiled by GradleFx. The Flex and AIR SDKs come with a handy tool to determine the SWF version of a SWF, called swfdump, which is located in the %FLEX_AIR_SDK%/bin folder. Execute this tool against the TestRunner.swf located in %YOUR_PROJECT%/build/reports folder. Stop its executing right after it starts, because we're only interested in the first part of its output (it outputs quite a lot). ::

    > %FLEX_AIR_SDK%/bin/swfdump %YOUR_PROJECT%/build/reports/TestRunner.swf

The output might look like this: ::

    Adobe SWF Dump Utility
    Version 2.0.0 build 354139
    Copyright 2003-2012 Adobe Systems Incorporated. All rights reserved.

    <?xml version="1.0" encoding="UTF-8"?>
    <!-- Parsing swf file:/C:/myproject/build/reports/TestRunner.swf -->
    <swf xmlns="http://macromedia/2003/swfx" version="26" framerate="24.0" size="10000x7500" compressed="true" >

So in this output we can see that this SWF uses version 26. This is something we can match against the `Flash Player and Adobe AIR compatibility list <http://www.adobe.com/devnet/articles/flashplayer-air-feature-list.html>`_ to find out whether this matches your AIR SDK. When I look up SWF version 26 I can see it's being used by default by AIR SDK 15.

If this isn't the expected AIR SDK version, then you might be using a Flex version which targets a newer Flash Player version than your AIR SDK supports. So either you upgrade your AIR SDK to the version which matches the SWF version (see `Flash Player and Adobe AIR compatibility list <http://www.adobe.com/devnet/articles/flashplayer-air-feature-list.html>`_), or you specify the '-swf-version' compiler option to FlexUnit so that it matches the SWF version supported by your AIR SDK: ::

    flexUnit {
        additionalCompilerOptions = [
            '-swf-version=25'
        ]
    }