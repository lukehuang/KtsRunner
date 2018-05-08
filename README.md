# KtsRunner
[![Build Status](https://travis-ci.org/s1monw1/KtsRunner.svg?branch=master)](https://travis-ci.org/s1monw1/KtsRunner)
___
**KtsRunner** is a light-weight tool that allows the execution of `.kts (Kotlin Script) files from ordinary Kotlin programs.
It's enabled by [JSR 223](https://www.jcp.org/en/jsr/detail?id=223) (Java Scripting Engines API).

## Usage

### Running a script from file system

A simple usage example for KtsRunner can be described as follows:
The declaration of a class is placed in a `.kts file, which is supposed to be loaded into a normal Kotlin program so that it
can be processed further.

1. The example class
```kotlin
data class ClassFromScript(val x: String)
```

2. The `.kts` file
```kotlin
import de.swirtz.ktsobjectloader.ClassFromScript

ClassFromScript("I was created in kts")
```

3. The code to load the class

```kotlin
val scriptReader = Files.newBufferedReader(Paths.get("path/classDeclaration.kts"))
val loadedObj: ClassFromScript = KtsObjectLoader().load<ClassFromScript>(scriptReader)
println(loadedObj.x)
// >> I was created in kts
```

As shown, the `KtsObjectLoader` class can be used for executing a `.kts` script and return its result. The example shows a script that creates an instance of the `ClassFromScript` type that is loaded via ``KtsObjectLoader`` and then processed in the regular program.

### Executing scripts directly

The `KtsObjectLoader` also allows the evaluation of simple `String` based scripts:

```kotlin
val scriptContent = "5 + 10"
val fromScript: Int = KtsObjectLoader().load<Int>(scriptContent))
println(fromScript)
// >> 15
```


## Getting Started

In your Gradle build, simply include the following repository and dependency:

```kotlin
maven { 
    setUrl("https://dl.bintray.com/s1m0nw1/KtsRunner")
}

compile("de.swirtz:ktsrunner:0.0.x")

```

