# Developer's Guide: How to Deploy and Manage Applications with Kubernetes

This guide provides instructions on how to deploy and manage applications using Kubernetes covering only the essential steps.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Structure Setup](#project-structure-setup)
- [Prepare the Application Image](#prepare-the-application-image)
- [Deploy Application with Kubernetes](#deploy-application-with-kubernetes)
    - [Set Up Kubernetes Cluster](#set-up-kubernetes-cluster)
    - [Deploy Image to Kubernetes](#deploy-image-to-kubernetes)
    - [Access the Application](#access-the-application)

---

### Prerequisites

1. Install Docker.
2. Set up a Docker Hub account.
3. Install kubectl.
4. Install Minikube (or set up access to a managed Kubernetes service).

---

### Project Structure Setup

1. Create the directories for your project:

    ```bash
    > mkdir quickstart_docker
    > mkdir quickstart_docker/application
    > mkdir quickstart_docker/docker
    > mkdir quickstart_docker/docker/application
 
    ```
2. Use the directories as follows for clarity and standard purposes:

    ```bash
    quickstart_docker/   # Root project directory
    ├── application/     # Application code directory
    └── docker/          # Docker-related files
        └── application/ # Dockerfile for the application
    ```

---

### Prepare the Application Image

To prepare an application image and then deploy it with Kubernetes, follow these steps:

1. Ensure your application is inside the **`quickstart_docker/application`** directory.
<!-- Validate location with developer -->

2. Create the **`application.py`** file inside the **`quickstart_docker/application`** directory.
3. Copy and paste the following code in the **`application.py`** file:

    ```python
    import http.server
    import socketserver

    PORT = 8000

    Handler = http.server.SimpleHTTPRequestHandler

    httpd = socketserver.TCPServer(("", PORT), Handler)

    print("serving at port", PORT)
    httpd.serve_forever()

    ```

4. Create a pre-built image from Docker Hubhe that contains Python, an operating system, and the required dependencies for your application environment:

    1. Create the **`Dockerfile`** inside the **`quickstart_docker/docker/application`** directory.
    2. Copy and paste the following code in the **`Dockerfile`** file:

    ```dockerfile
    # Use a base image from Docker Hub
    FROM python:3.5

    # Set the working directory in the container
    WORKDIR /app

    # Copy application code into the container
    COPY ./application /app

    # Expose port 8000 to the outside world
    EXPOSE 8000

    # Run the application when the container launches
    CMD ["python", "/app/application.py"]

    ```

    3. Build the Docker Image with the following command:
        ```bash
        > docker build . -f docker/application/Dockerfile -t exampleapp
        ```

        <table border="1" style="background-color: lightgray;">
          <tr>
           <td>
            <p><strong>Note</strong>: The description of the arguments is:</p>
            <ul>
                <li><strong><code>.</code></strong>: Represents the working directory and the build context.</li>
                <li><strong><code>-f docker/application/Dockerfile</code></strong>: Specifies the Dockerfile location.</li>
                <li><strong><code>-t exampleapp</code></strong>: Tags the image for easier reference.</li>
            </ul>
           </td>
          </tr>
        </table>
    4. List your Docker images to verify:
        ```bash
        > docker images
        ```

        Example output:
        ```bash
        REPOSITORY    TAG       IMAGE ID        CREATED         SIZE
        exampleapp    latest    83ioe0edc28a    2 seconds ago   154MB
        python        3.6       05stv8636w3f    6 weeks ago     154MB

        ```
    5. Push your built image to your Docker repository.

<table border="1" style="background-color: lightgray;">
    <tr>
        <td>
            <p><strong>Note</strong>: For more details on Docker images, refer to the <a href="https://docs.docker.com/reference/dockerfile/">Docker documentation</a>.</p>
        </td>
    </tr>
</table>

---

### Deploy Application with Kubernetes

To deploy an application with Kubernetes, follow the steps in these subsections.
- [Set Up Kubernetes Cluster](#set-up-kubernetes-cluster)
- [Deploy Image to Kubernetes](#deploy-image-to-kubernetes)
- [Access the Application](#access-the-application)

#### Set Up Kubernetes Cluster
WIP

#### Deploy Image to Kubernetes
WIP

#### Access the Application
WIP