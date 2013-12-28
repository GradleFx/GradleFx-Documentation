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
Other customizations
^^^^^^^^^^^^^^^^^^^^^^^

There are a lot more properties available on flexUnit.*, all these can be found on the properties description page.