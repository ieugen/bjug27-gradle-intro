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

Step 2: The Gradle lifecycle
----------------------------

This step is a big deep dive, but I think it's important on the long run. If you understand this, it will make things much
more clearer.

Gradle, inspired by Maven has a lifecycle, but unlike Maven, it has a very simple and generic lifecycle.
It has three phases: Initialization, Configuratiion and Execution. When you run **gradle myTask** command for instance,
gradle will do the following:

* Initialization
  - identifies project to build
  - creates Project instance
* Configuration
  - executes buildscript{} for all its scope
  - configures the project objects
* Execution
  - creates the Task DAG
  - runs the build

>A more detailed description of the process is depicted bellow:
>
>During the **Initialization** phase, gradle will look for **settings.gradle** file to determine the projects involved
>in this build. After this it creates a *Project* instance which is an in-memory view of the projects it will build and
>starts the second pase **Configuration** which will populate the project instance.
>
>The **Configuration** phase is responible for populating the Project instance with configuration information: register
>the tasks involved with each project, what are the plugins needed to be applied and the tasks they provide.
>Build the list of properties that will be available for property place-holder replacement, run the buildscritp{} block, etc.
>
>The result of the **Configuration** phase is of course a configuration object (instance of Project). Gradle can now take
>this cofiguration, and with the task name supplied as parameter, determine the task graph: a graph of task and the order
>in which they should be executed, and execute them.

Bellow, you can see the graphs created for a project that uses the *java-plugin*
![Gradle task graphs for java-plugin](http://www.gradle.org/docs/current/userguide/img/javaPluginTasks.png)

In order to visualize the differences between configuration and execution phase you can run:
~~~
  gradle -q viewLifecycle
~~~

And you will get a sample output that looks like this:
~~~
This is executed during 'configuration' phase
This is still 'configuration' phase, inside a Task
This is the end of the 'configuration' phase
----------
This is 'execution' phase, second doFirst action
This is 'execution' phase, first doFirst action
This is 'execution' phase, first doLast action
This is 'execution' phase, second doLast actio
~~~



