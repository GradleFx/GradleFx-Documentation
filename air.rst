========
AIR
========

This page describes how you need to configure your AIR project. Only a few things are needed for this.

.. note:: There's a working example available in the GradleFx examples project: https://github.com/GradleFx/GradleFx-Examples/tree/master/air-single-project

--------------
Project type
--------------

First you'll need to specify the project type, which in this case is 'air'. You do this as follows: ::

    type = 'air'

---------------------
AIR descriptor file
---------------------

Then you'll need an AIR descriptor file (like in every AIR project). If you give this file the same name as your project and put it in the default source directory (src/main/actionscript) then you don't have to configure anything because this is the convention. If you want to deviate from this convention you can specify the location like this: ::

    air {
		applicationDescriptor	'src/main/resources/airdescriptor.xml'
	}

--------------
Certificate
--------------

Then you'll need a certificate to sign the AIR package. This certificate has to be a *.p12 file. GradleFx uses the project name for the certificate by convention, so if your certificate is located at the root of your project and has a %myprojectname%.p12 filename; then you don't have to configure anything. If you want to deviate from this convention, then you can do this by overriding the air.keystore property:  ::

    air {
		keystore	'certificate.p12'
	}

You also need to specify the password for the certificate. This property is required. You can specify this as follows: ::

    air {
		storepass	'mypassword'
	}

If you don't want to put the password in the build file then you can use the properties system of Gradle, see the Gradle documentation for more information about this: http://www.gradle.org/docs/current/userguide/tutorial_this_and_that.html#sec:gradle_properties_and_system_properties

---------------------------------
Adding files to the AIR package
---------------------------------

In most cases you will want to add some files to your AIR package, like application icons which are being specified in your application descriptor like this: ::

    <icon>
        <image32x32>assets/appIcon.png</image32x32>
    </icon>

Only specifying those icons in your application descriptor won't do it for the compiler, so you need to provide them to it. With GradleFx you can do that with the includeFileTrees property, which looks like this: ::

    air {
		includeFileTrees = [
			fileTree(dir: 'src/main/actionscript/', include: 'assets/appIcon.png')
		]
	}

You have to make sure that the 'include' part always has the same name as the one specified in your application descriptor, otherwise the compiler won't recognize it. The fileTree also accepts patterns and multiple includes, more info about this can be found in the Gradle documentation: http://gradle.org/docs/current/userguide/working_with_files.html