# Use Maven on Linux Ubuntu (22.04.3)
[Tutorial link](https://github.com/heig-vd-dai-course/heig-vd-dai-course/blob/main/04-java-intellij-idea-and-maven/COURSE_MATERIAL.md)

#### Install Java

If you are using Linux (WSL excluded) or macOS, you can install and use
[SDKMAN!](https://sdkman.io/) to install and switch between different versions
of Java.

Then, install Java 17 Temurin:

```sh
# Install Java 17 Temurin
sdk install java 17.0.8-tem
```

If you are on Windows, we recommend to install Java 17 directly on your system,
without using a version manager even if you are using WSL.

Install Java 17 Temurin from the official website: <https://adoptium.net/>.

#### Check the installation

Open a terminal and type `java --version`.

The output should be similar to this:

```text
openjdk 17.0.8 2023-07-18
OpenJDK Runtime Environment Temurin-17.0.8+7 (build 17.0.8+7)
OpenJDK 64-Bit Server VM Temurin-17.0.8+7 (build 17.0.8+7, mixed mode, sharing)
```

### Download and run Maven

In this section, you will download and run Maven manually. In a future section,
you will initialize the Maven wrapper using Maven itself.

#### Download Maven

Download the latest version of Maven from the official website:
<https://maven.apache.org/download.cgi>. Download the **Binary archive**, not
the Source archive. Once downloaded, you can extract the archive.

#### Run Maven

Open a terminal and switch to the directory where you extracted the archive.

If you are using Linux (WSL excluded) or macOS, you can then run Maven with the
following command:

```sh
# Switch to the directory where you extracted the archive
cd ~/Downloads/apache-maven-*

# Run Maven
./bin/mvn --version
```

If you are using Windows, you can then run Maven with the following command:

```sh
# Switch to the directory where you extracted the archive
cd %USERPROFILE%\Downloads\apache-maven-*

# Run Maven
.\bin\mvn.cmd --version
```

The output should be similar to this:

```text
Apache Maven 3.9.4 (dfbb324ad4a7c8fb0bf182e6d91b0ae20e3d2dd9)
Maven home: /Users/ludelafo/Downloads/apache-maven-3.9.4
Java version: 17.0.8, vendor: Eclipse Adoptium, runtime: /Users/ludelafo/.sdkman/candidates/java/17.0.8-tem
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "13.5.1", arch: "x86_64", family: "mac"
```

This means that Maven is correctly running.

#### "Install" Maven by adding it to your `PATH`

If you are using Linux (WSL excluded) or macOS, use your package manager to
install Maven. This will add Maven to your `PATH` so you can use it anywhere.

If you are using Windows, you can add Maven to your `PATH` manually. You can
follow this tutorial: <https://phoenixnap.com/kb/install-maven-windows>.

> **Note**  
> I (Ludovic) am interested if one of you could improve this section with
> instructions and/or screenshots. As I am not using Windows myself, I cannot
> test it entirely.
>
> Feel free to open an issue and a pull request on GitHub if you want to help!
> Thanks!

### Install and configure IntelliJ IDEA

In this section, you will install and configure IntelliJ IDEA Ultimate Edition.

You can use another IDE if you prefer, but we have great experience with
IntelliJ IDEA.

#### Enable the IntelliJ student license

Follow the official documentation to enable the IntelliJ student license:
<https://www.jetbrains.com/community/education/#students>

#### Download and install IntelliJ Toolbox App

Go to the official website and following the instructions on how to install
IntelliJ Toolbox App on your system: <https://www.jetbrains.com/toolbox/app>.

#### Enable the student license in IntelliJ Toolbox App

Open IntelliJ Toolbox App and login with your JetBrains account.

> **Note**  
> I (Ludovic) am interested if one of you could improve this section with
> instructions and/or screenshots. I did not do it myself for a long time, maybe
> it has changed and my memory is not up to date anymore.
>
> Feel free to open an issue and a pull request on GitHub if you want to help!
> Thanks!

#### Install IntelliJ IDEA Ultimate Edition

Install IntelliJ IDEA from the Toolbox App and you should be good to go!

### Create and run a new Maven project with IntelliJ IDEA

In this section, you will create a new Maven project with IntelliJ IDEA.

#### Create the IntelliJ IDEA project

Open IntelliJ IDEA and create a new project. Fill the form as shown in the
following screenshot:

![Create the Maven project](images/practical-content-create-the-maven-project.png)

#### Run the Java project from IntelliJ IDEA

Press the "Run" button in the toolbar to run the Maven project.

The output should be `Hello World!` in the "Run" tab.

#### Initialize the Maven wrapper

Open a terminal within IntelliJ IDEA. Initialize the Maven wrapper using the
Maven binary you downloaded previously:

```sh
# Initialize the Maven wrapper
~/Downloads/apache-maven-3.9.4/bin/mvn wrapper:wrapper
```

This will create the Maven wrapper files in your project:

```text
.
├── .mvn
│   └── wrapper
│       ├── maven-wrapper.jar
│       └── maven-wrapper.properties
├── mvnw
└── mvnw.cmd
```

The `mvnw` and `mvnw.cmd` files are the Maven wrapper scripts. These files are
committed to Git.

The `maven-wrapper.jar` file is the Maven wrapper itself. This file is not
committed to Git.

The `maven-wrapper.properties` file contains the configuration of the Maven
wrapper. This file is committed to Git.

Now, instead of using the Maven binary you downloaded previously, you can use
the Maven wrapper:

```sh
# Check the Maven version
./mvnw --version
```

The output should be similar to the previous execution of Maven.

#### Update the `pom.xml` file to generate a JAR file

Maven uses the `pom.xml` file to define the **build process** of your
application.

Maven has a plugin called `maven-jar-plugin` that can be used to **generate a
JAR file** from your application.

Add the following configuration to the `pom.xml` file:

```xml
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.3.0</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>ch.heigvd.Main</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

You can find the latest version of the `maven-jar-plugin` on the Maven
Repository:
<https://mvnrepository.com/artifact/org.apache.maven.plugins/maven-jar-plugin>.

#### Package and run the project from the command line

You can now generate a JAR file using the `package` command:

```sh
# Package the application
./mvnw package
```

Maven will generate a JAR file in the `target` directory.

Run the JAR file using the `java` command:

```sh
# Run the application
java -jar target/java-intellij-idea-and-maven-1.0-SNAPSHOT.jar
```

The output should be `Hello World!`.

Congratulations! You have successfully created and run your first Maven project!

You could share this JAR file with other developers and they could run it on
their computer, without having to install IntelliJ IDEA or Maven.

#### Store the Maven configuration as IntelliJ IDEA Run/Debug configuration

Running Maven commands from the command line is not very convenient. You can
store the Maven configuration as an IntelliJ IDEA Run/Debug configuration.

This will allow you to run Maven commands from IntelliJ IDEA, without having to
open a terminal.

Other developers will also be able to run Maven commands from IntelliJ IDEA, as
the Run/Debug configurations can be committed to Git.

In the "Run" tab, click on the "Edit Configurations..." button.

Click on the "+" button and select "Maven".

Fill the form as shown in the following screenshot:

![Create the Maven Run/Debug configuration](images/practical-content-store-the-maven-configuration-as-intellij-idea-run-debug-configuration.png)

Notice the **Run** command: `dependency:resolve clean compile package`.

This will **download the dependencies**, **delete** the compiled classes,
**compile** the source code and **package** the application.

By checking the **Store as project file** checkbox, the Run/Debug configuration
will be stored in the `.idea` directory, which can be committed to Git.

Make usage of the Maven wrapper by modifying the **Maven option**.

Save the configuration and run it by pressing the "Run" button in the toolbar.

The output should be similar to the previous execution of Maven.

#### Add a dependency

Let's add the
[Logback](https://mvnrepository.com/artifact/ch.qos.logback/logback-classic)
dependency to the `pom.xml` file.

```xml
    <dependencies>
        <!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.4.11</version>
        </dependency>
    </dependencies>
```

> **Note**  
> What is the difference between a Maven dependency and a Maven plugin ? A
> plugin performs a specific task, such as compiling the source code or
> generating a JAR file. It won't be included in the JAR file generated by
> Maven. A dependency is an external library used by your application, such as
> Logback. It will be included in the JAR file generated by Maven.
>
> You can find more information about this in
> [this StackOverflow answer](https://stackoverflow.com/a/52119718)

Update the `src/main/java/ch/heigvd/Main.java` file to use Logback:

```java
package ch.heigvd;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Main {
    public static void main(String[] args) {
        Logger logger = LoggerFactory.getLogger(Main.class);

        logger.debug("Hello World!");
    }
}
```

Download the Logback dependency by running the Maven `dependency:resolve`
command:

```sh
# Download the dependencies
./mvnw dependency:resolve
```

Run the **Current file** Run/Debug configuration to execute the application
within IntelliJ IDEA.

> **Note**  
> Having trouble with IntelliJ IDEA not recognizing the `Logger` class? Try the
> following: **Right-click on the project** > **Maven** > **Reload project**.
> This will reload the Maven project and download the dependencies.

#### Build and run the project

Build the project using the Maven `package` command:

```sh
# Package the application
./mvnw package
```

Run the JAR file using the `java` command:

```sh
# Run the application
java -jar target/java-intellij-idea-and-maven-1.0-SNAPSHOT.jar
```

It does not work! The output is an error message:

```text
Exception in thread "main" java.lang.NoClassDefFoundError: org/slf4j/LoggerFactory
        at ch.heigvd.Main.main(Main.java:8)
Caused by: java.lang.ClassNotFoundException: org.slf4j.LoggerFactory
        at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:641)
        at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:188)
        at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:521)
        ... 1 more
```

Why? Because the `maven-jar-plugin` does not include the dependencies in the JAR
file by default.

Let's fix this.

#### Update the `pom.xml` file to include the dependencies in the JAR file

Update the `pom.xml` file to include the dependencies in the JAR file. You need
to replace the previous `build` section with the following:

```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.5.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>ch.heigvd.Main</mainClass>
                                </transformer>
                                <transformer implementation="org.apache.maven.plugins.shade.resource.DontIncludeResourceTransformer">
                                    <resource>MANIFEST.MF</resource>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```

This will use the `maven-shade-plugin` to include the dependencies in the JAR
file.

You can find the latest version of the `maven-shade-plugin` on the Maven
Repository:
<https://mvnrepository.com/artifact/org.apache.maven.plugins/maven-shade-plugin>.

This plugin will intervene in the `package` phase of the Maven build process. It
will execute the `shade` goal, which will transform the JAR file to include the
dependencies.

A goal is a specific command that can be executed by a plugin.

Build and run the project using the following commands:

```sh
# Download the dependencies
./mvnw dependency:resolve

# Package the application
./mvnw package

# Run the application
java -jar target/java-intellij-idea-and-maven-1.0-SNAPSHOT.jar
```

The output should now be `Hello World!` again!

You should notice the following elements:

- The `target` directory contains the
  `java-intellij-idea-and-maven-1.0-SNAPSHOT.jar` file
- A new `original-java-intellij-idea-and-maven-1.0-SNAPSHOT.jar` file was
  created
- A new `dependency-reduced-pom.xml` file was created

The `java-intellij-idea-and-maven-1.0-SNAPSHOT.jar` file is the JAR file
generated by the `maven-shade-plugin` plugin with all dependencies included.

The `original-java-intellij-idea-and-maven-1.0-SNAPSHOT.jar` file is the JAR
file generated by the `maven-shade-plugin` plugin without all dependencies
included. If you try to run the application with this JAR file, you will get the
same error as before.

The `dependency-reduced-pom.xml` file is a **reduced version** of the `pom.xml`
file, containing only the dependencies used by the application and not the
transitive dependencies.

> **Note**  
> _Why is it so complex to package an application with Java and Maven? Why do we
> need to use a plugin to include the dependencies in the JAR file?_
>
> Java can be used to develop many different types of applications, such as
> desktop applications, mobile applications, web applications, librairies, etc.
> Each type of application has its own needs and specificities. This is why
> Maven does not include the dependencies in the JAR file by default. This is
> also why we need to use a plugin to include the dependencies in the JAR file.
>
> We will not go any deeper in this topic in this course. You will learn more
> about this in other future courses. Our goal here is to give you the tools to
> develop Java applications and share them with other developers easily.

#### Initialize a local Git repository

Open a terminal within IntelliJ IDEA and initialize a local Git repository:

```sh
# Initialize a local Git repository with a branch called `main`
git init --initial-branch=main
```

#### Ignore files for Git

By default, IntelliJ IDEA did create a `.gitignore` file and a
`.idea/.gitignore` file containing the files to be ignored by Git.

If you open these files, you will notice that it contains many files and
directories that are specific to IntelliJ IDEA, but also for other IDEs and
specific configurations.

Many tools exist to generate `.gitignore` files, such as
<https://gitignore.io/>.

We consider this as **bad practice** as it makes the comprehension of the
codebase harder (_What am I really using?_). You should **only ignore files that
are specific to your project**, the tools you are using and the environment you
are working in.

Let's clean the `.gitignore` files.

Open the `.gitignore` file update the content to the following:

```sh
## IntelliJ IDEA

# General
.idea/libraries/
.idea/shelf/
.idea/compiler.xml
.idea/jarRepositories.xml
.idea/modules.xml
.idea/workspace.xml
*.iws
*.iml
*.ipr

# Editor-based HTTP Client requests
.idea/httpRequests/

# Datasource local storage ignored files
.idea/dataSources/
.idea/dataSources.local.xml

## Linux

# Temporary files
*~

## macOS

# Files created by macOS Finder
.DS_Store

## Maven
.mvn/wrapper/maven-wrapper.jar
target/

## Windows

# Windows thumbnail cache files
Thumbs.db

# Folder config file
[Dd]esktop.ini
```

Delete the `.idea/.gitignore` file.

#### Add a README

Add a `README.md` file to explain what the project is, how to build it and how
to run it.

#### Create a GitHub repository

Create a new GitHub repository as seen in a previous chapter. Do not initialize
it with a README, a license or a `.gitignore` file.

> **Warning**  
> Do not initialize the repository with a README, a license or a `.gitignore`
> file! You will add these files later.

#### Add the remote repository and push the project to GitHub

GitHub should provide you with the commands to add the remote repository and
push the project to GitHub:

```sh
# Add the remote repository
git remote add origin <URL_TO_YOUR_GITHUB_REPOSITORY>

# Add the files to the staging area
git add .

# Check that only the required files are added to the staging area
git status

# Commit the files to the local repository
git commit -m "Initial commit"

# Push the project to GitHub
git push --set-upstream origin main
```

The last command will push the `main` branch to the `origin` remote repository
and set the `main` branch as the default branch.

Open the GitHub repository in your browser and check that the files have been
pushed to GitHub.
