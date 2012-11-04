==========================
Flex/AIR SDK Auto Install
==========================

GradleFx gives you the option to automatically download and install the Flex/AIR SDK. You can do this by specifying either of them as a dependency.
This mechanism supports both the Adobe and the Apache Flex SDK.

----------------
Overview
----------------

When you specify the SDK's you'll always have to use a packaged SDK. The supported archive formats are zip, tar.gz and tbz2.

What basically happens when you declare the dependency is this:

1. GradleFx will determine the install location of the SDK. By convention it will create an SDK specific directory in the %GRADLE_USER_HOME%/gradlefx/sdks directory. The name of the SDK specific directory is a hash of the downloaded sdk archive location.
2. When the SDK isn't yet installed GradleFx will install it.
3. Once installed it will assign the install location to the flexHome convention property.

GradleFx will always install the AIR SDK in the same directory as the Flex SDK.

 .. note:: A sample project which uses the auto-install feature can be found here: `Auto-install sample <https://github.com/GradleFx/GradleFx-Examples/blob/develop/sdk-autoinstall/build.gradle>`_

----------------
Dependency types
----------------

There are a couple of ways to specify the SDK's as dependencies.

^^^^^^^^^^^^^^^^^^^^^
Maven/Ivy Dependency
^^^^^^^^^^^^^^^^^^^^^

If you have deployed the SDK archives to a Maven/Ivy repository then you can specify them like this: ::

    dependencies {
	    flexSDK group: 'org.apache', name: 'apache-flex-sdk', version: '4.8.0', ext: 'zip'
	    airSDK  group: 'com.adobe', name: 'AdobeAIRSDK', version: '3.4', ext: 'zip'
	}
	
^^^^^^^^^^^^^^^^^^^^^
URL-based Dependency
^^^^^^^^^^^^^^^^^^^^^

You can also specify the SDK by referencing a URL. To do this you need to define custom Ivy URL Resolvers.
For example for the Apache Flex SDK this would be something like this: ::

	repositories {
		add(new org.apache.ivy.plugins.resolver.URLResolver()) {
			name = 'Apache'
			// pattern for url http://apache.cu.be/incubator/flex/4.8.0-incubating/binaries/apache-flex-sdk-4.8.0-incubating-bin.zip
			addArtifactPattern 'http://apache.cu.be/incubator/flex/4.8.0-incubating/binaries/[module]-[revision]-incubating-bin.[ext]'
		}
	}
	
Always make sure to replace the artifact name, version and extension type with [module], [revision] and [ext] in the pattern.
Once you've defined the pattern you can define the dependencies like this: ::

    dependencies {
	    flexSDK group: 'org.apache', name: 'apache-flex-sdk', version: '4.8.0', ext: 'zip'
	    airSDK  group: 'com.adobe', name: 'AdobeAIRSDK', version: '3.4', ext: 'zip'
	}
	
^^^^^^^^^^^^^^^^^^^^^
File-based dependency
^^^^^^^^^^^^^^^^^^^^^

And the last option is to specify the SDK's as file-based dependencies. This can be done as follows: ::
	
    dependencies {
	    flexSDK files('C:/sdks/flex-4.6-sdk.zip')
	    airSDK  files('C:/sdks/air-3.4-sdk.zip')
	}
	
-----------------------------
Apache Flex SDK dependencies
-----------------------------
As you may probably know the Apache Flex SDK requires some dependencies that aren't included in the SDK archive. 
GradleFx handles the installation of these dependencies for you. During the installation some prompts will be shown to accept some licenses.
When you've made sure you read the licenses, you can turn the prompts off (e.g. for a continuous integration build) like this: ::

    sdkAutoInstall {
	    showPrompts	= false
    }
	
