==========================
Properties/Conventions
==========================
The GradleFx plugin provides some properties you can set in your build script. Most of them are using conventions, so you'll only need to specify them if you want to use your own values.

The following sections describe the properties you can/have to specify in your build script(required means whether you have to specify it yourself):

----------------------
Standard Properties
----------------------

+-----------------------------+----------------------------+----------+-------------------------------------------------+
| Property Name               | Convention                 | Required | Description                                     |
+=============================+============================+==========+=================================================+
| gradleFxUserHomeDir         | %GRADLE_USER_HOME%/gradleFx| false    | The location where GradleFx will store GradleFx |
|                             |                            |          | specific files (e.g. installed SDK's)           |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| flexHome                    | FLEX_HOME environment      | false    | The location of your Flex SDK                   |
|                             | var                        |          |                                                 |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| flexSdkName                 |                            | false    | The name you want to give to the Flex SDK       |
|                             |                            |          | Primarily used in the IDE integration           |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| type                        | n/a                        | true     | Whether this is a library project or an         |
|                             |                            |          | application. Possible values: 'swc', 'swf',     |
|                             |                            |          | 'air' or 'mobile'                               |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| srcDirs                     | ['src/main/actionscript']  | false    | An array of source directories                  |
|                             |                            |          |                                                 |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| resourceDirs                | ['src/main/resources']     | false    | An array of resource directories (used in the   |
|                             |                            |          | copyresources task, or included in the SWC for  |
|                             |                            |          | library projects)                               |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| testDirs                    | ['src/test/actionscript']  | false    | An array of test source directories             |
|                             |                            |          |                                                 |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| testResourceDirs            | ['src/test/resources']     | false    | An array of test resource directories           |
|                             |                            |          |                                                 |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| includeClasses              | null                       | false    | Equivalent of the include-classes compiler      |
|                             |                            |          | option. Accepts a list of classnames            |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| includeSources              | null                       | false    | Equivalent of the include-sources compiler      |
|                             |                            |          | option. Accepts a list of classfiles and/or     |
|                             |                            |          | directories.                                    |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| frameworkLinkage            | 'external' for swc         | false    | How the Flex framework will be linked in the    |
|                             | projects, 'rsl' for swf    |          | project: "external", "rsl", "merged" or "none"  |
|                             | projects and 'none' for    |          |                                                 |
|                             | pure as projects           |          |                                                 |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| useDebugRSLSwfs             | false                      | false    | Whether to use the debug framework rsl's when   |
|                             |                            |          | frameworkLinkage is rsl                         |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| additionalCompilerOptions   | []                         | false    | Additional compiler options you want to specify |
|                             |                            |          | to the compc or mxmlc compiler. Can be like     |
|                             |                            |          | ['-target-player=10', '-strict=false']          |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| fatSwc                      | null                       | false    | When set to true the asdoc information will be  |
|                             |                            |          | embedded into the swc so that Adobe Flash       |
|                             |                            |          | Builder can show the documentation              |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| localeDir                   | 'src/main/locale'          | false    | Defines the directory in which locale folders   |
|                             |                            |          | are located like en_US etc.                     |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| locales                     | []                         | false    | The locales used by your application. Can be    |
|                             |                            |          | something like ['en_US', 'nl_BE']               |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| mainClass                   | 'Main'                     | false    | This property is required for the mxmlc         |
|                             |                            |          | compiler. It defines the main class of your     |
|                             |                            |          | application. You can specify your own custom    |
|                             |                            |          | file like 'org/myproject/MyApplication.mxml' or |
|                             |                            |          | 'org.myproject.MyApplication'                   |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| output                      | ${project.name}            | false    | This is the name of the swc/swf that will be    |
|                             |                            |          | generated by the compile task                   |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| jvmArguments                | []                         | false    | You can use this property to specify jvm        |
|                             |                            |          | arguments which are used during the compile     |
|                             |                            |          | task. Only one jvm argument per array item: e.g.|
|                             |                            |          | jvmArguments = ['-Xmx1024m','-Xms512m']         |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| playerVersion               | '10.0'                     | false    | Defines the flash player version                |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| htmlWrapper                 | complex property           | false    | This is a complex property which contains       |
|                             |                            |          | properties for the createHtmlWrapper task       |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| flexUnit                    | complex property           | false    | This is a complex property which contains       |
|                             |                            |          | properties for the flexUnit task                |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| air                         | complex property           | false    | This is a complex property which contains       |
|                             |                            |          | properties for AIR projects                     |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| asdoc                       | complex property           | false    | This is a complex property which contains       |
|                             |                            |          | properties for the asdoc task                   |
+-----------------------------+----------------------------+----------+-------------------------------------------------+
| sdkAutoInstall              | complex property           | false    | This is a complex property which contains       |
|                             |                            |          | properties for the SDK auto install feature     |
+-----------------------------+----------------------------+----------+-------------------------------------------------+

 .. note:: All the available compiler options for the mxmlc and compc compiler are available
      here `Compc options <http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7a92.html>`_
      , `Mxmlc options <http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7a80.html>`_

--------------------
Complex properties
--------------------
^^^^^^^^^^^^^^^
air
^^^^^^^^^^^^^^^

+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                     |
+=============================+====================================================+==========+=================================================+
| keystore                    | "${project.name}.p12"                              | false    | The name of the certificate which will be used  |
|                             |                                                    |          | to sign the air package. Uses the project name  |
|                             |                                                    |          | by convention.                                  |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| storepass                   | null                                               | true     | The password of the certificate                 |
|                             |                                                    |          |                                                 |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| applicationDescriptor       | "src/main/actionscript/${project.name}.xml"        | false    | The location of the air descriptor file. Uses   |
|                             |                                                    |          | the project name by convention for this file.   |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| mainSwfDir                  | root directory of the package                      | false    | The directory in the package where the output   |
|                             |                                                    |          | swf file will be placed, for example 'foo/bar'  |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| includeFileTrees            | null                                               | false    | A list of FileTree objects which reference the  |
|                             |                                                    |          | files to include into the AIR package, like     |
|                             |                                                    |          | application icons which are specified in your   |
|                             |                                                    |          | application descriptor. Can look like this:     |
|                             |                                                    |          | air.includeFileTrees = [fileTree(dir:           |
|                             |                                                    |          | 'src/main/actionscript/', include:              |
|                             |                                                    |          | 'assets/appIcon.png')]                          |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| fileOptions                 | []                                                 | false    | Similar to includeFileTrees, but allows more    |
|                             |                                                    |          | flexibility without the convenience of a        |
|                             |                                                    |          | FileTree. It's most important use is to specify |
|                             |                                                    |          | directories instead of individual files.        |
|                             |                                                    |          | air.fileOptions = ['-C',                        |
|                             |                                                    |          | 'src/main/actionscript/',                       |
|                             |                                                    |          | 'sound']                                        |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+

^^^^^^^^^^^^^^^
airMobile
^^^^^^^^^^^^^^^

+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                                                                                                                                                                                                                                                     |
+=============================+====================================================+==========+=================================================================================================================================================================================================================================================================================+
| target                      | apk                                                | false    |  Specifies the mobile platform for which the package is created.                                                                                                                                                                                                                |
|                             |                                                    |          |                                                                                                                                                                                                                                                                                 |
|                             |                                                    |          |    | **ane** - an AIR native extension package                                                                                                                                                                                                                                  |
|                             |                                                    |          |                                                                                                                                                                                                                                                                                 |
|                             |                                                    |          |  Android package targets:                                                                                                                                                                                                                                                       |
|                             |                                                    |          |                                                                                                                                                                                                                                                                                 |
|                             |                                                    |          |    | **apk** - an Android package. A package produced with this target can only be installed on an Android device, not an emulator.                                                                                                                                             |
|                             |                                                    |          |    | **apk-captive-runtime** - an Android package that includes both the application and a captive version of the AIR runtime. A package produced with this target can only be installed on an Android device, not an emulator.                                                 |
|                             |                                                    |          |    | **apk-debug** - an Android package with extra debugging information. (The SWF files in the application must also be compiled with debugging support.)                                                                                                                      |
|                             |                                                    |          |    | **apk-emulator** - an Android package for use on an emulator without debugging support. (Use the apk-debug target to permit debugging on both emulators and devices.)                                                                                                      |
|                             |                                                    |          |    | **apk-profile** - an Android package that supports application performance and memory profiling.                                                                                                                                                                           |
|                             |                                                    |          |                                                                                                                                                                                                                                                                                 |
|                             |                                                    |          |  iOS package targets:                                                                                                                                                                                                                                                           |
|                             |                                                    |          |                                                                                                                                                                                                                                                                                 |
|                             |                                                    |          |    | **ipa-ad-hoc** - an iOS package for ad hoc distribution.                                                                                                                                                                                                                   |
|                             |                                                    |          |    | **ipa-app-store** - an iOS package for Apple App store distribution.                                                                                                                                                                                                       |
|                             |                                                    |          |    | **ipa-debug** - an iOS package with extra debugging information. (The SWF files in the application must also be compiled with debugging support.)                                                                                                                          |
|                             |                                                    |          |    | **ipa-test** - an iOS package compiled without optimization or debugging information.                                                                                                                                                                                      |
|                             |                                                    |          |    | **ipa-debug-interpreter** - functionally equivalent to a debug package, but compiles more quickly. However, the ActionScript bytecode is interpreted and not translated to machine code. As a result, code execution is slower in an interpreter package.                  |
|                             |                                                    |          |    | **ipa-debug-interpreter-simulator** - functionally equivalent to ipa-debug-interpreter, but packaged for the iOS simulator. Macintosh-only. If you use this option, you must also include the -platformsdk option, specifying the path to the iOS Simulator SDK.           |
|                             |                                                    |          |    | **ipa-test-interpreter** - functionally equivalent to a test package, but compiles more quickly. However, the ActionScript bytecode is interpreted and not translated to machine code. As a result, code execution is slower in an interpreter package.                    |
|                             |                                                    |          |    | **ipa-test-interpreter-simulator** - functionally equivalent to ipa-test-interpreter, but packaged for the iOS simulator. Macintosh-only. If you use this option, you must also include the -platformsdk option, specifying the path to the iOS Simulator SDK.             |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| extensionDir                |                                                    | false    | The name of a directory to search for native extensions (ANE files).                                                                                                                                                                                                            |
|                             |                                                    |          | Either an absolute path or a relative path from the project directory.                                                                                                                                                                                                          |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| targetDevice                |                                                    | false    | Specify ios_simulator, the serial number (Android), or handle (iOS) of the connected device.                                                                                                                                                                                    |
|                             |                                                    |          | On iOS, this parameter is required; on Android, this paramater only needs to be specified when more than one Android device or emulator is attached to your computer and running.                                                                                               |
|                             |                                                    |          | If the specified device is not connected, ADT returns exit code 14: Device error (Android) or Invalid device specified (iOS).                                                                                                                                                   |
|                             |                                                    |          | If more than one device or emulator is connected and a device is not specified, ADT returns exit code 2: Usage error                                                                                                                                                            |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| provisioningProfile         |                                                    | false    | The path to your iOS provisioning profile. Relative from your project directory.                                                                                                                                                                                                |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| outputExtension             | apk                                                | false    | The extension of the packaged application.                                                                                                                                                                                                                                      |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| platform                    | android                                            | false    | The name of the platform of the device. Specify ios or android.                                                                                                                                                                                                                 |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| platformSdk                 |                                                    | false    | The path to the platform SDK for the target device:                                                                                                                                                                                                                             |
|                             |                                                    |          | Android - The AIR 2.6+ SDK includes the tools from the Android SDK needed to implement the relevant ADT commands.                                                                                                                                                               |
|                             |                                                    |          | Only set this value to use a different version of the Android SDK. Also, the platform SDK path does not need to                                                                                                                                                                 |
|                             |                                                    |          | be supplied if the AIR_ANDROID_SDK_HOME environment variable is already set.                                                                                                                                                                                                    |
|                             |                                                    |          | iOS - The AIR SDK ships with a captive iOS SDK. The platformsdk option lets you package applications with an                                                                                                                                                                    |
|                             |                                                    |          | external SDK so that you are not restricted to using the captive iOS SDK.                                                                                                                                                                                                       |
|                             |                                                    |          | For example, if you have built an extension with the latest iOS SDK, you can specify that SDK when packaging                                                                                                                                                                    |
|                             |                                                    |          | your application. Additionally, when using ADT with the iOS Simulator, you must always include the platformsdk                                                                                                                                                                  |
|                             |                                                    |          | option, specifying the path to the iOS Simulator SDK.                                                                                                                                                                                                                           |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| simulatorPlatformSdk        |                                                    | false    | The path to the platform SDK for the simulator.                                                                                                                                                                                                                                 |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| simulatorTarget             | apk                                                | false    | Specifies the mobile platform of the simulator. See the target property for more information.                                                                                                                                                                                   |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| simulatorTargetDevice       |                                                    | false    | Specifies the device of the simulator. See the ``targetDevice`` property for more information.                                                                                                                                                                                  |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sampler                     | false                                              | false    | (iOS only, AIR 3.4 and higher) Enables the telemetry-based ActionScript sampler in iOS applications.                                                                                                                                                                            |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| nonLegacyCompiler           | false                                              | false    | Which compiler to use during packaging. When true, it will enable the new compiler which is faster. More info: http://www.adobe.com/devnet/air/articles/ios-packaging-compiled-mode.html                                                                                        |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

^^^^^^^^^^^^^^^
adl
^^^^^^^^^^^^^^^

+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                                                                                               |
+=============================+====================================================+==========+===========================================================================================================================+
| profile                     |                                                    | false    | ADL will debug the application with the specified profile.                                                                |
|                             |                                                    |          | Can have the following values: desktop, extendedDesktop, mobileDevice                                                     |
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------+
| screenSize                  |                                                    | false    | The simulated screen size to use when running apps in the mobileDevice profile on the desktop.                            |
|                             |                                                    |          | To specify the screen size as a predefined screen type, look at the list provided here:                                   |
|                             |                                                    |          | http://help.adobe.com/en_US/air/build/WSfffb011ac560372f-6fa6d7e0128cca93d31-8000.html                                    |
|                             |                                                    |          | | To specify the screen pixel dimensions directly, use the following format: widthXheight:fullscreenWidthXfullscreenHeight|
+-----------------------------+----------------------------------------------------+----------+---------------------------------------------------------------------------------------------------------------------------+

^^^^^^^^^^^^^^^
htmlWrapper
^^^^^^^^^^^^^^^

+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                     |
+=============================+====================================================+==========+=================================================+
| title                       | project.description                                | false    | The title of the html page                      |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| file                        | "${project.name}.html"                             | false    | Name of the html file                           |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| percentHeight               | '100'                                              | false    | Height of the swf in the html page              |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| percentWidth                | '100'                                              | false    | Width of the swf in the html page               |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| application                 | project.name                                       | false    | Name of the swf object in the HTML wrapper      |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| swf                         | project.name                                       | false    | The name of the swf that is embedded in the HTML|
|                             |                                                    |          | page. The '.swf' extension is added             |
|                             |                                                    |          | automatically, so you don't need to specify it. |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| history                     | 'true'                                             | false    | Set to true for deeplinking support.            |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| output                      | project.buildDir                                   | false    | Directory in which the html wrapper will be     |
|                             |                                                    |          | generated.                                      |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| expressInstall              | 'true'                                             | false    | use express install                             |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| versionDetection            | 'true'                                             | false    | use version detection                           |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| source                      | null                                               | false    | The relative path to your custom html template  |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+
| tokenReplacements           |[                                                   | false    | A map of tokens which will be replaced in your  |
|                             |   application:    wrapper.application,             |          | custom template. The keys have to be specified  |
|                             |                                                    |          | as ${key} in your template                      |
|                             |   percentHeight:  "$wrapper.percentHeight%",       |          |                                                 |
|                             |                                                    |          |                                                 |
|                             |   percentWidth:   "$wrapper.percentWidth%",        |          |                                                 |
|                             |                                                    |          |                                                 |
|                             |   swf:            wrapper.swf,                     |          |                                                 |
|                             |                                                    |          |                                                 |
|                             |   title:          wrapper.title                    |          |                                                 |
|                             |]                                                   |          |                                                 |
|                             |                                                    |          |                                                 |
+-----------------------------+----------------------------------------------------+----------+-------------------------------------------------+

^^^^^^^^^^^^^^^
flexUnit
^^^^^^^^^^^^^^^
(Since GradleFx uses the FlexUnit ant tasks it also uses the same properties, more information about the properties specified in this table can be found in the "Property Descriptions" section on this page: http://docs.flexunit.org/index.php?title=Ant_Task)

+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                        |
+=============================+====================================================+==========+====================================================+
| template                    | Uses the internal template provided by GradleFx    | false    | The path to your test runner template relative     |
|                             |                                                    |          | from the project directory                         |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| player                      | 'flash'                                            | false    | Whether to execute the test SWF against the        |
|                             |                                                    |          | Flash Player or ADL. See the "Property             |
|                             |                                                    |          | Descriptions" section on this page for more        |
|                             |                                                    |          | information:                                       |
|                             |                                                    |          | http://docs.flexunit.org/index.php?title=Ant_Task  |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| command                     | FLASH_PLAYER_EXE environment variable              | false    | The path to the Flash player executable which will |
|                             |                                                    |          | be used to run the tests                           |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| toDir                       | "${project.buildDirName}/reports"                  | false    | Directory to which the test result reports are     |
|                             |                                                    |          | written                                            |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| workingDir                  | project.path                                       | false    | Directory to which the task should copy the        |
|                             |                                                    |          | resources created during compilation.              |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| haltonfailure               | 'false'                                            | false    | Whether the execution of the tests should stop once|
|                             |                                                    |          | a test has failed                                  |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| verbose                     | 'false'                                            | false    | Whether the tasks should output information about  |
|                             |                                                    |          | the test results                                   |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| localTrusted                | 'true'                                             | false    | The path specified in the 'swf' property is added  |
|                             |                                                    |          | to the local FlashPlayer Trust when this property  |
|                             |                                                    |          | is set to true.                                    |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| port                        | '1024'                                             | false    | On which port the task should listen for test      |
|                             |                                                    |          | results                                            |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| buffer                      | '262144'                                           | false    | Data buffer size (in bytes) for incoming           |
|                             |                                                    |          | communication from the Flash movie to the task.    |
|                             |                                                    |          | Default should in general be enough, you could     |
|                             |                                                    |          | possibly increase this if your tests have lots of  |
|                             |                                                    |          | failures/errors.                                   |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| timeout                     | '60000'                                            | false    | How long (in milliseconds) the task waits for a    |
|                             |                                                    |          | connection with the Flash player                   |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| failureproperty             | 'flexUnitFailed'                                   | false    | If a test fails, this property will be set to true |
|                             |                                                    |          |                                                    |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| headless                    | 'false'                                            | false    | Allows the task to run headless when set to true.  |
|                             |                                                    |          |                                                    |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| display                     | '99'                                               | false    | The base display number used by Xvnc when running  |
|                             |                                                    |          | in headless mode.                                  |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| includes                    | ['**/*Test.as']                                    | false    | Defines which test classes are executed when       |
|                             |                                                    |          | running the tests                                  |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| excludes                    | []                                                 | false    | Defines which test classes are excluded from       |
|                             |                                                    |          | execution when running the tests                   |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| swfName                     | "TestRunner.swf"                                   | false    | the name you want to give to the resulting test    |
|                             |                                                    |          | runner application                                 |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| additionalCompilerOptions   | []                                                 | false    | A list of custom compiler options for the test     |
|                             |                                                    |          | runner application                                 |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| ignoreFailures              | 'false'                                            | false    | When enabled, failed tests will be ignored and     |
|                             |                                                    |          | won't make the build fail                          |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+

^^^^^^^^^^^^^^^
asdoc
^^^^^^^^^^^^^^^

+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                        |
+=============================+====================================================+==========+====================================================+
| outputDir                   | 'doc'                                              | false    | The directory in which the asdoc documentation     |
|                             |                                                    |          | will be created                                    |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| additionalASDocOptions      | []                                                 | false    | Additional options for the asdoc compiler.         |
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+

^^^^^^^^^^^^^^^
sdkAutoInstall
^^^^^^^^^^^^^^^

+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+
| Property Name               | Convention                                         | Required | Description                                        |
+=============================+====================================================+==========+====================================================+
| showPrompts                 | true                                               | false    | Whether to show prompts during the installation    |
|                             |                                                    |          | or let it run in full auto mode. Make sure you     |
|                             |                                                    |          | agree with all the licenses before turning this off|
+-----------------------------+----------------------------------------------------+----------+----------------------------------------------------+

.. note:: All the available asdoc options (for Flex 4.6) can be found here: `asdoc compiler options <http://help.adobe.com/en_US/flex/using/WSd0ded3821e0d52fe1e63e3d11c2f44bc36-7ffa.html#WSd0ded3821e0d52fe1e63e3d11c2f44bb7b-7feb>`_

------------------------------
Example usage (build.gradle)
------------------------------
::

    buildscript {
        repositories {
            mavenLocal()
        }
        dependencies {
            classpath group: 'org.gradlefx', name: 'gradlefx', version: '0.5'
        }
    }

    apply plugin: 'gradlefx'

    flexHome = System.getenv()['FLEX_SDK_LOCATION'] //take a custom environment variable which contains the Flex SDK location

    srcDirs = ['/src/main/flex']

    additionalCompilerOptions = [
      '-player-version=10',
      '-strict=false'
    ]

    htmlWrapper {
		title         = 'My Page Title'
		percentHeight =	80
		percentWidth  =	80
	}
