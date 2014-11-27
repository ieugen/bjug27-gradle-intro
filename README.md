Gradle build automation tool
============================

A step by step intro to Gradle
------------------------------

You can use this project to get an intro to Gradle. You will need git and java.
The code is organized as a series of branches that you can check-out and follow the instructions in this README.
The *master* branch will contain all contributions and the latest version.
Individual branches will guide you through every step.

You can get the latest version of this guide from [https://github.com/ieugen/bjug27-gradle-intro](https://github.com/ieugen/bjug27-gradle-intro)


Step 1: from 0 to Gradle
------------------------

To use gradle, first download and install it: [http://gradle.org/](http://gradle.org/). I'm using version 2.1.

Once you have it on your path you can use the init plugin to create an empty project:
~~~
   $ gradle init 
~~~

The init plugin is documented [Build init plugin](http://www.gradle.org/docs/current/userguide/build_init_plugin.html).
It provides other templates to bootstrap software projects: java-library, scala-library, pom, etc.
~~~
  $ gradle init --type java-library
~~~

We need a *base* type project, which is default. This has an empty **build.gradle** project with comments on how to
change it to turn it into a  *java* project.

In this gradle project, like in any other, you can run the Gradle commands to get information about the project:

~~~
  $ gradle tasks ; echo "Display the list of tasks available -- depends on the plugins declared in the build script"
~~~

You will get a sample output like the one following this paragraph. Those are the built-in tasks available.
You can use **projects** task to list all pprojects (usefull in multi-module builds), you can use **properties** task to
list the properties Gradle knows about, and will use instead of your placeholders, etc.

~~~
------------------------------------------------------------
All tasks runnable from root project
------------------------------------------------------------

Build Setup tasks
-----------------
init - Initializes a new Gradle build. [incubating]
wrapper - Generates Gradle wrapper files. [incubating]

Help tasks
----------
components - Displays the components produced by root project 'bjug27-gradle'.
dependencies - Displays all dependencies declared in root project 'bjug27-gradle'.
dependencyInsight - Displays the insight into a specific dependency in root project 'bjug27-gradle'.
help - Displays a help message
projects - Displays the sub-projects of root project 'bjug27-gradle'.
properties - Displays the properties of root project 'bjug27-gradle'.
tasks - Displays the tasks runnable from root project 'bjug27-gradle'.

To see all tasks and more detail, run with --all.

BUILD SUCCESSFUL
~~~
