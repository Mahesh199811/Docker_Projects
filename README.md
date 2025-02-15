# Project-1

## Establish Secure Connection between two  Ubuntu Containers using SSH

![Screenshot_2025-02-16-00-40-11-24_f9ee0578fe1cc94de7482bd41accb329](https://github.com/user-attachments/assets/552e8066-6b35-4954-8420-d64f9711a98c)

### Step 1: Run Docker Image
```bash
docker pull ubuntu
docker image
```
- `docker pull ubuntu`: This command pulls the latest Ubuntu image from the Docker Hub repository. It ensures you have the most recent version of the Ubuntu container.
- `docker image`: Lists all the Docker images available on your local machine. This is used to verify that the Ubuntu image has been successfully downloaded.

### Step 2: Create New Directory
```bash
mkdir Docker-Projects
cd Docker-Projects
docker run -it --name container1 ubuntu
```
- `mkdir Docker-Projects`: Creates a new directory named `Docker-Projects` where you can organize project-related files.
- `cd Docker-Projects`: Changes the current directory to `Docker-Projects`.
- `docker run -it --name container1 ubuntu`: Runs a new container from the Ubuntu image with interactive terminals (`-it`) and names it `container1`.

### Step 3: Configure SSH
```bash
apt-get update
apt-get install openssh-server
apt-get install nano
nano /etc/ssh/sshd_config
```
- `apt-get update`: Updates the package lists for upgrades for packages that need upgrading, as well as new packages that have just come to the repositories.
- `apt-get install openssh-server`: Installs the OpenSSH server which allows secure remote connections.
- `apt-get install nano`: Installs Nano, a simple text editor used for editing configuration files.
- `nano /etc/ssh/sshd_config`: Opens the SSH configuration file for editing. Here, you would uncomment and modify certain lines, such as enabling root login (`PermitRootLogin yes`).

### Step 4: Create 2nd Container
```bash
docker run -it --name container2 ubuntu
apt-get update
apt-get install openssh-client
```
- `docker run -it --name container2 ubuntu`: Similar to the first container, this command runs another new container named `container2`.
- `apt-get install openssh-client`: Installs the SSH client in `container2`, which will be used to connect to `container1`.

### Step 5: Starting the Container 1
```bash
docker exec -it container1 bash
docker start container1
docker exec -it container1 bash
cat /etc/shadow | grep root
passwd root
```
- `docker exec -it container1 bash`: Executes an interactive bash shell inside `container1`.
- `docker start container1`: Ensures that `container1` is running.
- `cat /etc/shadow | grep root`: Checks the root entry in the shadow file to ensure the root has a password set.
- `passwd root`: Sets or changes the password for the root user in `container1`.

### Step 6: Get IP Address of Container 1
```bash
docker inspect container1 | grep IPAddress
docker exec -it container2 bash
docker start container2
docker exec -it container2 bash
ssh root@<IPAddress>
```
- `docker inspect container1 | grep IPAddress`: Retrieves the IP address of `container1`.
- `docker exec -it container2 bash` and `docker start container2`: Similar to step 5, ensures `container2` is running and you have a bash shell open.
- `ssh root@<IPAddress>`: Connects to `container1` from `container2` using SSH.

### Step 7: Check whether the container 1 is running or not
```bash
docker exec -it container1 bash
service --status-all
service ssh start
```
- `service --status-all`: Lists all services and their status in `container1`.
- `service ssh start`: Starts the SSH service if it's not already running.

### Step 8: Successfully connected 2 Ubuntu containers using SSH
- At this point, you have successfully established an SSH connection from `container2` to `container1`. This setup allows for secure command execution and data transfer between containers.

This detailed breakdown explains the purpose and function of each command used in setting up SSH connections between Docker containers running Ubuntu.

