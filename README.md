# Module support check plugin

Checks for JPMS/Jigsaw support of all dependent `jars` and also if there is OSGi support.

Writes out a file based on extension (`md`, or `csv`) if specified as a `gradle` property.

Kotlin version of [this plugin](https://github.com/woggioni/my-gradle-plugins/blob/master/jpms-check).
Attribution [license](licenses/woggioni.md).

## Requirements

Requires Java 11 or later (possibly Java 9 or later).

## Local build

Ensure your default SDK is Java 11 or higher, then:

```shell script
./gradlew check publishToMavenLocal
```

or something like this:

```shell script
 ./gradlew  -Dorg.gradle.java.home=/usr/lib/jvm/java-11-amazon-corretto/  check publishToMavenLocal
```

## Usage

If using locally, in `settings.gradle` ensure you can obtain the plugin from `mavenLocal`
i.e.

```groovy
pluginManagement {
    repositories {
        //..... other entries
        mavenLocal()
    }
}
```

Add in `build.gradle`

```groovy
plugins {
    id "net.lapthorn.plugins.modules-check" version "1.0.0"
}
```

Finally, from the CLI.

```shell script
./gradlew -Pmodules-check.outputFile=/tmp/results.md modules-check
```
