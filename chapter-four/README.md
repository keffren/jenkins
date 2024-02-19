# OPERATE PIPELINE

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
