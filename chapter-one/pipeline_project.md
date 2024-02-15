
# Pipeline Projects

[Jenkins Pipeline](https://www.jenkins.io/doc/book/pipeline/) is a tool for defining your Continuous Delivery/Deployment flow as code. Two syntaxes are supported:

- Scripted
    - sequential execution, using Groovy expressions for flow control
- Declarative
    - uses a framework to control execution

Some of the advantages of Pipeline over freestyle are:

- Can be restarted and pausable (human approval)
- Advanced visualisation
    - We define the flow through code and monitor the result through visualisation
- SCM friendly
    - Pipelines are defined in the plain-text **Jenkinsfile** so can be stored in the same repository as the application code and can be treated like any other code

A Pipeline is defined in a `Jenkinsfile` that uses a DSL (Domain-Specific Language) based on Apache Groovy syntax and it is stored in an SCM. 

Pipeline-as-code allows the entire team to collaborate on the continuous delivery process: from development, to QA, all the way through to operations and production.

## Jenkins Pipeline sections

The basic structure of a Declarative Pipeline is simple and straightforward:

- **It is structured in sections, called `stages`**, each of which defines a chunk of work to be done.
- **Each `stage` includes `steps`** that execute the actual programs and scripts to be run.
- An agent statement defines the node where the programs and scripts execute. You can define one agent to run the entire Pipeline or you can specify different agents for different stages.

## Declarative versus Scripted Pipeline

Declarative and Scripted Pipelines use different syntaxes, but both are defined in a `Jenkinsfile` under source code management (SCM) and both rely on the Pipeline DSL, which is based on Apache Groovy syntax.

### Scripted pipeline

- Executed serially, from top down
- Relies on Groovy expressions for flow control
    - **Requires extensive knowledge of Groovy syntax**
- Very flexible and extensible
    - Limitations are mostly Groovy limitations

Example:

```
node {
    stage('Build') {
        sh 'mvn clean install'
    }
    stage('Test') {
        sh 'mvn test'
    }
}

```

### Declarative Pipeline

The declarative pipeline syntax provides a defined set of capabilites that lets you define a pipeline **without learning Groovy**.

Using Blue Ocean simplifies the Pipeline creation process even more.

Example:

```
pipeline {
    agent { label 'linux' }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
```

## Tools for working with pipeline

Pipelines can be developed and maintained using different tools:

- Graphical Blue Ocean Visual Editor with the embedded Code Editor
- Jenkins dashboard with the inline editor that is provided
- Jenkins dashboard with a text editor and standard SCM tools

All tools result in the same Jenkinsfile that defines the Pipeline as code so the the tools can be used interchangeably on the same Pipeline.