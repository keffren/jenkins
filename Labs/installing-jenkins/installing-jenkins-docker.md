# Install Jenkins as Container

## Benefits

- **Faster setup and deployment:**
    - Saves time and effort compared to traditional installation methods.
- **Consistency across environments:** 
    - Docker ensures Jenkins environment is identical across development, testing, and production stages. The container image bundles all the necessary dependencies (operating system, libraries, configurations) into a single unit.
- **Improved Scalability:**  
    - Docker makes scaling Jenkins instances up or down much simpler. We can easily spin up new containers to handle increased workloads and terminate them when not needed.

## Cons

- **Data Persistence:** 
    - By default, Docker containers are ephemeral, meaning data created within them is lost when the container stops. This can be problematic for Jenkins.
    - Attach the container to a named volumes o bind mount
- **Conflicting Docker Installations:**
    - If Jenkins image includes its own Docker installation, it might **conflict with the Docker daemon** on the host machine. This can lead to unexpected behavior or errors.

## How can we deploy Jenkins on Docker?

### For a simple use of Jenkins without the need to use Docker.

```
docker run --name my-jenkins-demo -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home --restart=on-failure jenkins/jenkins:lts
```

### Jenkins as Docker-Docker

I recommend read [Running Jenkins on Docker](https://medium.com/gdgsrilanka/running-jenkins-on-docker-for-a-newbie-855ad376500b)

Also, I recommend to may use [Sysbox](https://github.com/nestybox/sysbox) (*open-source and free container runtime*)for deploy Jenkins as container.

## How Can we retrieve the installation hash to set up Jenkins?

During the installation, jenkins has created an admin. That it stored at `/var/jenkins_home/secrets/initialAdminPassword`

There are two ways to retrieve the password generated to continue with jenkins environment installation:

1. Get it from the logs:
	- `docker logs my-jenkins-demo`
		b14a70da4af142418ed163448550bf34

		```
		*************************************************************
		*************************************************************
		*************************************************************

		Jenkins initial setup is required. An admin user has been created and a password generated.
		Please use the following password to proceed to installation:

		b14a70da4af142418ed163448550bf34

		This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

		*************************************************************
		*************************************************************
		*************************************************************
		```
1. Get it through the container:
	- `docker exec my-jenkins-demo cat /var/jenkins_home/secrets/initialAdminPassword`

## How Can I access to Jenkins?

I have deployed jenkins using docker at my local network. So the entrypoint is : `http://127.0.0.1:8080/`