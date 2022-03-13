# Notes on installing intellij on minty

Assuming you want an IDE, there are a number of choices.

This instructions for IntelliJ.

VSCODE is decent as well.


## Check that you have a current JDK

## Find latest version of IntelliJ

link: https://www.jetbrains.com/idea/download/other.html

Looks like 2021.3.2 (Released 27 Jan 2022)

## Download

```
cd /tmp
steve@minty:/tmp$ wget https://download-cdn.jetbrains.com/idea/ideaIC-2021.3.2.tar.gz
--2022-03-13 11:34:10--  https://download-cdn.jetbrains.com/idea/ideaIC-2021.3.2.tar.gz
Resolving download-cdn.jetbrains.com (download-cdn.jetbrains.com)... 65.8.56.3, 65.8.56.20, 65.8.56.34, ...
Connecting to download-cdn.jetbrains.com (download-cdn.jetbrains.com)|65.8.56.3|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 803838802 (767M) [binary/octet-stream]
Saving to: ‘ideaIC-2021.3.2.tar.gz’

ideaIC-2021.3.2.tar.gz        2%[                                            ]  16.97M  5.21MB/s    eta 2m 27s 

( 5 mins or so)

```
## Unzip

Note filename changes based on the version you downloaded.

```
steve@minty:/tmp$ tar xvf ideaIC-2021.3.2.tar.gz 
```

## copy extracted dir

```
steve@minty:/tmp$ sudo mv idea-IC-213.6777.52 /opt/idea
[sudo] password for steve: 
steve@minty:/tmp$ 
```

## First time run

```
steve@minty:/tmp$ /opt/idea/bin/idea.sh
Mar. 13, 2022 11:40:42 A.M. java.util.prefs.FileSystemPreferences$1 run
INFO: Created user preferences directory.
Mar. 13, 2022 11:40:42 A.M. java.util.prefs.FileSystemPreferences$6 run
WARNING: Prefs file removed in background /home/steve/.java/.userPrefs/prefs.xml
... launches a GUI.
... answer questions intelligently.
... I set the UI to light (eventually I well set it to Solarized Light)
... I add the VimIdea plugin.

```

## Set up idea from the command line

The idea.sh script is supposed to add an alias idea for you.

It didn't. Its free software. I suppose I _could_ go look the script.


For now:


```
steve@minty:/tmp$ alias idea=/opt/idea/bin/idea.sh
```

Add that alias to your start up.

eg)

```
steve@minty:/tmp$ ed ~/.bashrc
3954
$
[[ -s "$HOME/.sdkman/bin/sdkman-init.sh" ]] && source "$HOME/.sdkman/bin/sdkman-init.sh"
a

alias idea=/opt/idea/bin/idea.sh
.
wq
3988

```

They are moving to a toolbox/gui launching technique, so I suspect this will not get much attention.


## Open project

```
steve@minty:~/projects/simple_gradle$ idea .

(there will be a LOT of errors an warnings from intellij. Ignore them.)
```

## Run build (from intellij)

* open the file `build.gradle`
* on the far right, open Gradle panel
* open Tasks in the gradle panel
* double click the `clean` task
* observe in the Run panel at the bottom of the window that it was successful
* double click the `build` task
* observe in the Run panel it was successful.
* open `build/reports/tests/test/index.html`
* right click `build/libs/gradle-tutorial.jar` and run it
* observe correct output in the Run Panel ("Gradle 4tw!")

(should add a run task to build.gradle)


