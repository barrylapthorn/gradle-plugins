# Module support check plugin

Checks for JPMS/Jigsaw support of all `jar` dependencies and also if there is OSGi support.

Writes out a file based on extension (`md`, or `csv`) if specified as a `gradle` property.

Kotlin version of [this plugin](https://github.com/woggioni/my-gradle-plugins/blob/master/jpms-check).
Attribution [license](licenses/woggioni.md).

## Requirements

Requires Java 11 or later (possibly Java 9 or later).  And possibly gradle 6.x.

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

Typical output, e.g. markdown:

jar|OSGI|JPMS|multi-release|`module-info.class`|`Automatic-Module-Name`
:--|:--:|:--:|:-----------:|:-----------------:|:---------------------:
antlr:antlr:2.7.7|||||
co.paralleluniverse:quasar-core:0.8.2_r3||YES||YES|co.paralleluniverse.quasar.core
com.esotericsoftware:kryo:4.0.2|YES||||
com.esotericsoftware:minlog:1.3.0|YES||||
com.esotericsoftware:reflectasm:1.11.3|YES||||
com.fasterxml:classmate:1.3.4|YES|YES|||com.fasterxml.classmate
com.github.ben-manes.caffeine:caffeine:2.7.0|YES|YES|||com.github.benmanes.caffeine

### Options

* `modules-check.recursive=<true|false>`
    * check and list all sub-project dependencies 
* `modules-check.configurationName=<cfg>`
    * Default value = `default`
* `modules-check.outputFile=<path>`
    * Output file.  Attempts to output by file suffix. Defaults to csv, null = stdout.
* `modules-check.filter-osgi`
    * Only list non-OSGi jars in the results
    