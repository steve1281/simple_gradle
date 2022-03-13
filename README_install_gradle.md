# Notes on installing Gradle


## Verify the Java  version 

* you need java 8 or above.

* using 17, so all good:

```
steve@minty:~/projects/simple_gradle$ java -version
openjdk version "17.0.2" 2022-01-18
OpenJDK Runtime Environment (build 17.0.2+8-Ubuntu-120.04)
OpenJDK 64-Bit Server VM (build 17.0.2+8-Ubuntu-120.04, mixed mode, sharing)
```

## Installing

* https://gradle.org/install/

The site will direct you to us a package mananger (SDKMAN!).  While this is a handy tool, I choose to not.

* Remove any apt installed gradle

```
sudo apt-get remove gradle
```

* Manually installing

First note the latest version is 7.4.1  ; YMMV.

### Download

```
steve@minty:~/projects/simple_gradle$ export VERSION=7.4.1

steve@minty:~/projects/simple_gradle$ wget https://services.gradle.org/distributions/gradle-${VERSION}-bin.zip -P /tmp

--2022-03-12 08:48:10--  https://services.gradle.org/distributions/gradle-7.4.1-bin.zip
Resolving services.gradle.org (services.gradle.org)... 104.18.190.9, 104.18.191.9, 2606:4700::6812:bf09, ...
Connecting to services.gradle.org (services.gradle.org)|104.18.190.9|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://downloads.gradle-dn.com/distributions/gradle-7.4.1-bin.zip [following]
--2022-03-12 08:48:14--  https://downloads.gradle-dn.com/distributions/gradle-7.4.1-bin.zip
Resolving downloads.gradle-dn.com (downloads.gradle-dn.com)... 104.18.165.99, 104.18.164.99, 2606:4700::6812:a463, ...
Connecting to downloads.gradle-dn.com (downloads.gradle-dn.com)|104.18.165.99|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 115850061 (110M) [application/zip]
Saving to: ‘/tmp/gradle-7.4.1-bin.zip’
...


```

### Unzip 

```
sudo unzip -d /opt/gradle /tmp/gradle-${VERSION}-bin.zip
```

### Quick Check (you can skip this)

```
steve@minty:~/projects/simple_gradle$ /opt/gradle/gradle-${VERSION}/bin/gradle --version

------------------------------------------------------------
Gradle 7.4.1
------------------------------------------------------------

Build time:   2022-03-09 15:04:47 UTC
Revision:     36dc52588e09b4b72f2010bc07599e0ee0434e2e

Kotlin:       1.5.31
Groovy:       3.0.9
Ant:          Apache Ant(TM) version 1.10.11 compiled on July 10 2021
JVM:          17.0.2 (Private Build 17.0.2+8-Ubuntu-120.04)
OS:           Linux 5.4.0-91-generic amd64
```

### Set a link to it:

```
sudo ln -s /opt/gradle/gradle-${VERSION} /opt/gradle/latest
```

### Create script


```
steve@minty:~/projects/simple_gradle$ sudo ed /etc/profile.d/gradle.sh
/etc/profile.d/gradle.sh: No such file or directory
a
export GRADLE_HOME=/opt/gradle/latest
export PATH=${GRADLE_HOME}/bin:${PATH}
.
wq
77
```

### Make it executable 

```
sudo chmod +x /etc/profile.d/gradle.sh
source /etc/profile.d/gradle.sh
```

### And check:

```
steve@minty:~/projects/simple_gradle$ gradle -v

------------------------------------------------------------
Gradle 7.4.1
------------------------------------------------------------

Build time:   2022-03-09 15:04:47 UTC
Revision:     36dc52588e09b4b72f2010bc07599e0ee0434e2e

Kotlin:       1.5.31
Groovy:       3.0.9
Ant:          Apache Ant(TM) version 1.10.11 compiled on July 10 2021
JVM:          17.0.2 (Private Build 17.0.2+8-Ubuntu-120.04)
OS:           Linux 5.4.0-91-generic amd64

```


