# Datamill Engine

## Purpose

datamill-engine is a batch data processing service built on Java and Spring Boot. It is designed to take input files of records, validate and normalize each record, aggregate the results, persist them, and write an audit entry for every processing run. The intent is a pipeline where each run is traceable: what was processed, how many records, and with what outcome.

The data is synthetic and the project contains no proprietary code. It stands as a self-contained example of a data processing service on a standard stack, and as a reference for the ingest, validate, normalize, aggregate, persist, and audit pattern.

The objectives are three. To process record files in batches through a clear and repeatable sequence of steps. To make every run auditable, so the processing history stays visible. To keep the structure legible, so the pattern is straightforward to read and extend.

## Current state

The repository is a minimal Spring Boot application. It starts up and exposes no endpoints yet. The processing logic described in the purpose is not implemented. This README covers how to build and run the base.

## Requirements

Java 25 and Git.

Java 25 is the most recent long-term support release. The project is pinned to it in `build.gradle`, so Gradle uses Java 25 for this project regardless of any other Java version installed on the machine. Versions do not need to be managed by hand.

Gradle does not need to be installed separately. The project includes the Gradle wrapper, a script named `gradlew`, which downloads and runs the correct Gradle version.

## Operating system

The project runs on Windows, macOS, or Linux without changes. Java is cross platform and nothing here is tied to Linux. The only difference is the wrapper command. On macOS and Linux it is `./gradlew`. On Windows it is `gradlew.bat`. WSL or a Linux machine is not required.

## Installing Java

On Windows, download the Temurin 25 installer from adoptium.net and run it.

On macOS or Linux, install SDKMAN from sdkman.io, then run:

```
sdk install java 25.0.3-tem
```

If that build is not listed, run `sdk list java` and choose the most recent Temurin 25 entry.

Confirm the install with:

```
java -version
```

## Getting the project

```
git clone https://github.com/redlab-math/datamill-engine
cd datamill-engine
```

## Building and running

Build first. The first run downloads Gradle and the dependencies, so it takes a while.

On macOS or Linux:

```
./gradlew build
```

On Windows:

```
gradlew.bat build
```

Then start the application.

On macOS or Linux:

```
./gradlew bootRun
```

On Windows:

```
gradlew.bat bootRun
```

The application starts on port 8080. With no endpoints defined, a clean startup is the sign that it works. The Spring Boot startup log appears and the process keeps running until it is stopped with Ctrl and C.

## Project structure

```
datamill-engine
  build.gradle          build configuration and dependencies
  settings.gradle       project name
  gradlew, gradlew.bat  Gradle wrapper scripts
  gradle/wrapper        wrapper files
  src/main/java/com/redlab/datamill/engine/
    DatamillEngineApplication.java   the entry point
  src/main/resources
    application.properties           configuration
  src/test/java/com/redlab/datamill/engine/
    tests
```

The code lives under `src`. Inside it, `main` is the application and `test` is the code that checks it. Under `main`, the `java` folder holds the source and `resources` holds configuration. The folders under `java` mirror the package name, which in Java must match the package declared at the top of each file.

## Next steps

The repository is the base. The data processing logic will be added incrementally.
