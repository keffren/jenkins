# OPERATE PIPELINE

## How to change Home Directory?

### Jenkins home directory
It is used as central location where Jenkins **stores** all its configuration, settings, plugins, jobs, builds logs, etc.

1. Create a new folder which will be the new home dir
1. Copy all data from old/default home to the new one
1. Create an ENV VAR `JENKINS_HOME` and set it as global
    - Windows (PowerShell):
    ```
    Set-Variable -Name JENKINS_HOME -Value <new_home_path> -Scope Global
    ```
    - Linux
    ```
    export JENKINS_HOME=<new_home_path>
    ```
1. Restart Jenkins

## How to use Jenkins CLI?

- Navigate onto `Manage Jenkins > Configure Global Security`
    - Make sure that the `Enable security` checkbox is checked
- Go to `jenkins_url/cli/`
    - Download `jenkins-cli.jar` and place it at any location
- Open a terminal and within `jenkins-cli.jar` path, paste the nex command:
    ```
    java -jar jenkins-cli.jar -s jenkins_url:8080 help 
    ```
    - You will prompted for provide the passphrase which should be configure in **SSH Public Keys** within user configuration

## Rerun

Jenkins enables us to rerun a pipeline. The `Replay` feature allows for quick modifications and execution of an existing Pipeline without changing the Pipeline configuration or creating a new commit.

Rerunning a pipeline in Jenkins is possible by following the outlined steps:

1. Navigate onto `Jenkins > Pipeline > Branch`
1. Select a previously completed run in the build history (bottom left)
1. Click `Replay` in the left menu

## Restart from Stage

It's like Replay, but you click `Restart from Stage` instead

## How Jenkins tracks the changes from source code ?

There are two ways for Jenkins to be notified of a code change:

- **Push** notification
    - The Source Code Management notifies jenkins on new commits.
    - It needs to install and configure a WebHook
        - To install a WebHook on Jenkins navigate onto `System Configuration > Manage Jenkins`
    - It is more common and efficient
- **Poll**
    - Jenkins polls in regular intervals.

> [!TIP]
> A good strategy to get a high pipeline reliability is Configure both as a backup. Increase the poll interval to 1-2 hours
