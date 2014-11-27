Gradle build automation tool
============================

A step by step intro to Gradle
------------------------------

You can use this project to get an intro to Gradle. You will need git and java.
The code is organized as a series of branches that you can check-out and follow the instructions in this README.
The *master* branch will contain all contributions and the latest version.
Individual branches will guide you through every step.


Step 1: from 0 to Gradle
------------------------

To use gradle, first download and install it: [http://gradle.org/](http://gradle.org/). I'm using version 2.1.

Once you have it on your path you can use the init plugin to create an empty project:

   $ gradle init 

The init plugin is documented [Build init plugin](http://www.gradle.org/docs/current/userguide/build_init_plugin.html).
It provides other templates to bootstrap software projects: java-library, scala-library, pom, etc.

  $ gradle init --type java-library

