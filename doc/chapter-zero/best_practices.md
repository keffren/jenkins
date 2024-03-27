# BEST CI/CD PRACTICES

In this section, I'll cover a number of practices that will help to improve the effectiveness of the CI/CD service. 
[Source: Digital Ocean's post](https://www.digitalocean.com/community/tutorials/an-introduction-to-ci-cd-best-practices)

## Keep Pipelines Fast

CI/CD pipelines help shepherd changes through automated testing cycles, out to staging environments, and finally to production.

Each change must go through this process, keeping our pipelines **fast** and **dependable** is incredibly important. The tension between these two requirements can be difficult to balance.

There are some straightforward steps you can take to improve speed, like **scaling out** our CI/CD infrastructure and **optimizing** tests.

Consult with team members and stakeholders to align the team’s tasks about what the test suite is responsible for and what the primary areas of focus should be.

## Isolate and Secure our CI/CD Environment

From an operational security standpoint, our **CI/CD system represents some of the most critical infrastructure to protect**. Since the CI/CD system has complete access to our codebase and credentials to deploy in various environments, **it is essential to secure and insolate** it as much as possible.

Therefore **CI/CD systems should be deployed to internal, protected networks, unexposed to outside parties.**

The required isolation and security strategies will depend heavily on our network topology, infrastructure, and our management and development requirements. The important point to keep in mind is that our CI/CD systems are highly valuable targets and in many cases, they have a wide range of access to our vital systems.

## Make the CI/CD Pipeline the Only Way to Deploy to Production

A good point of using CI/CD Pipelines is that it helps **enforce best practices for testing and validates our deployment**. Promoting code through our CI/CD pipelines requires each change to demonstrate that it adheres to our organization’s standards and procedures. Failures in a CI/CD pipeline are immediately visible and highlights the errors. This mechanism that **safeguards the more important environments from untrusted code**.

To realize these advantages, however, **we need to ensure that every change to our production environment goes through our pipeline**. The CI/CD pipeline should be the only mechanism by which code enters the production environment. We can achieve this, automatically at the end of successfully testing with continuous deployment practices, or through a manual promotion of tested changes approved and made available by our CI/CD system.

So the pipeline protects the validity of our deployments regardless of whether this was a regular, planned release, or a fast fix to resolve an ongoing issue

## Maintain Parity with Production Wherever Possible

CI/CD pipelines promote changes through a series of test suites and deployment environments. Changes that pass the requirements of one stage are either automatically deployed or queued for manual deployment into more restrictive environments. **Early stages are meant to prove that it’s worthwhile to continue testing and pushing the changes closer to production.**

For later stages especially, reproducing the production environment as closely as possible in the testing environments helps ensure that the tests accurately reflect how the change would behave in production. **The more differences between our live environment and the testing environment, the less our tests will measure how the code will perform when released.**

## Build Only Once and Promote the Result Through the Pipeline

A primary goal of a CI/CD pipeline is to build confidence in our changes and minimize the chance of unexpected impact.

If our software requires a building or packaging step, that step should be executed only once and the resulting output should be reused throughout the entire pipeline (*This output is called Artifact*).

This guideline helps prevent problems that arise when software is compiled or packaged multiple times, allowing slight inconsistencies to be injected into the resulting artifacts. **Building the software separately at each new stage can mean the tests in earlier environments weren’t targeting the same software that will be deployed later, invalidating the results.**

To avoid this problem, **CI systems should include a build process as the first step in the pipeline that creates and packages the software in a clean environment**. The resulting artifact should be versioned and uploaded to an artifact storage system to be pulled down by subsequent stages of the pipeline, ensuring that the build does not change as it progresses through the system.

## Run our Fastest Tests Early

While keeping our entire pipeline fast is a great general goal, parts of our test suite will inevitably be faster than others. Because the CI/CD system serves as a pipe for all changes entering our system, **discovering failures as early as possible is important to minimize the resources devoted to problematic builds**. To achieve this, prioritize and run our fastest tests first.**Save complex, long-running tests until after you’ve validated the build with smaller, quick-running tests.**

Test prioritization usually means running our project’s unit tests first since those tend to be quick, isolated, and component focused. Afterwards, integration tests typically represent the next level of complexity and speed, followed by system-wide tests, and finally acceptance tests, which often require some level of human interaction.

## Minimize Branching in our Version Control System

One of the main principles of CI/CD is to integrate changes into the primary shared repository early and often. To take advantage of this benefit that CI provides, it is best to **limit the number and scope of branches in our repository**. Most implementations suggest that developers commit directly to the main branch or merge changes from their local branches in at least once a day.

*How can we do it? Use git methodologies like* ***GitHub Flow or Git Flow***.

## Run Tests Locally Before Committing to the CI/CD Pipeline

Related to the earlier point about discovering failures early, developers should be run some tests locally prior to committing to the shared repository. This makes it possible to detect certain problematic changes before they block other team members.

To ensure that developers can test effectively on their own, our test suite should be runnable with a single command that can be run from any environment. **The same command used by developers on their local machines should be used by the CI/CD system** to kick off tests on code merged to the repository. Often, this is coordinated by providing a **shell script** or **makefile** to automate running the testing tools in a repeatable, predictable manner.

## Run Tests in Ephemeral Environments When Possible

To help ensure that our tests run the same at various stages, it’s often a good idea to use clean, ephemeral testing environments when possible. Usually, this means **running tests in containers** to abstract differences between the host systems and to provide a standard API.

Most benefits of containers:

- Containers run with minimal state
- The portability of our testing infrastructure. With containers, developers have an easier time replicating the configuration that will be used later on in the pipeline without having to either manually set up and maintain infrastructure or sacrifice environmental fidelity.
- Containers can be spun up easily when needed and then destroyed, users can make fewer compromises with regard to the accuracy of their testing environment when running local tests. In general, using containers locks in some aspects of the runtime environment to help minimize differences between pipeline stages.

## Conclusion

- Keep Pipelines Fast
    - Keep our pipelines **fast** and **dependable** is incredibly 
- Isolate and Secure our CI/CD Environments
    - CI/CD systems should be deployed to internal, protected networks, unexposed to outside parties
- Make the CI/CD Pipeline the Only Way to Deploy to Production
    - We need to ensure that every change to our production environment goes through the pipeline
- Maintain Parity with Production Wherever Possible
    - The more differences between our live environment and the testing environment, the less our tests will measure how the code will perform when released\
- Build Only Once and Promote the Result Through the Pipeline
    - CI systems should build process as the first step in the pipeline that creates an artifact which should be versioned and uploaded to an artifact storage system to be pulled down by subsequent stages of the pipeline
-  Run our Fastest Tests Early
    - Discovering failures as early as possible is important to minimize the resources devoted to problematic builds
- Minimize Branching in our Version Control System
    - Limit the number and scope of branches in our repository
- Run Tests Locally Before Committing to the CI/CD Pipeline
    - The same command used by developers on their local machines should be used by the CI/CD system
        - Shell script or makeFile
- Run Tests in Ephemeral Environments When Possible
    - It’s often a good idea to use clean, ephemeral testing environments when possible.
        -  Containerization technology

[***Next***](../chapter-one/jenkins_intro.md)