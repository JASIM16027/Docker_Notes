# Docker Notes

## Operating System

https://drive.google.com/file/d/1EpvvD9CTQfaOCyBIWGYbDB_iWHbODE2R/view?usp=drive_link

### What is an operating system?
- An operating system (OS) is software that manages computer hardware resources and provides services for computer programs.
- It acts as an intermediary between the hardware and software, allowing applications to run efficiently and enabling users to interact with the computer.

- An operating system (OS) consists of two primary layers: the application layer and the kernel layer. Each layer has distinct responsibilities and interacts in specific ways to ensure the smooth functioning of the computer system.

  ![image](https://github.com/user-attachments/assets/48036c84-552a-4a2c-bd46-21955ad19be4)

  This image represents the structure and layers of a typical Linux operating system (OS). Let's break down each component:

1. **Top Icons (Ubuntu, Fedora, openSUSE, CentOS)**:
   - These are popular Linux distributions (distros), each with its own package management, configuration, and user interface tweaks.
   - **Ubuntu** (orange icon): Known for ease of use, popular among beginners and general-purpose users.
   - **Fedora** (blue icon): Known for its cutting-edge features and ties to the Red Hat ecosystem.
   - **openSUSE** (green icon): Known for its flexibility and powerful management tools, popular among developers and IT professionals.
   - **CentOS** (purple icon): Known for stability and often used in enterprise environments, closely related to Red Hat Enterprise Linux (RHEL).

2. **OS Layer**:
   - This layer represents the operating system as a whole, which manages hardware resources and provides services for applications.
   - Each distribution has its own OS layer that includes unique tools, configurations, and user interfaces but is built on the same Linux kernel.

3. **Software Layer**:
   - This layer includes the various applications or "software" running on the operating system. Each distribution can have its own set of software pre-installed or available for installation.
   - Despite differences between distributions, the applications share a common structure and work with the underlying OS and kernel.
   - **Role**: The application layer serves as the interface between the user and the operating system. It includes all the user-facing applications and utilities that perform various tasks.
   - **Components**: This layer comprises software applications like web browsers, word processors, and media players, as well as system utilities that manage files, configure settings, and monitor system performance.
   - **Functionality**: Applications in this layer rely on the underlying services provided by the kernel to perform their tasks. They request resources and services through system calls, which the kernel processes.
   - **User Interaction**: This layer is where users interact directly with the system, entering commands and receiving outputs.

4. **OS Kernel**:
   - The kernel (specifically, the Linux kernel) is the core part of the operating system, acting as a bridge between the application layer and the hardware. It handles low-level tasks such as hardware interactions, memory management, and process control.
   - All these Linux distributions share the same Linux kernel at the core, though there might be minor variations depending on the version or modifications made by each distro.
  - **Components**: The kernel includes several critical components:
    - **Process Management**: Handles the creation, scheduling, and termination of processes, ensuring efficient CPU utilization.
    - **Memory Management**: Manages the allocation and deallocation of memory space to processes, and handles paging and segmentation.
    - **Device Management**: Controls hardware devices through device drivers, ensuring that applications can interact with hardware components like printers, disk drives, and network interfaces.
    - **File System Management**: Manages data storage, retrieval, and organization on storage devices, providing a structured way to store and access files.
    - **Security and Access Control**: Enforces security policies, controls access to system resources, and ensures that only authorized processes and users can perform certain actions.
    - **Functionality**: The kernel operates in a privileged mode with full access to all hardware. It handles low-level tasks such as interrupt handling, context switching, and communication between hardware and software components.
    - **Hardware Interaction**: It directly interacts with the hardware through device drivers, translating high-level commands from applications into low-level operations that the hardware can execute.
    - 
In summary, this diagram illustrates how different Linux distributions share a common kernel but differ at the OS and software layers, providing diverse user experiences and software ecosystems.


### How is software installed on a computer?
- Software installation involves copying files from a storage medium (e.g., CD, USB drive) to the hard disk.
- The installation process sets up the necessary files and configurations for the software to be executed.

### How does the software load in RAM?
To understand how software loads into RAM, let’s break down the process with a simplified text diagram:

  - **Application Request** :  **User** initiates a request to open a software application (e.g., a web browser).
  - **Operating System (OS) Receives Request** : The **OS** receives this request and checks if the application file exists on the storage (e.g., hard drive or SSD). 

  -  **Loading the Application from Disk**  
       - The OS locates the application on the storage disk.
       - It loads the application’s **executable code** and **data** into **RAM** in small blocks (pages).
  

  -  **Allocating Memory in RAM**  
     - The OS allocates space in RAM for the application’s code, data, and runtime variables.
     - This involves dividing RAM into pages, where each part of the application is stored in a specific page.
  
  -  **Loading Shared Libraries (if needed)**  
     - Some applications rely on **shared libraries** (e.g., graphics libraries) that may already be in RAM. 
     - If the libraries are not in RAM, they are loaded from disk into RAM and linked to the application.
    
  -  **Setting Up Process Control Block (PCB)**  
     - The OS creates a **Process Control Block (PCB)** to keep track of the application’s state, including its memory locations, priority, and resources.
     - The PCB is stored in RAM for quick access by the CPU scheduler.
     - 
  -  **CPU Accesses RAM and Starts Execution**  
     - The OS schedules the application to run, and the **CPU** begins fetching the application code from RAM.
     - The **CPU** reads instructions from the RAM, executes them, and loads additional parts of the application from the disk if needed (paging).

    ```
    User Action --> Application Request --> OS File System Check --> Disk Access --> Load Application Code to RAM 
    --> Allocate Pages in RAM --> Load Shared Libraries (if needed) --> Create Process Control Block (PCB) 
    --> CPU Accesses RAM --> Start Execution
    ```
  - When an application loads, the OS reads the program from storage, allocates memory in RAM, loads necessary libraries, and tracks the process through a PCB. The CPU then accesses RAM to execute the application, fetching and processing each instruction as needed.


### 32-bit and 64-bit Computers
- **32-bit:** Processes data in 32-bit chunks, limited to 4 GB of RAM.
- **64-bit:** Processes data in 64-bit chunks, capable of handling more RAM, improving performance for larger applications.

## Processor

### Register Set
- A small amount of very fast memory within the CPU.
- Holds data that the CPU is currently working on or needs frequently.
- Examples: AX, BX, CX registers.

### Pointing Register
- A register that holds memory addresses.
- Used to point to specific locations in memory for data retrieval or storage.

### Arithmetic and Logical Operations
- Processors support operations like AND, OR, NOT, ADD, SUB, MUL, and DIV.

## Process (Virtual Computer)

![image](https://github.com/JASIM16027/Docker_Notes/assets/39296494/f6e26763-5def-4583-9aae-8a6e8e8cffb2)

![image](https://github.com/JASIM16027/Docker_Notes/assets/39296494/5f9559f1-483d-47a5-b633-c06c36de9b1c)


### Process State
- A process is an instance of a running program.
- States include running, waiting, or terminated.

### Process ID (PID)
- Unique identifier assigned by the OS to each process.

### Attributes of a Process
- Attributes include total read/write operations, priority level, and other characteristics.

### Context Switching
- The process of saving and restoring the state of a process, allowing the CPU to switch between processes.
- 

### Process Control Block (PCB)
- A data structure maintained by the OS for each process.
- Contains information like current state, CPU registers, memory allocation, and more.

### Concurrency
- The ability of multiple processes or threads to execute in overlapping time intervals, giving the illusion of simultaneous execution.

### Multi-threaded/Core Processor
- A CPU with multiple cores, allowing it to execute multiple threads simultaneously for improved performance.

### Logical CPU or Processor
- The virtual representation of a CPU core, allowing systems with hyper-threading or multi-threading technology to divide each physical core into multiple logical CPUs.

### Parallel Execution
- Simultaneous execution of multiple tasks or processes on different processors or cores, enhancing performance and efficiency.

### Thread or Virtual Process
- A unit of execution within a process, sharing the same memory space for concurrent execution.
- Threads also undergo context switching.

- ``` When the computer starts, the operating system's code is executed, and the processor only knows the operating system. ```


## Docker
When you install docker on your machine. the file structure will be like this:
![image](https://github.com/user-attachments/assets/0c00969e-cb07-4403-8e05-0790f18f6fa6)


### Before Docker - Hypervisor
- Hypervisors create and manage virtual machines (VMs) that emulate entire computer systems, running full operating systems and requiring dedicated resources.

### Hypervisor vs Docker
- Hypervisors virtualize hardware to run multiple VMs on a single machine.
- Docker virtualizes the OS, allowing containers to share the host OS kernel, making them more lightweight.

### Why do we need Docker?
- Docker provides lightweight, isolated containers with faster startup times, using fewer resources, and allowing efficient packaging and deployment of applications.

### What is Docker? All parts of the Docker ecosystem.
- Docker is a platform for creating and managing containers.
- Components: Docker client (CLI), Docker server (daemon), Docker machine, Docker images, Docker Hub, Docker Compose.

### Workflow of Docker: "docker run -it <some-image>" - explained
1. Execute `docker run -it <some-image>` in the terminal.
2. Docker CLI validates and sends the command to the Docker server.
3. Docker server pulls the image from Docker Hub if not available locally.
4. Docker server creates a container based on the image.
5. The `-it` option makes the container run in interactive mode, providing a shell prompt for interaction.
6. User interacts with the container via the command prompt.

### Docker Image and its parts
- A Docker image is a snapshot of a file system containing software, dependencies, and configurations.
- Consists of a file system snapshot and a startup command.

### "username@machineName:/$" - explained
- The command prompt inside the Docker container:
  - `username`: User within the container.
  - `machineName`: Container's virtual machine or host system name.
  - `/$`: Current working directory inside the container.

### Kernel, Namespacing, and Control Groups
- **Kernel:** Core of the OS interacting with hardware and providing essential services.
- **Namespacing:** Linux kernel feature for resource isolation and process-level virtualization.
- **Control Groups (cgroups):** Kernel feature managing and limiting resources available to processes within a container.

### What is a Container? (Virtual Computer)
- A lightweight, isolated runtime environment encapsulating an application and its dependencies.
- Shares the host OS kernel but has its own isolated file system and resources.

![image](https://github.com/user-attachments/assets/1f2e8eb3-d7bd-4c41-85c6-268b131abd28)



When comparing Docker containers to virtual machines (VMs), it's essential to understand their fundamental differences, use cases, and advantages.

### Docker Containers

**Overview:**
- Docker is a platform that uses OS-level virtualization to deliver software in packages called containers.
- Containers share the host system's kernel but run in isolated user spaces.

**Advantages:**
1. **Lightweight:** Containers are more lightweight than VMs because they share the host OS kernel, resulting in less overhead.
2. **Performance:** Since they don't need a full OS to boot, containers can start up and shut down much faster than VMs.
3. **Portability:** Containers encapsulate all dependencies and configurations, making them highly portable across different environments.
4. **Resource Efficiency:** Containers use resources more efficiently due to shared OS components and reduced overhead.

**Use Cases:**
- Microservices architecture
- Continuous integration/continuous deployment (CI/CD) pipelines
- Running multiple applications on a single OS instance
- Development and testing environments


#### Background: Virtualization Before Docker

![image](https://github.com/user-attachments/assets/a72334df-5f17-441f-a16b-5cc91a2c58fe)


**Hypervisors:**
- Hypervisors are software, firmware, or hardware that create and manage virtual machines (VMs).
- They allow multiple VMs to run on a single physical machine by virtualizing the underlying hardware.
- Each VM runs a full operating system and requires dedicated resources, such as CPU, memory, and storage.

**Limitations of Hypervisors:**
- VMs are resource-intensive since each VM requires its own OS.
- VMs have longer startup times due to the need to boot an entire OS.
- Managing and maintaining multiple VMs can be complex and inefficient.




### Virtual Machines (VMs)

![image](https://github.com/user-attachments/assets/5c6f9b7c-a2d1-4f72-b406-e308114dea46)


- Higher Utilization of underlying resources
- Virtual machine also consume higher disk space(such as GB)
- Take long time to boot compare to docker container
- complete isolation

**Overview:**
- VMs run on a hypervisor, which is a software layer that allows multiple operating systems to share a single hardware host.
- Each VM includes a full operating system and emulated hardware.

**Advantages:**
1. **Isolation:** VMs offer complete isolation since each VM runs a full OS. This makes them suitable for running multiple, different OS environments on the same physical hardware.
2. **Compatibility:** VMs can run any operating system that the hypervisor supports, making them more versatile for running different OSes.
3. **Security:** The full isolation provided by VMs can be beneficial for security-sensitive applications.

**Use Cases:**
- Running multiple OS instances on a single hardware system
- Legacy application support
- Use cases requiring strong isolation between applications
- Testing and development across different OS environments

### Key Differences

1. **Boot Time:**
   - **Containers:** Seconds
   - **VMs:** Minutes

2. **Resource Utilization:**
   - **Containers:** More efficient, share the host OS kernel
   - **VMs:** Less efficient, each VM requires a full OS

3. **Isolation:**
   - **Containers:** Process-level isolation
   - **VMs:** Full OS-level isolation

4. **Portability:**
   - **Containers:** Highly portable, suitable for microservices
   - **VMs:** Less portable, more suited for running different OSes

### Choosing Between Docker and VMs

- **Use Docker if:**
  - You need a lightweight, fast, and portable solution.
  - Your applications are designed as microservices.
  - You require efficient use of system resources.
  - You need a streamlined development and deployment pipeline.

- **Use VMs if:**
  - You need strong isolation between applications.
  - You need to run different operating systems on the same hardware.
  - Your application requires a full OS environment.
  - You are dealing with legacy systems or applications.

In summary, Docker containers are optimal for scenarios where resource efficiency, fast deployment, and application portability are critical. In contrast, VMs are more suitable for situations requiring complete isolation and the ability to run different operating systems on the same hardware.



### **Why Do We Need Docker?**

#### Docker: A Solution to Traditional Virtualization Limitations
![image](https://github.com/user-attachments/assets/04c81395-89f8-438f-bfc9-604259d6008c)

Docker makes it really easy to install and run software without worrying about setup or dependencies.

- **Lightweight:** Docker containers share the host OS kernel, reducing the overhead associated with running multiple OS instances.
- **Isolated:** Containers provide process and filesystem isolation, ensuring applications run in their own environments.
- **Fast Startup Times:** Containers can start almost instantly because they don't require booting a full OS.
- **Efficient Resource Usage:** Containers use fewer resources compared to VMs, as they share the host OS kernel and other resources.


### Components of the Docker Ecosystem

![image](https://github.com/user-attachments/assets/576d93dc-228b-4834-bf43-6fbacb0409aa)


![image](https://github.com/user-attachments/assets/b2f948e2-f40f-4b8e-b30b-37c3e025d6ce)



1. **Docker Client:**
   - The Docker client is a command-line interface (CLI) tool used to interact with the Docker daemon.
   - Commands issued through the CLI (e.g., `docker run`, `docker build`) are sent to the Docker daemon for execution.

2. **Docker Server (Docker Daemon):**
   - The Docker daemon (`dockerd`) runs on the host machine and manages Docker objects such as images, containers, networks, and volumes.
   - It listens for Docker API requests and handles the creation, execution, and monitoring of containers.

3. **Docker Machine:**
   - Docker Machine is a tool that simplifies the setup of Docker on virtual machines or physical hosts.
   - It automates the provisioning and configuration of Docker hosts, making it easier to manage Docker environments across different platforms.

4. **Docker Images:**
   - Docker images are read-only templates that contain the application code, runtime, libraries, and dependencies required to run an application.
   - Images are built from Dockerfiles, which specify the instructions needed to create the image.
   - They are used to instantiate Docker containers.

5. **Docker Hub:**
   - Docker Hub is a cloud-based registry service for sharing and accessing Docker images.
   - It allows users to publish their own images, browse existing images, and download images for use in their own environments.

6. **Docker Compose:**
   - Docker Compose is a tool for defining and running multi-container Docker applications.
   - Using a YAML file (`docker-compose.yml`), you can specify the services, networks, and volumes needed for an application.
   - It simplifies the management of applications that require multiple containers working together.

### Step-by-Step Explanation of Docker's Functionality


1. **Building an Image:**
   - Create a `Dockerfile` with instructions on how to build your application image.
   - Use the command `docker build -t <image_name> .` to build the image from the Dockerfile.

2. **Running a Container:**
   - Use the command `docker run -d --name <container_name> <image_name>` to run a container from an image.
   - The `-d` flag runs the container in detached mode, allowing it to run in the background.

3. **Managing Containers:**
   - Use `docker ps` to list running containers.
   - Use `docker stop <container_name>` to stop a running container.
   - Use `docker rm <container_name>` to remove a stopped container.

4. **Using Docker Compose:**
   - Create a `docker-compose.yml` file to define your multi-container application.
   - Use the command `docker-compose up -d` to start the application with all defined services.
   - Use `docker-compose down` to stop and remove the application’s containers, networks, and volumes.

This diagram illustrates how Docker works when you run the command `docker run hello-world`. It visually explains the relationship between your local machine (computer) and Docker Hub.

### Explanation:

This diagram helps visualize the connection between your machine and Docker Hub when using Docker to manage containers.

![image](https://github.com/user-attachments/assets/71d9e9ce-09d5-485f-afef-1fabd2a4eceb)


1. **docker run hello-world**: 
   - This is a Docker command that tells Docker to run the "hello-world" container.

2. **Your Computer**: 
   - **Docker Client**: This is the command-line interface (CLI) tool that you use to interact with Docker. It receives the `docker run hello-world` command.
   - **Docker Server**: Also known as Docker Daemon, it manages Docker containers and handles images. The Docker Client communicates with the Docker Server to manage containers.
   - **Image Cache**: Docker keeps a cache of images it has already downloaded. If the "hello-world" image is already cached on your computer, Docker Server will use it directly without downloading it again.
   - **hello-world Container**: If the image is not cached locally, Docker will pull it from Docker Hub and create a running container from the image.

3. **Docker Hub**:
   - **hello-world, redis, busybox, Other Images**: Docker Hub is a cloud-based repository where Docker images are stored. The "hello-world" image is just one of many pre-built images (such as Redis, BusyBox, or custom ones). When you run `docker run hello-world`, Docker checks Docker Hub for the image if it's not found locally.
   - **Single file with everything needed to run one specific program**: Each Docker image on Docker Hub is a self-contained file that includes everything needed to run a program, including code, libraries, and dependencies.

### Workflow:
1. You run the `docker run hello-world` command on your computer.
2. Docker Client sends the command to the Docker Server.
3. The Docker Server checks whether the "hello-world" image is cached locally. If not, it pulls it from Docker Hub.
4. Docker creates a container from the image and runs it.

## How running Processes on your computer communication with hardware resources

![image](https://github.com/user-attachments/assets/4ca90484-1d49-4ce6-ad97-be47569b4a14)

This diagram illustrates how processes on your computer interact with hardware components via the **kernel** using **system calls**.

1. **Processes running on your computer**:
   - These are the programs that are actively running on your system, such as:
     - **Chrome**: A web browser.
     - **Terminal**: A command-line interface.
     - **Spotify**: A music streaming app.
     - **NodeJS**: A runtime environment for executing JavaScript.
   - Each of these applications operates as a separate process on your computer.
 
2. **System Calls**:
   - A **system call** is a mechanisms how a running program asks/request the operating system’s kernel for a service. These services typically involve access to hardware components like the CPU, memory, or disk.
   - Examples of system calls:
     - Reading from a file.
     - Allocating memory.
     - Accessing the network.
   - In this diagram, each of the processes (like Chrome or Spotify) makes system calls to the kernel to interact with the hardware.

3. **Kernel**:
   - The **kernel** is the core part of the operating system that manages the system's resources(RAM,CPU)  and hardware(Hard Disk / SSD,GPU,NIC) . It acts as an intermediary between running programs and the underlying hardware.
   - The kernel ensures that programs can access resources like CPU, memory, or the hard disk securely and efficiently.

4. **Hardware Components**:
   - The kernel controls access to the key hardware components:
     - **CPU**: The central processing unit, which executes the instructions of programs.
     - **Memory**: RAM (random-access memory), where active programs store data they are using.
     - **Hard Disk**: Long-term storage for files and data.

### Workflow:

- Each running process (Chrome, Terminal, etc.) makes system calls to ask/request the kernel to communicate/interact with the hardware
- The **kernel** interprets these requests and interacts with the necessary hardware components (CPU, Memory, Hard Disk) on behalf of the process.

In summary, this diagram represents how running programs communicate with your computer’s hardware through the kernel using system calls, ensuring that hardware resources are managed efficiently and securely.

##  How the operating system kernel interacts with software applications and handles system calls, particularly when applications have dependencies on different versions ?

![image](https://github.com/user-attachments/assets/56f72a60-0350-4259-a393-084f2cf08cae)

![image](https://github.com/user-attachments/assets/1fc4aaef-7a22-44dd-948d-27fa558962b2)


The diagram illustrates how the operating system'S kernel interacts with software applications and handles system calls, particularly when applications have dependencies on different versions of Python. Here's a breakdown:

### 1. **Applications (Chrome and NodeJS)**:
   - **Chrome**: Requires **Python v2** to properly working or functioning.
   - **NodeJS**: Requires **Python v3** to properly working or functioning.
   - These applications are placed at the top layer, showing that they rely on system calls to communicate with the operating system.

### 2. **System Calls**:
   - Both applications (Chrome and NodeJS) communicate with the operating system's kernel via **System Calls**. System calls are mechanisms that allow programs to request services from the kernel, like accessing hardware resources or managing files.

### 3. **Kernel**:
   - The **Kernel** sits in the middle layer and is responsible for managing the system resources, hardware, and processes . It ensures that the system calls made by Chrome and NodeJS are handled properly and also ensures each application gets access to the appropriate version of Python needed for execution.
   - The kernel abstracts hardware complexities and manages how the software interacts with system resources like memory, CPU, and hard disk.

### 4. **Hard Disk Segments**:
   - Below the kernel is the **Hard Disk**, which contains two distinct segments:
     - One segment is allocated to **Python v2** for Chrome.
     - Another segment is allocated to **Python v3** for NodeJS.
   - These segments are likely different environments or virtual environments set up to allow different versions of Python to coexist on the same system without conflict.

### Summary:
- **Chrome** uses Python v2, and **NodeJS** uses Python v3. Both applications interact with the kernel via system calls, and the kernel manages the different Python versions stored on the hard disk, ensuring that the correct version is used for each application. This setup allows multiple Python versions to coexist and serve different applications that require specific versions.

## **Namespacing** and **Control Groups (cgroups)**

  - **Cgroups** = limits how much you can use;
  - **Namespaces** = limits what you can see (and therefore use).

![image](https://github.com/user-attachments/assets/53b0e06c-8571-418b-9a76-e09f0415dcb9)


The diagram explains two important Linux kernel features used to manage system resources in containers or isolated environments: **Namespacing** and **Control Groups (cgroups)**.

### 1. **Namespacing**:

![image](https://github.com/user-attachments/assets/b77b68fc-fd5b-48b3-a184-be1d89766e82)

   Namespacing is a feature used to isolate system resources for processes or groups of processes. This ensures that different processes don't interfere with each other and operate within their own confined space. Here's how different resources are isolated:
   
   - **Processes**: Each process or group of processes operates as if they are the only ones in the system. This ensures process isolation, so that one process doesn’t see or interfere with another.
   - **Users**: The user IDs are isolated so processes believe they are running under a specific user, and cannot interact with users outside their namespace.
   - **Hostnames**: Each namespace can have its own hostname, which isolates network configurations and makes it seem as though each container has its own unique host environment.
   - **Hard Drive**: Access to the file system can be restricted to a certain directory, so a process in a namespace can only interact with specific portions of the hard drive.
   - **Network**: Each namespace can have its own network stack (IP addresses, routing tables, ports), ensuring network isolation.
   - **Inter-process Communication (IPC)**: IPC mechanisms are isolated per namespace, so processes within a namespace can communicate with each other but are isolated from processes in other namespaces.

   **Purpose**: Namespacing creates isolated environments, often used in containerization (e.g., Docker), where each container thinks it’s running on its own machine.

### 2. **Control Groups (cgroups)**:
   Control groups are a kernel feature that limits, measures, and isolates the resource usage (such as CPU, memory, and network) of a process or a group of processes. This prevents any one process from consuming too many system resources, ensuring fair distribution. Here’s how resource limits can be applied:

   - **Memory**: Limits the amount of memory that a process can use. If it exceeds this limit, it might be terminated or slowed down.
   - **CPU Usage**: Restricts how much CPU time a process can use, ensuring that no single process monopolizes the CPU and disrupts the performance of other applications.
   - **Network Bandwidth**: Limits how much network bandwidth a process or group of processes can consume, avoiding network bottlenecks caused by a single application.
   - **HD I/O (Hard Disk Input/Output)**: Controls how much access a process can have to the hard drive for reading or writing data, which prevents processes from overwhelming disk operations.

   **Purpose**: Control groups are used to ensure resource efficiency, prevent resource abuse, and maintain system stability by limiting how much of each system resource a process can use.

---

### In Summary:
- **Namespacing** isolates system resources to provide secure and independent environments for processes or groups of processes.
- **Control Groups (cgroups)** limit and monitor the amount of resources a process can use, ensuring resource control and fairness across the system. 

These two mechanisms are foundational for containerization technologies (like Docker, Kubernetes) that need to isolate environments and efficiently manage system resources.

![image](https://github.com/user-attachments/assets/8787d6f0-6dca-4ac8-9fb3-04a8b85eb22e)

![image](https://github.com/user-attachments/assets/ad515fb2-15a4-4eb1-aeae-98efb90f3c0f)

![image](https://github.com/user-attachments/assets/c22eddfe-8e71-4920-bf57-106fbb896237)



This diagram illustrates a containerized environment, showing how processes interact with system resources, specifically the hard disk. Here's an explanation:

1. **Container:** 
   -  there are two processes: **Chrome** and **NodeJS**.
   -   The **Chrome** process relies on **Python V2** for certain tasks.
   - The **NodeJS** process relies on **Python V3** for certain tasks.

2. **System Call to Access the Hard Disk:**
   - A **system call** is being made from from the  two processes: **Chrome** and **NodeJS* to read data from the hard disk.

3. **Question:**
   - The diagram asks, "**Which process is making this system call?**"
     - **Chrome** **NodeJS** is responsible for **Python V3** and **NodeJS** is responsible for **Python V2**.
       
4. **Hard Disk:**
   - The hard disk is divided into segments:
     - One segment contains **Python V2**.
     - Another segment contains **Python V3**, which is used by **NodeJS**.

### Summary:
The diagram focuses on a **process inside a container** (likely NodeJS) making a system call to access the **hard disk**. The disk is split into segments, including one for **Python V3**, which the system call is probably targeting.

![image](https://github.com/user-attachments/assets/5ff57308-6aa9-4927-87fb-7c47c8ebf01b)


## How do you install Chrome on a computer with no operating system?

![image](https://github.com/user-attachments/assets/5e56bb91-5c8c-495a-9f0a-a0e21b3f22a1)


This flowchart appears to illustrate the steps involved in installing the Google Chrome browser on a computer that currently has no operating system (OS). Here's an explanation of each step:

1. **Install an operating system**:
   - Since the computer has no OS, you first need to install one. The flow mentions specifying a "base image," which could refer to installing an operating system from a pre-configured image (e.g., Linux, Windows).
   
2. **Start up your default browser**:
   - After installing the OS, the default browser (e.g., Edge for Windows or Firefox for some Linux distributions) will be available. 

3. **Navigate to chrome.google.com**:
   - Using the default browser, go to the Chrome download page at chrome.google.com.

4. **Download installer**:
   - Once on the Chrome website, download the Chrome installer file.

5. **Open file/folder explorer**:
   - After downloading, open the file explorer to locate the installer file.

6. **Execute chrome_installer.exe**:
   - Run the Chrome installer (`chrome_installer.exe`) by double-clicking the downloaded file.

7. **Execute chrome.exe**:
   - Once the installation is complete, the executable `chrome.exe` is launched to start Chrome.

Additional Notes in the Flow:
- **Specify a base image**: Refers to the step of installing a specific OS image, which could be a part of a larger automated deployment or manual OS installation.
- **Run commands to install additional programs**: This step is for running commands or scripts to install additional software beyond Chrome if required.
- **Command to run on startup**: This might suggest setting Chrome to run on startup after installation, likely using OS-specific configurations.

Overall, the chart represents the full sequence from setting up the OS to successfully running Chrome on the system.

Here’s a simple example of using Docker to run Google Chrome inside a container. This setup can be useful for testing or automation tasks where you need a browser running in a containerized environment.

### 1. **Dockerfile Example**

![image](https://github.com/user-attachments/assets/143a4586-8623-4847-86bb-5c7dfb8f08a8)

This diagram illustrates the process of building a Docker image from a `Dockerfile`, using Docker's client-server architecture. Here’s a breakdown of the steps:

1. **Dockerfile**: This is a configuration file that contains instructions on how to build and configure a Docker image. It specifies things like the base image, necessary dependencies, file locations, environment variables, and commands to run.

2. **Docker Client**: The Docker client is a command-line interface that takes user commands (like `docker build`) and communicates these to the Docker server.

3. **Docker Server**: Also known as the Docker daemon, this server processes the build request, interpreting the Dockerfile instructions and creating an image. The server also manages containers based on the built images.

4. **Usable Image**: After the server processes the Dockerfile and executes the necessary instructions, it produces a usable Docker image. This image can then be deployed to create a container, which runs the application as specified in the Dockerfile.

In summary, the Docker client sends the build request to the Docker server, which reads the Dockerfile instructions and outputs a Docker image ready for container deployment. This process enables consistent application behavior across different environments.



![image](https://github.com/user-attachments/assets/a9e40f8d-d35f-4657-9d6f-7205476c10a2)



Here’s a Dockerfile that installs Chrome in a lightweight `alpine` Linux container:

![image](https://github.com/user-attachments/assets/d8535ac2-b3f2-4098-a6c7-376b26d92833)

Explanation:

- **Writing a Dockerfile** is like setting up a new computer from scratch so it can do something specific, like run Chrome.

- Imagine you’re given an empty computer with nothing on it, and someone tells you, “Make this computer able to run Chrome.” You’d need to:
  - Install the operating system.
  - Set up basic tools.
  - Finally, download and install Chrome.

In the same way, when you write a Dockerfile, you’re telling Docker step-by-step how to set up everything needed to run your app, starting from a blank environment.


```Dockerfile
# Use an official base image
FROM debian:stable-slim

# Install dependencies
RUN apt-get update && apt-get install -y \
    wget \
    gnupg \
    --no-install-recommends

# Add Google Chrome’s repository key and install Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list' && \
    apt-get update && \
    apt-get install -y google-chrome-stable --no-install-recommends

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Set default command to run Chrome in headless mode
CMD ["google-chrome", "--no-sandbox", "--headless", "--disable-gpu", "--remote-debugging-port=9222"]
```

### 2. **Building the Docker Image**
Save the above Dockerfile in a directory and run the following command to build the Docker image:

```bash
docker build -t chrome-docker .
```

### 3. **Running the Container**
To run the container in headless mode (without a graphical interface) and perform automated tasks, you can use:

```bash
docker run -d -p 9222:9222 chrome-docker
```

### 4. **Using Chrome in the Container**
Once the container is running, you can connect to it via the remote debugging protocol on port `9222`, which you exposed above. You can use tools like Selenium or Puppeteer to interact with Chrome inside the container.

### Notes:
- This setup uses headless Chrome, meaning there’s no GUI (Graphical User Interface), which is ideal for automation or testing in CI pipelines.
- Make sure to adjust the Docker image and settings if you need a full Chrome environment with a UI, such as adding VNC for remote desktop or using a larger base image like Ubuntu.

## Building a Docker image using a Dockerfile

![image](https://github.com/user-attachments/assets/cfe9a038-ced9-4923-8d96-2a8d8165093f)


![image](https://github.com/user-attachments/assets/464ce112-9498-4cfc-a5e3-32f61c688d3b)


![image](https://github.com/user-attachments/assets/cfc4cd72-1117-4a0e-ad3b-3e89a33a723c)

![image](https://github.com/user-attachments/assets/d8e4dd83-c6bf-4cf4-8ded-d46b8143dd2f)



This diagram represents the steps for building a Docker image using a Dockerfile. Here's a more detailed breakdown of each section and its role:

### 1. **FROM alpine**
   - **Explanation**: 
     - This line in the Dockerfile specifies the base image to be used, which is `alpine`, a lightweight Linux distribution.
     - **What happens**: Docker downloads the `alpine` image from the Docker Hub (or from a specified registry).
     - **Result**: The base image forms the foundation upon which subsequent layers and instructions are added.

### 2. **RUN apk add --update redis**
   - **Explanation**: 
     - This command installs `redis` on top of the `alpine` base image. `apk` is the package manager for `alpine`.
     - The `--update` flag ensures that the package index is updated before installing `redis`.

   - **Detailed steps**:
     1. **Get image from the previous step**: The Alpine base image is fetched.
     2. **Create a container out of it**: Docker creates a container based on the Alpine image.
     3. **Run `apk add --update redis` inside the container**: The Redis package is installed within the temporary container.
     4. **Take a snapshot of the modified filesystem (FS)**: Once Redis is installed, Docker takes a snapshot of the container’s filesystem, capturing all the changes (i.e., the addition of Redis).
     5. **Shut down the temporary container**: The container used to perform the installation is no longer needed and is stopped.
     6. **Get image ready for the next instruction**: The updated image (now with Redis installed) is prepared for the next step in the Dockerfile.

### 3. **CMD ["redis-server"]**
   - **Explanation**: 
     - This instruction sets the default command that will be run when a container created from this image is started.
     - Here, it sets `redis-server` as the primary process for the container.

   - **Detailed steps**:
     1. **Get image from the last step**: The image from the previous step (Alpine + Redis) is retrieved.
     2. **Create a container out of it**: A new container is created based on the updated image.
     3. **Tell container it should run `redis-server` when started**: This step sets the container's default behavior to start Redis when the container is launched.
     4. **Shut down the temporary container**: This container is only used to modify the command and is then stopped.
     5. **Get image ready for the next instruction**: The image is now fully ready with Redis installed and configured to run as the default process.

### 4. **Final Image**
   - **Explanation**: 
     - There are no more steps. The Docker build process stops here.
     - **Output**: The final Docker image includes Alpine, Redis installed, and a command (`redis-server`) that will run by default whenever a container based on this image is started.

### Summary
This diagram outlines the creation of a Docker image in three steps:
1. Start with an `alpine` base image.
2. Install `redis` using `apk` in a temporary container, then snapshot the changes.
3. Set the container’s default command to `redis-server` to ensure Redis starts automatically when the container is run.

Each time a new instruction (like `RUN` or `CMD`) is executed, Docker creates a new layer in the image and commits the changes to a new layer.

### Docker image-building process based on several Dockerfile instructions

![image](https://github.com/user-attachments/assets/82e8edcf-a1ac-46d4-8695-8fa0f8efdccb)

This image is a visual representation of a Docker image-building process based on several Dockerfile instructions. Let's break it down step by step:

1. **Base Image (Alpine)**:  
   - The first step is to use an **Alpine Linux base image** (`FROM alpine`). 
   - Alpine is a lightweight Linux distribution that is commonly used for containers due to its minimal footprint.
   - The filesystem snapshot (FS Snapshot) contains basic directories such as `bin`, `dev`, `etc`, `home`, and `proc`, but no specific startup command has been defined at this stage.

2. **Adding Redis**:
   - The next step adds Redis to the image (`RUN apk add --update redis`). 
   - `apk` is the package manager for Alpine Linux, and here it's used to install Redis.
   - After this command, a new image is created (labeled **ab932 Image**). The filesystem snapshot now includes Redis binaries.
   - The startup command remains undefined.

3. **Adding GCC**:
   - The following command installs GCC (`RUN apk add --update gcc`), which is the GNU Compiler Collection, used for compiling C, C++, and other languages.
   - This results in another image (again labeled as **ab932 Image**—perhaps due to caching or naming overlap in the visual).
   - The filesystem snapshot now contains GCC-related binaries in addition to Redis. However, still, no startup command is defined.

4. **Defining the Startup Command**:
   - Finally, the command to start Redis (`CMD ["redis-server"]`) is added.
   - This creates the final image (labeled **fc60771eaa08 Image**), which includes everything from the previous steps.
   - The filesystem snapshot remains the same (with `bin`, `dev`, `etc`, `home`, `proc`, Redis, and GCC), but now the startup command is defined as `redis-server`, which will automatically start Redis when the container runs.

### Summary:
- The image starts with Alpine Linux as the base.
- Redis and GCC are installed in separate layers.
- The final command sets `redis-server` as the container's startup process.

This is a typical Docker build process where each step (or instruction) adds layers to the final image, with the last step determining the container's behavior when it runs.


Here’s another example with a Docker image build process to illustrate the layering approach in Docker:

### Example: Node.js Application with a Custom Base Image

Let’s assume we are building a Docker image for a Node.js application, using a custom base image with additional tools installed.

#### Dockerfile

```Dockerfile
# Step 1: Use Node.js as the base image
FROM node:14

# Step 2: Install wget (useful for retrieving remote files)
RUN apt-get update && apt-get install -y wget

# Step 3: Set the working directory inside the container
WORKDIR /usr/src/app

# Step 4: Copy package.json to the working directory
COPY package*.json ./

# Step 5: Install dependencies
RUN npm install

# Step 6: Copy the entire application code into the working directory
COPY . .

# Step 7: Expose the application's port
EXPOSE 3000

# Step 8: Define the startup command
CMD ["npm", "start"]
```


![image](https://github.com/user-attachments/assets/548d6b6a-c7be-487e-85a5-735d6989d547)

![image](https://github.com/user-attachments/assets/405d28ba-9ce0-48b9-a4bb-261efbb7d92e)


#### Step-by-Step Breakdown (with Image Layers):

1. **Base Image (Node.js)**:
   - We start with the official **Node.js 14** image (`FROM node:14`).
   - This image comes pre-installed with Node.js and npm, providing a base environment for running JavaScript applications.

2. **Adding `wget`**:
   - The second step installs `wget` using the `apt-get` package manager (`RUN apt-get update && apt-get install -y wget`).
   - After this step, a new image layer is created with the `wget` binary included.

3. **Setting Working Directory**:
   - The working directory is set to `/usr/src/app` (`WORKDIR /usr/src/app`), which means any following commands that interact with files will use this directory as the default location.
   - No change to the file system content happens at this point, but it defines where the application’s files will go.

4. **Copying `package.json`**:
   - The `package*.json` files (both `package.json` and `package-lock.json`) are copied into the working directory (`COPY package*.json ./`).
   - These files contain metadata and dependencies for the Node.js project.

5. **Installing Dependencies**:
   - The dependencies listed in `package.json` are installed with the `npm install` command (`RUN npm install`).
   - This creates another layer where the installed Node modules are added to the image.

6. **Copying Application Code**:
   - The rest of the application’s code is copied into the working directory (`COPY . .`).
   - This includes all the files required to run the Node.js app (e.g., `server.js`, application logic, etc.).

7. **Exposing Port 3000**:
   - The application will listen on port 3000, so this port is exposed using `EXPOSE 3000`.

8. **Defining the Startup Command**:
   - Finally, the startup command is defined as `CMD ["npm", "start"]`, which means when the container runs, it will execute `npm start` to launch the Node.js app.

### Image Layer Visualization:

- **Base Layer**: Node.js runtime (from the official Node.js image).
- **Layer 1**: Adds `wget` through `apt-get`.
- **Layer 2**: Sets the working directory for the application.
- **Layer 3**: Copies `package.json` and `package-lock.json` for dependency management.
- **Layer 4**: Installs Node.js dependencies using `npm install`.
- **Layer 5**: Copies all the application code into the image.
- **Layer 6**: Exposes port 3000.
- **Layer 7**: The container will run the `npm start` command when it is launched.

#### Container Behavior:
- Once the image is built and the container is started, it will launch the Node.js application, and the application will be accessible on port 3000.

---

### Another Example: Python Web Application with Flask

#### Dockerfile

```Dockerfile
# Step 1: Use Python as the base image
FROM python:3.9-slim

# Step 2: Install pipenv for managing dependencies
RUN pip install pipenv

# Step 3: Set the working directory inside the container
WORKDIR /app

# Step 4: Copy Pipfile and Pipfile.lock to the working directory
COPY Pipfile Pipfile.lock ./

# Step 5: Install project dependencies
RUN pipenv install --system --deploy

# Step 6: Copy the application code into the working directory
COPY . .

# Step 7: Expose the application's port
EXPOSE 5000

# Step 8: Define the startup command
CMD ["python", "app.py"]
```

#### Breakdown:

1. **Base Image (Python)**:
   - Uses the official **Python 3.9 slim** image (`FROM python:3.9-slim`), a lightweight version of the Python runtime.

2. **Adding Pipenv**:
   - Installs `pipenv` (`RUN pip install pipenv`), a tool for managing Python dependencies and virtual environments.
   
3. **Working Directory**:
   - Sets the working directory to `/app` where the application will be stored and run from (`WORKDIR /app`).

4. **Copy Pipfile**:
   - Copies `Pipfile` and `Pipfile.lock` to the image, which are used to specify the required Python dependencies (`COPY Pipfile Pipfile.lock ./`).

5. **Installing Dependencies**:
   - Installs all dependencies listed in the `Pipfile` using `pipenv install --system --deploy`. This ensures that the project dependencies are installed in the system rather than in a virtual environment, making them available globally in the container.

6. **Copy Application Code**:
   - Copies the entire application code into the container (`COPY . .`).

7. **Exposing Port 5000**:
   - Exposes port 5000 for the Flask app to be accessible.

8. **Defining Startup Command**:
   - Specifies the startup command as `python app.py`, which runs the Flask application.

---

### Image Layer Visualization:

- **Base Layer**: Python 3.9 slim version.
- **Layer 1**: Adds `pipenv` for dependency management.
- **Layer 2**: Working directory is set to `/app`.
- **Layer 3**: `Pipfile` and `Pipfile.lock` are added for dependency management.
- **Layer 4**: Installs dependencies with `pipenv install`.
- **Layer 5**: Copies application code to `/app`.
- **Layer 6**: Exposes port 5000 for the web server.
- **Layer 7**: Specifies `python app.py` as the startup command.

#### Container Behavior:
- Once built and started, the container will run the Flask web application and serve it on port 5000.

Both of these examples show how Docker images are built layer by layer, and how each instruction in the Dockerfile contributes to the final image that will run the application in a container.


## how Docker containers interact with the underlying system resources 

![image](https://github.com/user-attachments/assets/dea4b638-ce4f-4e76-b305-af94e180f4c1)

![image](https://github.com/user-attachments/assets/0109d3c4-36f8-4372-8eb8-ff2c0f01d625)

![image](https://github.com/user-attachments/assets/5230e70d-abfc-4605-84be-73a9863ef900)

![image](https://github.com/user-attachments/assets/2a43b557-6434-4c50-88b6-bb8f18364265)

![image](https://github.com/user-attachments/assets/e4a454c0-21a9-48c1-89b5-06e7e8548e30)

![image](https://github.com/user-attachments/assets/49423746-9b16-49f2-a262-1f8a030d4e42)

![image](https://github.com/user-attachments/assets/954576b6-ca45-4145-9254-cc363506b1aa)

![image](https://github.com/user-attachments/assets/219f745f-40a7-4f61-8de3-ba199b6762cf)

![image](https://github.com/user-attachments/assets/033fe035-0f4d-43b1-bbd7-c66992d8e507)

![image](https://github.com/user-attachments/assets/14c90dfd-0c24-4899-9195-25b5faec8e32)

![image](https://github.com/user-attachments/assets/c23dc99f-2d26-4189-adc7-7a47d4fdb899)





This diagram illustrates how Docker containers interact with the underlying system resources (such as the kernel, CPU, RAM, and disk) and what happens when you build and run a Docker container using a Node.js image on Alpine Linux.

### Explanation of Each Component:

#### **Dockerfile Instructions:**

1. **`FROM node:alpine`**:
   - The Docker build process begins with a base image, in this case, a lightweight **Alpine Linux** image with **Node.js** pre-installed (`node:alpine`).
   - This base image provides a minimal environment to run a Node.js application.

2. **`RUN npm install`**:
   - This command installs the necessary Node.js dependencies for the application using npm. It’s executed during the image build process, creating a layer where all the required libraries and modules are installed.

3. **`CMD ["npm", "start"]`**:
   - This command defines the default startup process of the container. When the container runs, it will execute `npm start` to start the Node.js application.

#### **Node:alpine Image Layer**:

- The image resulting from the instructions mentioned above is labeled as **Node:alpine Image**. 
- This image includes a **filesystem snapshot** of all the required directories like:
  - `bin`, `dev`, `etc`, `home`, `proc`—which represent the directories from the Alpine Linux base image and the Node.js environment.
- No startup command is explicitly defined in the snapshot until the `CMD` instruction in the Dockerfile, where the container is set to run the Node.js application.

#### **Container (at Runtime):**

- **Kernel**: 
  - The Docker container relies on the **host operating system's kernel** to interact with hardware resources like CPU, RAM, and disk. Containers share the kernel with the host system but have isolated processes, making them lightweight compared to virtual machines.
  
- **Running Process**:
  - Once the container is started (based on the `CMD` instruction), it initiates a **running process**, such as the Node.js application.
  - The running process has access to a defined subset of system resources (RAM, network, CPU, and storage).
  
- **Resource Isolation**:
  - The container's **RAM**, **Network**, **CPU**, and **Disk** usage are isolated from the rest of the system, meaning the container operates as if it is a separate entity, despite sharing the kernel with the host OS.
  - The container is given a specific **hard drive segment** for its file system (including directories like `bin`, `dev`, etc.) and data, while the rest of the hard drive remains inaccessible to it. This is part of Docker's storage and resource isolation feature.

#### **Rest of the Hard Drive**:
- The **REST OF HARD DRIVE** block represents the part of the system's disk space that is outside the container’s scope. Containers only have access to the portion of disk space allocated to them and can't interact with the rest of the system’s file storage unless explicitly configured (e.g., through Docker volumes).

### Summary:
- The left-hand side represents how the image is built using Alpine Linux with Node.js, installing dependencies via npm, and specifying the startup command (`npm start`).
- The right-hand side shows how the container operates at runtime, interacting with the system kernel, consuming resources (RAM, CPU, network, disk), and maintaining file system isolation from the rest of the system.

This setup emphasizes Docker's ability to package applications in a way that they can run in isolated environments, with controlled access to system resources.



## Dockerfile

```Dockerfile

FROM node:18-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build

CMD [ "node", "dist/main.js" ]


```


This is a Dockerfile, a script that defines the environment and steps needed to create a Docker container for a Node.js application. Let's go through it step-by-step:

1. **FROM node:18-alpine**
   - This line specifies the base image for the Docker container. `node:18-alpine` is a lightweight version of the Node.js 18 runtime, based on the Alpine Linux distribution. This helps keep the image small and efficient.

2. **WORKDIR /usr/src/app**
   - This sets the working directory inside the container to `/usr/src/app`. All subsequent commands will be run in this directory. If the directory does not exist, it will be created.

3. **COPY package*.json ./**
   - This command copies the `package.json` and `package-lock.json` files from the host machine to the current working directory in the container (`/usr/src/app`). The `*` wildcard ensures both files are copied if they exist.

4. **RUN npm ci**
   - `npm ci` (short for "clean install") installs the dependencies listed in `package-lock.json`. This command is preferred in CI (Continuous Integration) environments as it ensures a clean and reproducible install of dependencies.

5. **COPY . .**
   - This copies all files from the current directory on the host machine to the current working directory in the container (`/usr/src/app`). Essentially, it adds the application code to the container.

6. **RUN npm run build**
   - This runs the `build` script defined in the `package.json` file. This script typically compiles the application, preparing it for production. The exact behavior depends on what is defined in the `build` script of your `package.json`.

7. **CMD [ "node", "dist/main.js" ]**
   - This specifies the command to run when the container starts. Here, it runs `node dist/main.js`, which likely starts the Node.js application. `dist/main.js` is presumably the entry point of the built application.

## Docker Compose configuration for a microservices architecture:

version: '3.8'
```yml
services:
  user-service:
    container_name: user-service
    build:
      context: ./user-service
      dockerfile: Dockerfile
    ports:
      - "8081:8081"
    env_file:
      - ./user-service/.env
    networks:
      - my-network

  product-service:
    container_name: product-service
    build:
      context: ./product-service
      dockerfile: Dockerfile
    ports:
      - "8082:8082"
    env_file:
      - ./product-service/.env
    networks:
      - my-network

  order-service:
    container_name: order-service
    build:
      context: ./order-service
      dockerfile: Dockerfile
    ports:
      - "8083:8083"
    env_file:
      - ./order-service/.env
    networks:
      - my-network

networks:
  my-network:
    driver: bridge

```

### Conclusion

Docker revolutionizes the way applications are developed, shipped, and run by providing a lightweight, efficient, and consistent environment for application execution. Its ecosystem, comprising various tools and services, enhances the capabilities of container management, making it a powerful solution for modern application development and deployment.






### Docker Port Forwarding

Each computer has its own localhost and ports. Docker containers, being virtual machines, also have their own localhost and ports. To access services running inside Docker containers from the host machine, you need to perform port forwarding.

#### Accessing a MySQL Container

To connect to a MySQL database running inside a Docker container, you must map a port on the host machine to the container's port. Here’s how to do it:

1. **Run the MySQL container with port forwarding:**
   ```bash
   docker run -p host_machine_port:container_port -e MYSQL_ROOT_PASSWORD=your_password mysql
   ```
   Example:
   ```bash
   docker run -p 4000:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
   ```

2. **Enter the running container:**
   ```bash
   docker exec -it <container_id> sh
   ```

3. **Access MySQL inside the container:**
   ```bash
   mysql -u <MYSQL_USER> -p
   ```

Now, you can connect to MySQL on `localhost:4000` from the host machine. Docker will forward the request to the container's port `3306`.

#### MongoDB

1. **Start the MongoDB container with port forwarding:**
   ```bash
   sudo docker run -dp 27017:27017 -v local-mongo:/data/db --name local-mongo --restart=always mongo
   ```

2. **Enter the MongoDB container:**
   ```bash
   sudo docker exec -it local-mongo sh
   ```

3. **Start the MongoDB shell:**
   ```bash
   mongo
   ```

#### Redis

1. **Stop Redis server:**
   ```bash
   /etc/init.d/redis-server stop
   ```

2. **Start Redis server:**
   ```bash
   /etc/init.d/redis-server start
   ```

3. **Restart Redis server:**
   ```bash
   /etc/init.d/redis-server restart
   ```

#### PostgreSQL

1. **Start the PostgreSQL container with port forwarding:**
   ```bash
   sudo docker run -p 4000:5432 -e POSTGRES_PASSWORD=123456 postgres
   ```

2. **Enter the PostgreSQL container:**
   ```bash
   sudo docker exec -it <container_id> sh
   ```

3. **Access PostgreSQL CLI:**
   ```bash
   psql -U postgres
   ```

4. **Create a database inside the container:**
   ```sql
   CREATE DATABASE mydatabase;
   ```

5. **Create a user with a password:**
   ```sql
   CREATE ROLE myuser WITH LOGIN PASSWORD 'mypassword';
   ```

6. **Grant privileges to the user on the database:**
   ```sql
   GRANT ALL PRIVILEGES ON DATABASE mydatabase TO myuser;
   ```

7. **Show all databases:**
   ```sql
   \l
   ```

8. **Connect to a specific database:**
   ```sql
   \c database_name
   ```

9. **Show all tables:**
   ```sql
   \dt
   ```

10. **Access a specific schema:**
    ```sql
    \dt schema_name.*
    ```

11. **Query a specific table:**
    ```sql
    SELECT * FROM <table_name>;
    ```

12. **Exit the CLI:**
    ```sql
    \q
    ```

By using these commands, you can manage port forwarding and access various database services running inside Docker containers from your host machine.



### Docker Port Forwarding and Volume Mapping

This guide provides instructions for running Docker containers with port forwarding and volume mapping.

#### Port Forwarding

To forward a port from your host machine to a Docker container, use the following command:

```bash
docker run -p host_machine_port:container_port image_name
```

**Example:** To run an Nginx container and forward port 3004 on the host machine to port 80 in the container:

```bash
docker run -p 3004:80 nginx
```

When you request `localhost:3004`, the host machine will forward the request to the Nginx container running on port 80.

#### Volume Mapping

Volume mapping allows you to share files between your host machine and a Docker container. Use the following command:

```bash
docker run -v host_machine_folder_path:container_folder_path image_name
```

**Example:** To run a MySQL container and map a host directory (`/my/host/data`) to the container's data directory (`/var/lib/mysql`):

```bash
docker run -v /my/host/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql
```

#### Combining Port Forwarding and Volume Mapping

You can combine port forwarding and volume mapping in one command:

```bash
docker run -p host_machine_port:container_port -v host_machine_folder_path:container_folder_path image_name
```

**Example:** To run a MySQL container, forward port 4000 on the host machine to port 3306 in the container, and map a host directory (`/my/host/data`) to the container's data directory (`/var/lib/mysql`):

```bash
docker run -p 4000:3306 -v /my/host/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql
```

With volume mapping, files created in the container will be visible in the mapped directory on the host machine. This allows for easy file sharing and persistent data storage between the host and the container.



### Dockerfile

```dockerfile
# Use the official Node.js image based on Alpine Linux
FROM node:alpine

# Set the working directory to /app
WORKDIR /app

# Copy package.json from the host into the container's working directory
COPY package.json .

# Install dependencies listed in package.json
RUN npm install

# Copy all the application files from the host into the container's working directory
COPY . .

# Define the default startup command
CMD ["npm", "run", "start"]
```

### Building the Docker Image

To build the Docker image, run the following command:

```bash
docker build -t example-image:v1 .
```

### How the Process Works

1. **FROM node:alpine:** The Docker daemon starts by creating a temporary container using the official Node.js image based on Alpine Linux.

2. **WORKDIR /app:** It then sets the working directory to `/app` within the container.

3. **COPY package.json .:** The `package.json` file from the host machine is copied into the container's `/app` directory.

4. **RUN npm install:** This command installs all the dependencies listed in `package.json` within the container.

5. **COPY . .:** All the application files from the host machine are copied into the container's working directory (`/app`).

6. **CMD ["npm", "run", "start"]:** This command specifies the default command to run when a container created from this image is started. It tells the container to start the Node.js application using `npm`.

### Pushing the Docker Image to Docker Hub

To share your Docker image with others, you can push it to a container registry like Docker Hub. Ensure you are logged in to your Docker Hub account using `docker login`.

1. **Tag the image with your username and version:**

   ```bash
   docker tag example-image:v1 your-username/example-image:v1
   ```

2. **Push the tagged image to Docker Hub:**

   ```bash
   docker push your-username/example-image:v1
   ```

### Summary

- **Build the Image:** The `docker build` command compiles the Dockerfile into an image.
- **FROM Directive:** Starts from a base image (Node.js based on Alpine Linux).
- **WORKDIR:** Sets the working directory in the container.
- **COPY:** Copies files from the host into the container.
- **RUN npm install:** Installs dependencies.
- **CMD:** Specifies the command to run the application.
- **Push to Docker Hub:** Tags and pushes the image to Docker Hub for sharing.



### 1. **What is the base image used in the Dockerfile?**

To find out the base image in a Dockerfile, inspect the `FROM` statement at the beginning of the file.

```bash
cat Dockerfile
```

The `FROM` statement specifies the base image being used.

---

### 2. **What command is used to run the application inside the container?**

The command used to run the application in a container is defined in the `CMD` or `ENTRYPOINT` section of the Dockerfile.

To inspect it:

```bash
cat Dockerfile
```

Look for the `CMD` or `ENTRYPOINT` instruction, which specifies how the application is launched.

---

### 3. **Build a Docker image using the Dockerfile and name it `webapp-color`.**

To build the Docker image from the Dockerfile, run the following command:

```bash
docker build -t webapp-color .
```

This command builds an image and names it `webapp-color` without specifying any tag, so it defaults to the `latest` tag.

---

### 4. **Run an instance of the image `webapp-color` and publish port 8080 on the container to 8282 on the host.**

To run the container, mapping the container's port 8080 to the host's port 8282:

```bash
docker run -d -p 8282:8080 webapp-color
```

This command runs the container in detached mode (`-d`), maps the container's port 8080 to host port 8282, and starts an instance of `webapp-color`.

---

### 5. **What is the base Operating System used by the `python:3.6` image?**

To find the base operating system of the `python:3.6` image, you can run a container interactively and check the OS details:

```bash
docker run -it python:3.6 /bin/bash
```

Inside the container, use the following command to check the operating system:

```bash
cat /etc/os-release
```

This will provide information about the base OS of the `python:3.6` image.

---

### 6. **Why use `-it` in the command `docker run -it python:3.6 /bin/bash`?**

The `-it` option in Docker is used to run a container interactively with a pseudo-TTY. Here's the breakdown:
- `-i` keeps STDIN open to interact with the container.
- `-t` allocates a pseudo-terminal.

The full command:

```bash
docker run -it python:3.6 /bin/bash
```

Allows you to interact with the container's shell directly.

---

### 7. **Build a smaller Docker image using the same Dockerfile and name it `webapp-color:lite`.**

To build a smaller image, modify the base image in the Dockerfile to something smaller like `python:3.6-alpine` and ensure that the final image size is under 150MB.

Here’s how you would build it:

```bash
docker build -t webapp-color:lite .
```

By changing the base image to `python:3.6-alpine`, you reduce the size of the final image.


# Docker compose

Docker compose make executing docker run easier.

### Short Summary:
- **`docker compose up --build`**: Rebuild images and start the services.
- **`docker compose up`**: Start services using already built images (or build if necessary).
- **`docker compose down`**: Stop and remove all services, networks, and containers created by the `docker-compose` command.

This command starts the services defined in the `docker-compose.yml` file.



### 1. **`docker compose up --build`**

This command does two things:
- **`up`**: creates and starts the services defined in the `docker-compose.yml` file.
- **`--build`**: Forces the recreation (rebuild) of the images, even if the images already exist locally.

#### What it does:
- When you run `docker compose up --build`, Docker Compose will:
  1. Build or rebuild any images defined in the `docker-compose.yml` file.
  2. Create and start the containers for each service.
  3. If there are changes in your Dockerfile or the dependencies, it will rebuild the images before launching the containers.
  
#### When to use:
- Use this when you’ve made changes to the Dockerfile or dependencies and want to ensure those changes are reflected in the container.

---

### 2. **`docker compose up`**

**`docker compose up`** essentially does three things for each service defined in your `docker-compose.yml` file:

#### 1. **Create** the services:
   - If the containers do not already exist, Docker Compose will **create** new containers from the images specified in the `docker-compose.yml` file. If an image doesn’t exist locally, it will either pull it from a registry (like Docker Hub) or build it (if you have a build context defined).

#### 2. **Start** the services:
   - If the containers already exist but are stopped, Docker Compose will **start** them. This means it will resume the containers without recreating them. If they don’t exist, it will create and then start the containers.

#### 3. **Run** the services:
   - Once the services are started, the containers will begin to **run** the applications or processes they are configured for. For example, a web server, a database, or any other program defined in the Dockerfile or `docker-compose.yml` will start running.


### Summary:
When you run `docker compose up`, Docker:
1. **Create** the containers (if they don’t already exist).
2. **Start** the containers (if they exist but are stopped).
3. **Run** The actual processes inside the containers (like a web server, database, etc.) are executed and kept running.

If the containers are already running, it just continues to run them.

#### What it does:
- When you run `docker compose up` (without `--build`), Docker Compose will:
  1. Look for any pre-built images for your services.
  2. If the images are already built, it will use those to create and start the containers.
  3. If the images don’t exist, it will automatically build them (but only if they haven't been built before).
  
#### When to use:
- Use this when you want to start your application without forcing a rebuild of the images.
- It is faster than `docker compose up --build` because it doesn’t rebuild the images unless necessary.

---
### 3.  **`docker compose up -d`**

The `-d` flag stands for **detached mode**.

#### What it does:
- When you run `docker compose up -d`, Docker Compose will:
  1. Create and start all services defined in the `docker-compose.yml` file, just like the regular `docker compose up` command.
  2. Run the containers in **detached mode**, meaning they will run in the background.

#### Key differences:
- Without `-d`, the logs of the running containers are attached to your terminal, and you can see the output of the containers live. The terminal will be occupied until you stop the services with `Ctrl + C`.
- With `-d`, the containers will start in the background, and the terminal is freed up immediately, allowing you to continue using it.
  

#### How to view running services:
After running `docker compose up -d`, you can view the running containers with:
```bash
docker ps
```

If you want to see the logs of the containers while they run in detached mode, you can use:
```bash
docker compose logs
```

#### When to use:
- Use this when you want to run your services in the background without keeping your terminal occupied. It’s particularly useful when you don’t need to monitor the logs in real time.


### Example:
```bash
docker compose up -d
```
- This command will create, start the services, and run them in the background.


### 4. **`docker compose down`**

This command stops and removes the containers, networks, and volumes defined in the `docker-compose.yml` file.

#### What it does:
- When you run `docker compose down`, Docker Compose will:
  1. Stop all the running containers created by `docker compose up`.
  2. Remove the containers.
  3. Remove any networks that were created as part of the `docker-compose.yml`.
  4. Optionally remove named volumes if you use the `-v` flag (e.g., `docker compose down -v`).
  
#### When to use:
- Use this when you want to completely stop and clean up the environment created by Docker Compose. This is useful when you're done working on a project or want to start fresh.

---


The image shows a simple chart explaining the meaning of exit status codes, commonly used in programming and shell scripting.

- **Status Code 0:**
-  process.exit(0)
  - The message says, *"We exited and everything is OK."* 
  - This means that when a program or script finishes and returns an exit code of `0`, it signifies successful execution without any errors.

- **Status Code 1, 2, 3, etc.:**
  - process.exit(1 or 2 or 3 .....)
  - The message says, *"We exited because something went wrong."*
  - Any non-zero exit code (1 or higher) indicates that an error or some issue occurred during the execution, and the program or script did not complete successfully.

In summary:
- Exit code `0` = success.
- Exit code `1` or greater = failure or error occurred.
- 

![image](https://github.com/user-attachments/assets/d89a1507-4dee-45d1-b855-125ec9385633)

```yml
version: '3'
services:
  redis-server:
    image: 'redis'
  node-app:
    restart: on-failure
    build: .
    ports:
      - '4001:5000'

```


### **`docker build -f Dockerfile.dev .`**

This command is used to build a Docker image from a **specific Dockerfile** (`Dockerfile.dev`) instead of the default `Dockerfile` in the current directory (`.`).

### Breakdown of the command:

- **`docker build`**: The command to build or create a Docker image.
- **`-f Dockerfile.dev`**: The `-f` flag allows you to specify a custom Dockerfile (in this case, `Dockerfile.dev`) instead of the default `Dockerfile`.
- **`.` (dot)**: Defines the build context  which in this case is the current directory, typically the directory where the app's code and Dockerfile are located.


### Why use a custom Dockerfile?

In development, you might have a different Dockerfile (e.g., `Dockerfile.dev`) for your development environment, with certain tools, debuggers, or configurations that are not needed in production. For production, you'd typically use the standard `Dockerfile` which would be optimized for performance and smaller in size.

---

### Example:

Suppose you have two Dockerfiles:



1. **`Dockerfile`**: For production
   ```Dockerfile
      # Use the official Node.js image as a base image
      # Use a minimal Node.js image
       FROM node:16-alpine
      
      # Set the working directory in the container
      WORKDIR /usr/src/app
      
      # Copy package.json and package-lock.json into the working directory
      COPY package*.json ./
      
      # Install dependencies
      RUN npm install --production
      
      # Copy the rest of the application code into the container
      COPY . .
      
      # Expose the port that the app runs on
      EXPOSE 3000
      
      # Command to run the application
      CMD ["npm", "start"]


   ```

2. **`Dockerfile.dev`**: For development
   
   ```Dockerfile
       # Use the official Node.js image as a base image
       # Use a larger Node.js image with more development tools
       FROM node:16
   
      # Set the working directory in the container
       WORKDIR /usr/src/app
      
      # Copy package.json and package-lock.json into the working directory
       COPY package*.json ./
      
       # Install additional development tools like nodemon for hot-reloading
       RUN npm install -g nodemon
      
      # Copy the rest of the application code into the container
       COPY . .
      
      # Expose the port that the app runs on
       EXPOSE 3000
     # Start the app with nodemon to enable live-reloading during development
       CMD ["nodemon", "app.js"]
   ```


### How to build using `Dockerfile.dev`:

To build the development image, you'd run:
```bash
docker build -f Dockerfile.dev -t my-app-dev .
```

- **`-f Dockerfile.dev`**: Instructs Docker to use the `Dockerfile.dev` instead of the default `Dockerfile`.
- **`-t my-app-dev`**: Tags the built image with the name `my-app-dev`.
- **`.`**: Specifies the current directory as the build context (where your application code and `Dockerfile` are located).

### What happens when you run this command:
1. Docker reads the instructions in `Dockerfile.dev`.
2. It uses the full Node.js image (`node:16`) instead of the smaller `node:16-alpine` version, which is better for development because it includes additional tools.
3. It installs **all** dependencies (not just the production ones) and includes extra development tools (like `nodemon` for hot-reloading).
4. Docker builds the image and tags it as `my-app-dev`.

### Example usage:
After building the development image, you can run it with:
```bash
docker run -p 3000:3000 my-app-dev
```

This command will run your development environment on port 3000, using the image built with the development Dockerfile.

---

### Summary:
- `docker build -f Dockerfile.dev .` builds a Docker image using the custom `Dockerfile.dev` instead of the default `Dockerfile`.
- This is commonly used to differentiate between development and production environments where different dependencies, tools, or configurations are needed.

##  Git-based development workflow with continuous integration (CI) and deployment to AWS

![image](https://github.com/user-attachments/assets/9445d083-3479-49c9-9b9a-5d2c22963646)


This image represents a simplified Git-based development workflow with continuous integration (CI) and deployment to AWS. Here's the breakdown:

1. **GitHub Repo**: This is the main source code repository hosted on GitHub. It manages different branches of the code.

2. **Feature Branches**: As a developer (represented by "You"), you create a new branch for each feature you are working on. This is done to isolate your changes from the main `master` branch. You push the changes to the GitHub repository under the `feature` branch.

3. **Pull Request**: After working on your feature, you submit a pull request (PR) to merge the `feature` branch into the `master` branch. This initiates a code review process where your changes are reviewed by others.

4. **Master Branch**: Once the pull request is approved and merged, your changes become part of the `master` branch, which typically represents the production-ready code.

5. **Travis CI**: After merging into the `master` branch, Travis CI (a continuous integration service) automatically runs tests and builds the code. If the tests pass and the build is successful, it continues to the next step.

6. **AWS Hosting**: Once the CI build is successful, the code is deployed to AWS (Amazon Web Services), where the application is hosted. This ensures that the latest changes are live and accessible to users.

In summary:
- You work on a feature branch.
- Create a pull request to merge changes into the `master`.
- Travis CI runs tests and builds the project.
- If successful, the code is deployed to AWS for production.

##  Git-based development workflow with continuous integration (CI) and deployment to AWS

![image](https://github.com/user-attachments/assets/83026666-e1c3-44ac-a37a-a41ac15e942b)

This process follows common DevOps practices with automated testing and deployment.


This diagram represents a typical DevOps workflow for deploying code changes across development (Dev), testing (Test), and production (Prod) environments. Here's an explanation of the flow:

1. **Dev Environment**:
   - **Create/change features**: Developers create or modify code features.
   - **Make changes on a non-master branch**: The changes are made in a separate branch, not directly on the master branch.
   - **Push to GitHub**: The changes are pushed to a remote Git repository like GitHub.
   - **Create Pull Request to merge with master**: A pull request (PR) is created, suggesting the changes be merged into the master branch after review.

2. **Test Environment**:
   - **Code pushed to Travis CI**: When the PR is created, the code is automatically pushed to a Continuous Integration (CI) tool like Travis CI for testing.
   - **Tests run**: Automated tests are executed to ensure the changes don't break existing functionality.
   - **Merge PR with master**: If the tests pass and the code review is successful, the pull request is merged into the master branch.

3. **Prod Environment**:
   - **Code pushed to Travis CI**: After merging with master, the code is again pushed to Travis CI for a final round of tests.
   - **Tests run**: Another round of automated tests is run to ensure stability before deploying to production.
   - **Deploy to AWS Elastic Beanstalk**: If the tests pass, the code is deployed to the production environment using AWS Elastic Beanstalk.

This workflow shows a standard CI/CD (Continuous Integration/Continuous Deployment) pipeline that emphasizes automated testing and deployment.


![image](https://github.com/user-attachments/assets/606407d4-811e-4733-b182-87187a97844d)

![image](https://github.com/user-attachments/assets/17f854c5-27f0-4a8f-bc8a-3dff4569f79f)


### **Build Phase** and Run Phase in Production grade Application


```
            Build Phase
           -------------
               |
        +-----------------+
        | Use node:alpine |
        +-----------------+
               |
 +------------------------------+
 | Copy the package.json file   |
 +------------------------------+
               |
     +-----------------------+
     | Install dependencies  |
     +-----------------------+
               |
      +----------------------+
      | Run 'npm run build'  |
      +----------------------+
               |
               v

            Run Phase
           ------------
               |
        +----------------+
        |   Use nginx    |
        +----------------+
               |
 +------------------------------------+
 | Copy over the result of 'npm run   |
 | build'                             |
 +------------------------------------+
               |
      +------------------+
      |   Start nginx    |
      +------------------+
```

This diagram represents a Docker multi-stage build process for deploying a Node.js application. It is divided into two phases:

### 1. Build Phase
   - **Use `node:alpine`**: A lightweight version of the Node.js image (Alpine Linux) is used to keep the build environment small.
   - **Copy the `package.json` file**: This step involves copying only the `package.json` file to the container. This is done first to leverage Docker’s caching layer, allowing faster builds if dependencies don’t change.
   - **Install dependencies**: With the `package.json` file copied, dependencies are installed.
   - **Run `npm run build`**: This command builds the production-ready version of the app, generating static files (usually placed in a `build` or `dist` folder).

### 2. Run Phase
   - **Use `nginx`**: The application will run on an Nginx server, so an Nginx Docker image is used in this phase.
   - **Copy over the result of `npm run build`**: The static files from the build phase are copied to the Nginx container.
   - **Start Nginx**: Nginx serves the static files, allowing the application to be accessible in production.

This setup is efficient because the final Docker image only includes the Nginx server and the static files, making it lightweight and optimized for deployment.

### Sample Example 

```dockerfile
# Build Phase
FROM node:alpine AS builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

# Run Phase
FROM nginx
COPY --from=builder /app/build /usr/share/nginx/html
```

### Explanation
- **Build Phase**:
  - Starts from a lightweight Node.js image (`node:alpine`).
  - Sets the working directory to `/app`.
  - Copies `package.json` for dependency installation.
  - Copies the rest of the application files and builds the project.

- **Run Phase**:
  - Uses the `nginx` image to serve the static files.
  - Copies the built files from the build phase into the Nginx HTML directory (`/usr/share/nginx/html`).




### What is Docker?

Docker is a platform and ecosystem designed to develop, ship, and run applications inside containers. It consists of several key components that work together to manage containerized applications efficiently.

To better understand docker see the diagram : https://app.diagrams.net/?src=about#G1bzvbHFhDX4LxF4KLwHnEul0Mtnb06XmE#%7B%22pageId%22%3A%22Jy9q0EDmPOdd4UMKcCcg%22%7D

Got it! Here's the information organized into a table format with a sample command:

| Category            | Command                     | Description                                                  | Example                                              |
|---------------------|-----------------------------|--------------------------------------------------------------|------------------------------------------------------|
| Container Management| docker run                  | Create and start a new container from an image.              | `docker run -d --name my_container nginx`           |
|                     | docker start                | Start one or more stopped containers.                        | `docker start my_container`                         |
|                     | docker stop                 | Stop one or more running containers.                        | `docker stop my_container`                          |
|                     | docker restart              | Restart one or more containers.                              | `docker restart my_container`                       |
|                     | docker rm                   | Remove one or more containers.                               | `docker rm my_container`                            |
|                     | docker ps                   | List running containers.                                     | `docker ps`                                          |
|                     | docker ps -a                | List all containers (including stopped ones).                | `docker ps -a`                                       |
|                     | docker exec                 | Run a command inside a running container.                   | `docker exec -it my_container bash`                 |
|                     | docker logs                 | Fetch the logs of a container.                               | `docker logs my_container`                          |
| Image Management    | docker build                | Build a Docker image from a Dockerfile.                      | `docker build -t my_image .`                        |
|                     | docker pull                 | Pull an image or a repository from a registry.              | `docker pull nginx`                                 |
|                     | docker push                 | Push an image or a repository to a registry.                | `docker push my_username/my_image`                  |
|                     | docker images               | List all locally available images.                           | `docker images`                                     |
|                     | docker rmi                  | Remove one or more images.                                   | `docker rmi my_image`                               |
|                     | docker tag                  | Tag an image with a new name and/or tag.                    | `docker tag my_image my_new_image`                  |
| Network Management  | docker network create       | Create a new Docker network.                                 | `docker network create my_network`                  |
|                     | docker network ls           | List Docker networks.                                        | `docker network ls`                                 |
|                     | docker network inspect      | Display detailed information on one or more networks.        | `docker network inspect my_network`                 |
|                     | docker network connect      | Connect a container to a network.                            | `docker network connect my_network my_container`    |
|                     | docker network disconnect   | Disconnect a container from a network.                       | `docker network disconnect my_network my_container` |
| Volume Management   | docker volume create        | Create a new volume.                                         | `docker volume create my_volume`                    |
|                     | docker volume ls            | List Docker volumes.                                         | `docker volume ls`                                  |
|                     | docker volume inspect       | Display detailed information on one or more volumes.         | `docker volume inspect my_volume`                   |
|                     | docker volume rm            | Remove one or more volumes.                                  | `docker volume rm my_volume`                        |
|                     | docker volume prune         | Remove all unused volumes.                                   | `docker volume prune`                               |
| System Management   | docker info                 | Display system-wide information.                             | `docker info`                                       |
|                     | docker version              | Show the Docker version information.                         | `docker version`                                    |
|                     | docker system df            | Show Docker disk usage.                                      | `docker system df`                                  |
|                     | docker system prune         | Remove unused data (containers, networks, images, volumes). | `docker system prune`                               |
|                     | docker stats                | Display a live stream of container resource usage statistics.| `docker stats`                                      |
| Registry Management | docker login                | Log in to a Docker registry.                                 | `docker login`                                      |
|                     | docker logout               | Log out from a Docker registry.                              | `docker logout`                                     |
|                     | docker search               | Search for Docker images on Docker Hub.                      | `docker search nginx`                               |


Sure, here's the rewritten list of Docker networking commands:

**List available networks:**
```
docker network ls
```

**Remove one or more networks:**
```
docker network rm [network]
```

**Show information on one or more networks:**
```
docker network inspect [network]
```

**Connect a container to a network:**
```
docker network connect [network] [container]
```

**Disconnect a container from a network:**
```
docker network disconnect [network] [container]
```

Here's the list of Docker image-related commands:

**Create an image from a Dockerfile:**
```
docker build [dockerfile-path]
```

**Build an image from a Dockerfile located in the current directory:**
```
docker build .
```

**Create an image from a Dockerfile and tag it:**
```
docker build -t [name]:[tag] [dockerfile-path]
```

**Specify a file to build from:**
```
docker build -f [file-path]
```

**Pull an image from a registry:**
```
docker pull [image]
```

**Push an image to a registry:**
```
docker push [image]
```

**Create an image from a tarball:**
```
docker import [url/file]
```

**Create an image from a container:**
```
docker commit [container] [new-image]
```

**Tag an image:**
```
docker tag [image] [image]:[tag]
```

**Show all locally stored top-level images:**
```
docker images
```

**Show history for an image:**
```
docker history [image]
```

**Remove an image:**
```
docker rmi [image]
```

**Load an image from a tar archive or stdin:**
```
docker load --input [tar-file]
```

**Save an image to a tar archive file using Docker save command:**
```
docker save [image] > [tar-file]
```

**Remove unused images:**
```
docker image prune
```

Replace `[dockerfile-path]`, `[name]`, `[tag]`, `[file-path]`, `[image]`, `[url/file]`, `[container]`, and `[new-image]` with the appropriate values according to your use case.

### How do Windows and Mac have Containers without Namespacing?
- Use virtualization technologies (Hyper-V for Windows, HyperKit for Mac) to create lightweight VMs running a Linux distribution (WSL for Windows).
- Containers are deployed within these VMs, providing an isolated runtime environment.

### Docker Client & Server
- **Docker Client:** CLI tool for interacting with Docker.
- **Docker Server (Daemon):** Manages containers, handles image operations, and communicates with the host OS, similar to an OS for Docker machines.

### How to install images from Docker Hub
- Use `docker pull <image-name>` to install an image from Docker Hub.

### Set default command within Docker image
- Use the `CMD` instruction in a Dockerfile to set a default command to be executed when starting a container.

### Checking container status
- Use `docker ps` to check the status of running containers, providing information like container ID, image, command, created time, status, and names.

### Remove command for unused containers
- Use `docker rm <container-id>` to remove unused containers.
- Use `docker system prune` to remove all stopped containers, unused networks, dangling images, and build cache.

### Difference between `docker kill` and `docker rm` command
- `docker kill`: Sends a termination signal to a running container, forcing it to stop immediately.
- `docker rm`: Removes a stopped container from the system.

### "bin" folder with each image
- Contains binary executable files for commands and utilities included in the image.

### Install Ubuntu image and explore Linux commands
- Install the Ubuntu image with `docker pull ubuntu`.
- Run a container from the image using `docker run -it ubuntu`.
- Explore and execute Linux commands inside the container, such as `ls`, `cd`, `pwd`, etc.

### Difference between host/normal user and root user
- **Normal User:** Limited permissions, cannot perform certain administrative tasks.
- **Root User:** Administrative privileges, can access and modify system files, install software, and make system-wide changes.

