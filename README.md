# Simple Gradle app
 

reference : https://www.youtube.com/watch?v=-dtcEMLNmn0


# Initialize

## git

```
git init
```

## gradle

```
gradle init

steve@minty:~/projects/simple_gradle$ gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin

1

Select build script DSL:
  1: Groovy
  2: Kotlin

1

Generate build using new APIs and behavior (some features may change in the next minor release)? (default: no) [yes, no]                                                                                                         yes


Project name (default: simple_gradle): gradle-tutorial
```

## Directory structure

```
steve@minty:~/projects/simple_gradle$ tree
.
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── README_install_gradle.md
├── README_installjava.md
└── settings.gradle

2 directories, 8 files

```

## Build test (Just creates a local gradle env):

```
steve@minty:~/projects/simple_gradle$ ./gradlew
Downloading https://services.gradle.org/distributions/gradle-7.4.1-bin.zip
...........10%...........20%...........30%...........40%...........50%...........60%...........70%...........80%...........90%...........100%

```

## What are gradle tasks


### List available tasks

```
steve@minty:~/projects/simple_gradle$ ./gradlew tasks

> Task :tasks

------------------------------------------------------------
Tasks runnable from root project 'gradle-tutorial'
------------------------------------------------------------

Build Setup tasks
-----------------
init - Initializes a new Gradle build.
wrapper - Generates Gradle wrapper files.

Help tasks
----------
buildEnvironment - Displays all buildscript dependencies declared in root project 'gradle-tutorial'.
dependencies - Displays all dependencies declared in root project 'gradle-tutorial'.
dependencyInsight - Displays the insight into a specific dependency in root project 'gradle-tutorial'.
help - Displays a help message.
javaToolchains - Displays the detected java toolchains.
outgoingVariants - Displays the outgoing variants of root project 'gradle-tutorial'.
projects - Displays the sub-projects of root project 'gradle-tutorial'.
properties - Displays the properties of root project 'gradle-tutorial'.
tasks - Displays the tasks runnable from root project 'gradle-tutorial'.

To see all tasks and more detail, run gradlew tasks --all

To see more detail about a task, run gradlew help --task <task>

BUILD SUCCESSFUL in 748ms
1 actionable task: 1 executed
steve@minty:~/projects/simple_gradle$ 
```

* Project has a build script, scripts have tasks.

* Run a task : ./gradlew <task name>


* We use plugins in the build script to add tasks

### About groovy


runs on JVM
Gradle Groovy DSL (Domain Specific Langauge)

Is a scripting langauge:

```
def myVar = 'Executing as a script'
println myVar

semicolons optional
brackets optional

def myClosure = {
   println 'Executing closure'
}
myClosure()
```

But you don't really need to know much.


## The build script

```
Put your classes in 
   src/main/java


steve@minty:~/projects/simple_gradle$ vim src/main/java/com/test777767ont/GradleTutorial.java

steve@minty:~/projects/simple_gradle$ vim build.gradle
steve@minty:~/projects/simple_gradle$ cat build.gradle 
plugins {
	id 'java'
}

That added some new tasks.

So build it I guess:

steve@minty:~/projects/simple_gradle$ ./gradlew build

BUILD SUCCESSFUL in 1s
2 actionable tasks: 2 executed
steve@minty:~/projects/simple_gradle$ 

```

### Latest directory structure

```

steve@minty:~/projects/simple_gradle$ tree
.
├── build
│   ├── classes
│   │   └── java
│   │       └── main
│   │           └── com
│   │               └── test777767ont
│   │                   └── GradleTutorial.class
│   ├── generated
│   │   └── sources
│   │       ├── annotationProcessor
│   │       │   └── java
│   │       │       └── main
│   │       └── headers
│   │           └── java
│   │               └── main
│   ├── libs
│   │   └── gradle-tutorial.jar
│   └── tmp
│       ├── compileJava
│       │   └── previous-compilation-data.bin
│       └── jar
│           └── MANIFEST.MF
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── README_install_gradle.md
├── README_install_groovy.md
├── README_installjava.md
├── README.md
├── settings.gradle
├── simple_goove.groovy
└── src
    └── main
        └── java
            └── com
                └── test777767ont
                    └── GradleTutorial.java

```


### Can't run the jar yet:

```
steve@minty:~/projects/simple_gradle$ java -jar build/libs/gradle-tutorial.jar 
no main manifest attribute, in build/libs/gradle-tutorial.jar
steve@minty:~/projects/simple_gradle$

```

So, java doesn't know what class to run in the jar.

```
steve@minty:~/projects/simple_gradle$ jar -tf build/libs/gradle-tutorial.jar 
META-INF/
META-INF/MANIFEST.MF
com/
com/test777767ont/
com/test777767ont/GradleTutorial.class
```

We need to add a Main-Class attribute to the manifest ; gradle can do this.

```
steve@minty:~/projects/simple_gradle$ vim build.gradle 
steve@minty:~/projects/simple_gradle$ cat build.gradle 
plugins {
	id 'java'
}

jar {
	manifest {
		attributes 'Main-Class': 'com.test777767ont.GradleTutorial'
	}
}
```

### Re-build:

```
steve@minty:~/projects/simple_gradle$ ./gradlew build

BUILD SUCCESSFUL in 1s
2 actionable tasks: 1 executed, 1 up-to-datsteve@minty:~/projects/simple_gradle$ ./gradlew build

```

### Run again.

```
steve@minty:~/projects/simple_gradle$ java -jar build/libs/gradle-tutorial.jar 
Gradle 4tw!

```

## Testing

Gradle uses: src/test/java

```
steve@minty:~/projects/simple_gradle$ mkdir -p src/test/java/com/test777767
```

Create

```
steve@minty:~/projects/simple_gradle$ vim src/test/java/com/test777767/GradleTutorialTest.java
steve@minty:~/projects/simple_gradle$ cat src/test/java/com/test777767/GradleTutorialTest.java
package com.test777767ont;

import org.junit.Test;

public class GradleTutorialTest {

	@Test
	public void verifyNoExceptionThrown () {
		GradleTutorial.main(new String []{});
	}
}
```

NOTE: org.junit doesn't come automatically; gradle has to download for us.

### Add dependency to build

```
steve@minty:~/projects/simple_gradle$ vim build.gradle 
steve@minty:~/projects/simple_gradle$ cat build.gradle 
plugins {
	id 'java'
}

jar {
	manifest {
		attributes 'Main-Class': 'com.test777767ont.GradleTutorial'
	}
}

repositories {
        mavenCentral()
}

dependencies {
	testImplementation group: 'junit', name: 'junit', version: '4.13.2'
}

```

### Re-run build

```
steve@minty:~/projects/simple_gradle$ ./gradlew build

BUILD SUCCESSFUL in 1s
4 actionable tasks: 2 executed, 2 up-to-date
```

### View the report:

```
steve@minty:~/projects/simple_gradle$ firefox build/reports/tests/test/index.html
```


