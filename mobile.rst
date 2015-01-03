=======================
Mobile
=======================

This page describes how you can setup GradleFx to build your mobile project.

.. note::  There's a working example available in the GradleFx examples project: https://github.com/GradleFx/GradleFx-Examples/tree/master/mobile-android
.. note::  For a complete list of mobile convention properties, take a look at the ``airMobile`` and ``adt`` sections in the :doc:`properties_conventions` page. 

--------------
General setup
--------------
You'll have to define the project as a mobile project. You can define this as follows: ::

    type = 'mobile'
	
For other general AIR setup instructions, check out the AIR documentation page: :doc:`air` 

The mobile properties have conventions for Android, so if you're building for this platform, you're all set (unless you want to tune them a bit).
For iOS you'll have to override some convention properties.
Check out the platform specific sections for more information.

--------------
Android
--------------

^^^^^^^^^^^^^^^^^^^^^^^^^
Target & simulatorTarget
^^^^^^^^^^^^^^^^^^^^^^^^^
To specify how you want to package for Android, you can define the ``target`` property for installing to a device, or ``simulatorTarget`` for installing to a simulator.
This property defaults to ``apk`` for the ``target`` property and to ``apk-simulator`` for the ``simulatorTarget`` property.

These are all the targets you can use for Android:

| **apk** - an Android package. A package produced with this target can only be installed on an Android device, not an emulator.                                                                                                                                             |
| **apk-captive-runtime** - an Android package that includes both the application and a captive version of the AIR runtime. A package produced with this target can only be installed on an Android device, not an emulator.                                                 |
| **apk-debug** - an Android package with extra debugging information. (The SWF files in the application must also be compiled with debugging support.)                                                                                                                      |
| **apk-emulator** - an Android package for use on an emulator without debugging support. (Use the apk-debug target to permit debugging on both emulators and devices.)                                                                                                      |
| **apk-profile** - an Android package that supports application performance and memory profiling. 

You can specify it like this: ::

    airMobile {
        target = 'apk-debug'
    }
	
Or like this when you use any of the simulator tasks: ::

    airMobile {
		simulatorTarget = 'apk-emulator'
    }

--------------
iOS
--------------

^^^^^^^^^^^^^^
Platform
^^^^^^^^^^^^^^
The ``platform`` convention property defines the platform for which you want to deploy.
For iOS this value should be the following: ::

    airMobile {
	    platform = 'ios'
    }
	
^^^^^^^^^^^^^^^^^^^^^^^^^
Target & simulatorTarget
^^^^^^^^^^^^^^^^^^^^^^^^^
To specify how you want to package for iOS, you can define the ``target`` property for installing to a device, or ``simulatorTarget`` for installing to a simulator.
For iOS the ``target`` property is required, since it defaults to an Android value. The same is true for the ``simulatorTarget`` property in case you want to use a simulator.

These are all the targets you can use for iOS:

 | **ipa-ad-hoc** - an iOS package for ad hoc distribution.                                                                                                                                                                                                                   |
 | **ipa-app-store** - an iOS package for Apple App store distribution.                                                                                                                                                                                                       |
 | **ipa-debug** - an iOS package with extra debugging information. (The SWF files in the application must also be compiled with debugging support.)                                                                                                                          |
 | **ipa-test** - an iOS package compiled without optimization or debugging information.                                                                                                                                                                                      |
 | **ipa-debug-interpreter** - functionally equivalent to a debug package, but compiles more quickly. However, the ActionScript bytecode is interpreted and not translated to machine code. As a result, code execution is slower in an interpreter package.                  |
 | **ipa-debug-interpreter-simulator** - functionally equivalent to ipa-debug-interpreter, but packaged for the iOS simulator. Macintosh-only. If you use this option, you must also include the -platformsdk option, specifying the path to the iOS Simulator SDK.           |
 | **ipa-test-interpreter** - functionally equivalent to a test package, but compiles more quickly. However, the ActionScript bytecode is interpreted and not translated to machine code. As a result, code execution is slower in an interpreter package.                    |
 | **ipa-test-interpreter-simulator** - functionally equivalent to ipa-test-interpreter, but packaged for the iOS simulator. Macintosh-only. If you use this option, you must also include the -platformsdk option, specifying the path to the iOS Simulator SDK.

You can specify it like this: ::

    airMobile {
        target = 'ipa-debug'
    }
	
Or like this when you use any of the simulator tasks: ::

    airMobile {
		simulatorTarget = 'ipa-debug-interpreter-simulator'
    }
	
^^^^^^^^^^^^^^^^^^^^^^^^^^
Defining the target device
^^^^^^^^^^^^^^^^^^^^^^^^^^
For iOS you have to define the target device. This should be the ios_simulator or handle of the iOS device. ::

    airMobile {
		targetDevice 22
    }
	
You can find the handle of the attached devices with the following command: ::

    > adt -devices -platform ios
	
^^^^^^^^^^^^^^^^^^^^^^^^^^
Provisioning Profile
^^^^^^^^^^^^^^^^^^^^^^^^^^
To package an application for iOS, you need a provisioning profile provided by Apple. You can define it like this: ::
    
	airMobile {
		provisioningProfile = 'AppleDevelopment.mobileprofile'
	}
	
--------------
Tasks
--------------

To package a mobile project: ::

 > packageMobile
 > packageSimulatorMobile
 
To install a mobile project on a device/simulator: ::

 > installMobile
 > installSimulatorMobile
 
To uninstall a mobile project from a device/simulator: ::

 > uninstallMobile
 > uninstallSimulatorMobile
 
To launch a mobile project on a device/simulator: ::

 > launchMobile
 > launchSimulatorMobile

---------------------------------
Using native extensions (ANE)
---------------------------------

To use an ANE in your project you simple have to specify it as a dependency: ::

    dependencies {
       external group: 'org.mycompany', name: 'myane', version: '1.0', ext: 'ane'
    }

---------------------------------
Choosing a packaging mode
---------------------------------
Adobe AIR now supports two packaging compiler modes, a legacy compiler (which is slower) and a new compiler. For more information on this new compiler see http://www.adobe.com/devnet/air/articles/ios-packaging-compiled-mode.html

You can explicitly choose to use the new compiler by setting the ``nonLegacyCompiler`` property to true: ::

    airMobile {
        nonLegacyCompiler = true
    }
