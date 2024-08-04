# java-maven-testcontainers-sfn-example

An [SSCCE](http://www.sscce.org/) of using [LocalStack](https://www.localstack.cloud/) via [TestContainers](https://testcontainers.com/) to test a simple [AWS](https://aws.amazon.com/) [Step Function](https://aws.amazon.com/step-functions/) in a [Java](https://en.wikipedia.org/wiki/Java_%28programming_language%29) project with [maven](https://maven.apache.org/) build and [JUnit 5 Jupyter](https://junit.org/junit5/docs/current/user-guide/) test framework.

## Building

The build is fully integrated with maven and may be run using simply:

    mvn clean compile test verify

This will build the main code as well as run unit tests via [surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) and integration tests via [failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/).

## Reusing

The code is intended to be modular and reused. While I hope all the code is useful, I suspect the following code may be of particular interest:

* [`src/main/java/io.aleph0.example.testcontainers.sfn.ActivityManager`](https://github.com/aleph0io/java-maven-testcontainers-sfn-example/blob/main/src/main/java/io/aleph0/example/testcontainers/sfn/ActivityManager.java) -- A `Runnable` that polls for [activity tasks](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-activities.html). Runs in a standalone thread, either manually or via an `Executor`. Responds to thread interrupt.
* [`src/main/java/io.aleph0.example.testcontainers.sfn.util.Exceptions`](https://github.com/aleph0io/java-maven-testcontainers-sfn-example/blob/main/src/main/java/io/aleph0/example/testcontainers/sfn/util/Exceptions.java) -- Captures an `Exception` stack trace as a `String` for use in activity task error messages.
* [`src/it/java/io.aleph0.example.testcontainers.sfn.ExampleIT`](https://github.com/aleph0io/java-maven-testcontainers-sfn-example/blob/main/src/it/java/io/aleph0/example/testcontainers/sfn/ExampleIT.java) -- A self-contained integration test using TestContainers with the JUnit 5 Jupyter to create a CloudFormation stack, run the step function it creates, and then delete the CloudFormation stack.

The code is available under the Apache License v2.
