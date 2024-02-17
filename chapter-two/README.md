# PIPELINE CONFIGURATION

## Branches

As developer, we can can perform a job in Jenkins based on the repository branch. Therefore we can include o exclude a branch in the Pipeline stages.

How Can we do it?

1. Navigate into `Jenkins > My_Pippeline > Configuration > Branch Source`
1. Click on `Add` in Behaviours section
1. Choose `Filter by name (with regular expression)`
1. This a example: `^ main | feature.* $`

> [!WARNING]
> ONLY with **multibranch** project type

## Configure Build Tools

In order to build the application to the package, it needs some kind of build tool. Which depends on the application technology and language.

The most common build tools are:

- Java Backend:
    - The next tools for Java projects are both build automation tools used in software development to manage and build projects. They help automate the process of compiling, testing, packaging, and managing dependencies in a consistent and efficient manner. 
        - **Maven**
            - Uses XML-based configuration
        - **Gradle**
            - Uses a Groovy or Kotlin-based DSL (domain-specific language) for its build scripts
- JavaScript Frontend
    -  The next tools are package managers for JavaScript and Node.js. The choice between them often depends on the specific needs and preferences of the development team.
        - **npm**
        - **yarn**

### How Does Jenkins allows us to use these build tools?

1. Check if the build tool is already available in `Dashboard > Manage Jenkins > Tools`
    - If it is, then configure it
    - If it isn't, then install and configure it
1. Use it in the build configuration (build section of JenkinsFile)

How Can we specify the build tools in JenkinsFile?
There are two ways :

- As wrapper
    ```
    //...
    steps {
        nodejs('name_build_tool_installed'){
            sh 'npm init'
        }
    }
    //...
    ```
- As tool
    ```
    //...
    tools {
        gradle 'name_build_tool_installed'
    }
    //...
        steps {
            sh './gradlew -v'
        }
    //...
    ```
     - ONLY supported for Maven, Gradle, Ant, JDK and Git
