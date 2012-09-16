=============
AsDoc
=============
GradleFx has support for generating asdoc documentation for your swc-based projects.

--------------
How to use it
--------------
No specific configuration is needed for this, you can simply execute the "gradle asdoc" command and it will create a doc folder in your project which will contain the html documentation files.

^^^^^^^^^^^^^^^^^^^^^
Creating a fat swc
^^^^^^^^^^^^^^^^^^^^^

A fat swc is a swc file which has asdoc information embedded in it so that Adobe Flash Builder can show the documentation while you're working in it. GradleFx has a handly property for this which, when turned on, will always create a fat swc when you compile your project. This property can be set like this: ::

    fatSwc = true

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Customizing the asdoc generation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

GradleFx also provides some properties which can be used to customize the asdoc generation.
One of them is the asdoc.outputDir property, which allows you to specify a different destination directory for the asdoc documentation. This property can be used as follows: ::

    asdoc {
		outputDir	'documentation' //will create the documentation in the %projectdir%/documentation folder
	}

Another property which allows the most customization is the asdoc.additionalASDocOptions property. It can be used like the additionalCompilerOptions, but this one accepts asdoc compiler options.
These options can be found here (for Flex 4.6): `asDoc compiler options <http://help.adobe.com/en_US/flex/using/WSd0ded3821e0d52fe1e63e3d11c2f44bc36-7ffa.html#WSd0ded3821e0d52fe1e63e3d11c2f44bb7b-7feb>`_

The property can be used as follows: ::

    asdoc {
		additionalASDocOptions = [
			'-strict=false',
			'-left-frameset-width 200'
		]
	}