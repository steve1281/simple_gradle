# Installing later version of groovy

Groovy is the scripting langauge that gradle uses.  

## The default groovy is old

The groovy (YMMV) I had was out of date and was printing errors:

```
steve@minty:~/projects/simple_gradle$ groovy --version
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Groovy Version: 2.4.17 JVM: 11.0.13 Vendor: Ubuntu OS: Linux

```


## Install a package manager

For this experiment, I decided to install `SDKMAN!`.

```
$ curl -s get.sdkman.io | bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

## Install/Test groovy

```
$ sdk install groovy

$ groovy --version

steve@minty:~/projects/simple_gradle$ groovy --version
Groovy Version: 4.0.1 JVM: 17.0.2 Vendor: Private Build OS: Linux
```


## Simple test

```
steve@minty:~/projects/simple_gradle$ ./simple_goove.groovy 
hello

steve@minty:~/projects/simple_gradle$ cat ./simple_goove.groovy
#!/usr/bin/env groovy
println "hello" 
```
