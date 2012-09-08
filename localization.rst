================
Localization
================
GradleFx provides an easy way to specify locales instead of having to specify the compiler arguments. The two convention properties of importance are:

* **localeDir**: This defines the directory in which locale folders are located (relative from the project root). The convention here is 'src/main/locale'
* **locales**: Defines a list of locales used by your application, like en_US, nl_BE, etc. This property has no default.

Let's say you want to support the en_GB and nl_BE locales. Then you could have the following directory structure:

* %PROJECT_ROOT%/src/main/locale/en_GB/resources.properties
* %PROJECT_ROOT%/src/main/locale/nl_BE/resources.properties

Because 'src/main/locale' is already the default value for the localeDir property you only have to specify the locales, like this: ::

    locales = ['en_GB', 'nl_BE']

You can also change the default value of the localeDir in case you don't want to follow the convention like this: ::

    localeDir = 'locales' //directory structure will then look like this: %PROJECT_ROOT%/locales/en_GB