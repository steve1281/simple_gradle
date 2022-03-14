# Clone the repo

Problem is that `build.gradle` has customized script in it. But, if build.gradle is already there, you can't do a `gradle init`.

You could:

* init before you pull.  This would require me to create the local files and then clone over top of it. No thanks.
* commit all the gradle files.  This is ok, I guess, but its more baggage than I would like.
* move the blocking files, init, and then move them back.  Manual, but doable.

## clone

```
  $ git clone git@github.com:steve1281/simple_gradle.git
  $ cd simple_gradle
```

## fixing

```
  $ mv build.gradle build.gradle_backup
  $ mv settings.gradle settings.gradle_backup
  $ gradle init
  $ mv build.gradle_backup build.gradle
  $ mv settings.gradle_backup settings.gradle
  $ ./gradlew build
  $ java -jar build/libs/gradle-tutorial.jar
```


