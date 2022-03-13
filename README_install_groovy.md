# 

## yah, I give up....

gonna install SDKMAN!

```
$ curl -s get.sdkman.io | bash
Follow the instructions on-screen to complete installation.

Open a new terminal or type the command:

$ source "$HOME/.sdkman/bin/sdkman-init.sh"
Then install the latest stable Groovy:

$ sdk install groovy
After installation is complete and you’ve made it your default version, test it with:

$ groovy --version


```


## test

```
steve@minty:~/projects/simple_gradle$ ./simple_goove.groovy 
hello

steve@minty:~/projects/simple_gradle$ cat ./simple_goove.groovy
#!/usr/bin/env groovy
println "hello" 
```

## before 

```
steve@minty:~/projects/simple_gradle$ groovy --version
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Groovy Version: 2.4.17 JVM: 11.0.13 Vendor: Ubuntu OS: Linux
```

## after

```
steve@minty:~/projects/simple_gradle$ groovy --version
Groovy Version: 4.0.1 JVM: 17.0.2 Vendor: Private Build OS: Linux
```


