# PIPELINES

## Pipeline and continuous flow

The main requirement of Continuous Delivery is to set a "flow" that runs the whole process, starting from the SCM commit and going through building and testing, all the way until deployment.

The Pipeline builds and tests new code with the code that is already in SCM. One Pipeline can build the code for:

- Various platforms (such as JVM 8, JVM 11, and JVM 13)
- Different operating systems (such as Linux, macOS and Windows) 
- Different mobile operating systems (iOS and Android).

When the code passes all tests, it is ready to be deployed to production.

## Jenkins vocabulary

- **Controller:** (previously called "master") is a computer, VM or container where Jenkins is installed and run. It serves requests and handles build tasks.
- **Agent:** (previously called "slave") is a computer, VM or container that connects to a Jenkins controller. It executes the tasks requested by the controller.
- **Node:** is sometimes used to refer to the computer, VM or container used for the controller or agent. Be careful because "Node" has another meaning for Scripted Pipeline.
- **Executor:** is a computational resource for running builds. It performs operations and can run on any controller or agent, although running builds on controllers is not recommended.

## Project types

Jenkins provides three different project types that can define your continuous project:

- [Freestyle Projects](freestyle_project.md)
- [Pipeline Projects](pipeline_project.md)
    - Declarative Pipeline
    - Scripted Pipeline
- Multibranch Pipeline

| Freestyle | Pipeline | Multibranch Pipeline |
| --------- | -------- | -------------------- |
| Simple | **Whole delivery cycle** | Same as Pipeline |
| **Single tasks** | Single branch | **Multiple branches** |
| e.g. run tests | e.g. test->build -> ... | e.g. CI/CD for main, sandbox ... |

[***Next***](../chapter-two/README.md)