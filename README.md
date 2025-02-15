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

![alt text](<Screenshot 2025-02-16 at 1.22.55 AM.png>)

### Step 2: Create New Directory
```bash
mkdir Docker-Projects
cd Docker-Projects
docker run -it --name container1 ubuntu
```
- `mkdir Docker-Projects`: Creates a new directory named `Docker-Projects` where you can organize project-related files.
- `cd Docker-Projects`: Changes the current directory to `Docker-Projects`.
- `docker run -it --name container1 ubuntu`: Runs a new container from the Ubuntu image with interactive terminals (`-it`) and names it `container1`.

![alt text](<Screenshot 2025-02-16 at 1.36.05 AM.png>)

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

![alt text](<Screenshot 2025-02-16 at 1.42.16 AM.png>)

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

![alt text](<Screenshot 2025-02-16 at 1.54.03 AM.png>)

### Step 7: Check whether the container 1 is running or not
```bash
docker exec -it container1 bash
service --status-all
service ssh start
```
- `service --status-all`: Lists all services and their status in `container1`.
- `service ssh start`: Starts the SSH service if it's not already running.

![alt text](<Screenshot 2025-02-16 at 1.55.59 AM.png>)

### Step 8: Successfully connected 2 Ubuntu containers using SSH
- At this point, you have successfully established an SSH connection from `container2` to `container1`. This setup allows for secure command execution and data transfer between containers.

![alt text](<Screenshot 2025-02-16 at 1.57.08 AM.png>)

# Key take away from the project 

### 1. Improve Security
- **Setting up SSH connection between two containers**: Establishing an SSH connection ensures that all communications between the two containers are secure. SSH provides a secure channel over an unsecured network, encrypting all data that passes through it.
- **Secure and encrypted connection**: SSH uses strong encryption to protect the data being transmitted. This prevents eavesdropping and man-in-the-middle attacks.
- **Ensure confidentiality, integrity, and authenticity of data transmission**: SSH ensures that the data sent is confidential (only the intended recipient can read it), has integrity (data is not altered during transmission), and is authentic (the sender is verified).
- **Protect applications and data from unauthorized access and data breaches**: By using SSH, you can significantly reduce the risk of unauthorized access to your applications and data, protecting them from potential breaches.

### 2. Ease of Management
- **Manage and deploy containers**: SSH allows administrators to remotely manage and configure containers, making it easier to deploy and update applications without direct access to each container.
- **Reduce complexity**: By using SSH, the complexity of managing multiple containers and environments is reduced, as it provides a consistent and secure way to access and administer containers.
- **Less time required**: SSH streamlines the management process, reducing the time required to perform administrative tasks and updates across multiple containers.
- **From one environment to another**: SSH facilitates the migration and management of containers across different environments, aiding in testing and deployment processes.
- **Scale your application**: With SSH, scaling applications across multiple containers and hosts becomes more manageable, allowing for dynamic adjustments to workload and resources.

### 3. Better Collaboration
- **Multiple team members can work simultaneously**: SSH allows multiple administrators or developers to securely access and work on the same container environment simultaneously, without interference.
- **Productivity increase**: Secure and efficient access to container environments via SSH enhances productivity, as team members can quickly perform tasks and resolve issues without being physically present at the server location.
- **Secure and efficient manner**: The security features of SSH ensure that collaborative efforts are not compromised, maintaining the integrity and confidentiality of the work being done.

### 4. Portability
- **Reduce risk of downtime**: By using SSH, you can quickly and securely make changes to container configurations, reducing the risk of downtime associated with manual access and configuration errors.
- **Move from different environments**: SSH facilitates the movement of containers between different environments (e.g., from development to production), ensuring that configurations are maintained and that the transition is smooth.
- **Configuration issues**: SSH helps in diagnosing and resolving configuration issues remotely, which is crucial for maintaining the health and performance of containerized applications.
- **Management process**: The ability to manage containers remotely via SSH simplifies the overall management process, making it easier to handle deployments, updates, and maintenance tasks across various environments.