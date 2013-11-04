=============
Html Wrapper
=============

GradleFx allows you to create a html wrapper for your application by using the createHtmlWrapper task and the htmlWrapper convention properties.

--------------
Usage
--------------

^^^^^^^^^^^^^^^^^^^^^
Execution
^^^^^^^^^^^^^^^^^^^^^

You can create the html wrapper files without having to specify any htmlWrapper convention properties. Just execute the createHtmlWrapper task like this and it will use the conventions: ::

    >gradle createHtmlWrapper
	
^^^^^^^^^^^^^^^^^^^^^
Customization
^^^^^^^^^^^^^^^^^^^^^

You can customize the conventions by overriding the htmlWrapper properties, like this: ::

    htmlWrapper {
		title         = 'My Page Title'
		percentHeight =	80
		percentWidth  =	80
	}
	
.. note:: For a full list of htmlWrapper properties, visit the properties section: :doc:`properties_conventions`

You can also provide your own html page which contains replaceable tokens. This can be done with the help of the htmlWrapper.source and htmlWrapper.tokenReplacements properties.
source is the relative path to an existing HTML-file that can be provided as a template instead of using the default one. If the property isn't provided, the template will be generated with the default html file.

tokenReplacements is map of replacements for tokens in the provided source file. If the template contains the token ${swf}, it'll be replaced with 'example' if this property contains a [swf:example] mapping. If source isn't specified, this property will be ignored.

You can use this as follows: ::

    htmlWrapper {
		source            = 'myCustomTemplate.html'
		tokenReplacements = [swf:example]
	}    



