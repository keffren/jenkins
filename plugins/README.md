# Plugins

## Credentials

This plugin allows store and manage credentials in Jenkins. Hence, it centralizes them.
For more information, visit [the user guide](https://github.com/jenkinsci/credentials-plugin/blob/master/docs/user.adoc)

### Credentials Scope

- **System**
    - Only available on Jenkins Server. So it suitable for administrators.
    - It is not visible and accessible for Jenkins jobs.
- **Global**
    - It is accessible everywhere (Jenkins, nodes, pipelines and son)
- **Third Scope**
    - It's limited by the project
    - ONLY with multibranch pipeline

### Types

- Username with password (the most common)
    - ID : How we'll reference the credentials on Jenkins
- SSH Username with private key
- Secret file
- Secret text
- Certificate

> [!NOTE]
> Different plugins will provide different credentials types

## Credential Binding

Allows credentials to be **bound to environment variables** for use from miscellaneous build steps.

There are two ways to retrieve the retrieve the credentials within the pipeline:

- As environment variables

    ```
    pipeline{
        environment{
            MY_CREDENTIAL = credentials('credential_id')
        }
        ...
    }
    ```
    
- Using wrapper

    ```
    ...
    steps {
        withCredentials([usernamePassword(credentialsId: 'amazon', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            // Here use the vars
            echo "username is $USERNAME"
            echo "password is $USERNAME"
        }
    }
    ```
> [!IMPORTANT]
> The credentials must be defined, previously, in Jenkins using the GUI

## Folders 

This plugin enables to organize `jobs` through folders. Folders are nestable and you can define views within folders.
It's a good way to organize the credentials, but also it separate them: *"If there are two projects such as A and B. The project A won't have the credentials from project B"*