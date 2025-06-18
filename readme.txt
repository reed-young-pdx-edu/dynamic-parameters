Copyright (C) 2025 Portland State University
Dynamic Parameters for ImageJ2 - Reed Young

Dynamic Parameters is a preprocessor plugin for ImageJ2 that allows for more
customization in the input parameters for commands.  It allows for the number
and types of parameters to be changed dynamically in response to user input.
It is well suited for commands that have different parameters depending on other
parameters, such as a command that runs different algorithms that each have
different inputs.  It also has support for errors and warnings that depend on
the inputs.

INSTALLATION

To install the plugin, the update site "DHM Utilities" with the URL
"http://sites.imagej.net/Sudgy/" may simply be added in the ImageJ updater.  To modify the plugin or to install it without
the rest of DHM utilities, compile with maven and then copy the jar
to the ImageJ plugins folder, removing the old one if you need to.  Dependencies, listed in pom.xml, are likely already included in the ImageJ2/Fiji distribution, so any errors encountered while compiling are likely due to repositories moving.

The documentation can be created using maven's javadoc
plugin, and will be created in target/site/apidocs/.

USE

This plugin is intended for ImageJ2 programmers, to enhance other plugins by
allowing dynamic changes to parameters.  End-users of ImageJ will not
necessarily know they are using this plugin, when it is called by the
plugin that they are directly using.

To use this plugin, the programmer must have (or define) a SciJava @Parameter of a type that implements
the DParameter interface.  The DynamicPreprocessor class will find all of those
parameters and make a dialog for them.  (Note that this is separate from the
normal populating of parameters, so if you have a mixture of normal parameters
and dynamic parameters, two dialogs will show.)  DParameter is a generic type,
and its getValue() function will return the value that it has.

There are 5 types of simple parameters that come packaged with the plugin:

 - BoolParameter:   Get a boolean, through a checkbox.
 - ChoiceParameter: Pick a string from a list of strings.
 - DoubleParameter: Get a floating point number.  It also has support for
                    picking the number of decimal digits allowed, and for bounds
                    checking.  The default decimal digits is three and there are
                    no default bounds.
 - ImageParameter:  Get an ImagePlus from the currently open images.  The
                    command will refuse to start if there are no images open.
 - IntParameter:    Get an integer.  It supports bounds checking in the same way
                    as DoubleParameter.

In addition to these simple parameters, there is also the abstract class
HoldingParameter.  It is meant to be the superclass for any parameter that holds
other parameters.  Please consult that class's documentation on its use.

If you have any questions that are not answered here, in the documentation, or
in the source code, please email Reed Young at rry@pdx.edu.
