When you pull an image from Docker Hub, the process is a coordinated effort where dockerd acts as the orchestrator and containerd acts as the manager of the actual content. [1] 
Here is the breakdown of the process:
## 1. The Architecture Roles

* dockerd (Docker Daemon): The high-level interface. It handles API requests, authentication with Docker Hub, and manages high-level features like networking and volumes.
* containerd: The industry-standard container runtime. It manages the entire container lifecycle, including image transfer, storage, and execution.

## 2. The Step-by-Step Pull Flow
When you run docker pull nginx:latest:

   1. CLI to dockerd: The Docker CLI sends a REST API request to the dockerd daemon.
   2. dockerd to Registry: dockerd communicates with Docker Hub to check for the image, handle credentials, and initiate the download.
   3. dockerd to containerd: While dockerd initiates the pull, it instructs containerd to actually fetch the image layers.
   4. Content Management: containerd pulls the layers, unpacks them into a snapshotter (filesystem), and stores them in its internal content store. [2, 3] 

## Summary

* Initiator & Authenticator: dockerd
* Manager of Layers & Storage: containerd
