# ws_solace_java

Solace Pub Sub Event Mesh Integration with JAVA

Integrating Solace with different types of publisher's and subscribers in JAVA

# Why Apache Solace?

- Messaging System provides Loose Coupling
- Facilitates Event Mesh across multiple Event Brokers

## Getting Started with Solace

We will be using the container version of Solace Broker for our activities.

### Practice 1.1 - Installing podman machine

1. Download the PODman software
   https://github.com/containers/podman/releases/tag/v4.7.0
2. Scroll download to locate the installer → Download the installer → Install the PODMan software for your laptop (For MAC machines instructions please browse the link https://podman.io/docs/installation)
3. Launch a terminal / command prompt
4. Change your working directory to HOME directory

````Shell
Mac``` Shell
cd $HOME
Win``` Shell
cd c:\users\userName
````

5. Initialize a VM for PODman using below command
   podman machine init
6. Start the virtual machine using below command
   podman machine start
7. Verify if the setup is successful using below command
   podman version

### Practice 1.2 - Understanding how to work with containers

1. Download the ‘oraclelinux:8-slim’ image from docker hub

```Shell
podman image pull oraclelinux:8-slim
```

2. Create a container using an image, at this moment give a task for container

```Shell
podman container create --name date-printer oraclelinux:8-slim sh -c "while true;do $(echo date);sleep 5;done;"
```

Note that :-

- Name of container is ‘date-printer’
- Name of image is oraclelinux:8-slim
- Script to be executed by container is “while true;do $(echo date);sleep 5;done;”

3. Verify if the container is created

```Shell
podman container list -a
```

Notice, the state of container is ‘Created’ 4. Start the container

```Shell
podman container start date-printer
```

5. Check the logs output of container (Output printed by the container)

```Shell
podman container logs date-printer
```

6. Execute an alternate command over a running container.

```Shell
podman container exec date-printer echo Alternate task for container
```

7. Display the files/folders in the containers root folder

```Shell
podman container exec date-printer ls /
```

8. Stop the container

```Shell
podman container stop date-printer
```

9. Remove the container

```Shell
podman container rm date-printer
```

### Practice 1.3 - Starting the Solace container on podman

1. Launch a command prompt
2. Pull the ‘Standard solace broker image’

```Shell
podman image pull solace/solace-pubsub-standard
```

3. Verify if the image is pulled using below command

```Shell
podman image ls
```

4. Ensure below ports are free on your machine
   8080, 55555, 8008, 1883, 8000, 5672, 9000, 2222
   Use the below command for checking

```Shell
netstat -ano | find ":8080"
```

5. Start the solace container using below command

```Shell
podman run -d -p 8080:8080 -p 55555:55555 -p 8008:8008 -p 1883:1883 -p 8000:8000 -p 5672:5672 -p 9000:9000 -p 2222:2222 --shm-size=2g --env username_admin_globalaccesslevel=admin --env username_admin_password=admin --name=solace solace/solace-pubsub-standard
```

- podman run -d ⇒ Start the container in detached mode (i.e. Create + Start)
- -p ⇒ Port publish (i.e. container port published on virtual machine)
- --env ⇒ Environment variable values for the container
- --name ⇒ Name given to container.
  solace/solace-pubsub-standard ⇒ Standard Solace Broker Image
