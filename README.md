
# Docker Learning

## Deploy a Static Website on an Azure VM Using Docker

### Overview

This project demonstrates how to deploy a static website on an Azure Virtual Machine using Docker and Nginx.

The guide assumes that:
- An Azure Virtual Machine has already been provisioned and connected to.
- Docker has been successfully installed on the VM.
- You have SSH access to the VM.
- The static website application files are available in a github repository.

**Note:** This guide focuses on building a Docker image and deploying a container. VM provisioning and Docker installation are outside the scope of this exercise.

---

### Step 1: Copy the Application Files to the VM

Clone your application repository or copy the static website files into your VM.

For example:

```bash
git clone https://github.com/pravinmishraaws/Azure-Static-Website.git
```

### Step 2: Navigate to the Application Directory

Change into the directory containing your website files:

```bash
cd Azure-Static-Website
```

### Step 4: Create a Dockerfile

Create a file named `Dockerfile` in your application directory:

```bash
vi Dockerfile
```

Add the following instructions:

```dockerfile
# Use the lightweight Nginx Alpine image as the base image
FROM nginx:alpine

# Remove the default Nginx web content
RUN rm -rf /usr/share/nginx/html/*

# Copy the application files into the Nginx web directory
COPY . /usr/share/nginx/html

# Expose port 80 for HTTP traffic
EXPOSE 80
```

### Step 5: Build the Docker Image

Run the following command from the directory containing your Dockerfile:

```bash
docker build -t static-site:latest .
```

This builds a Docker image named `static-site` with the `latest` tag.

### Step 6: Verify the Docker Image

Confirm that the image was created successfully:

```bash
docker images
```

Look for `static-site` in the list of available images.

### Step 7: Run a Container

Create and start a container using the image:

```bash
docker run -d \
  --name static-site \
  -p 80:80 \
  --restart unless-stopped \
  static-site:latest
```

**Command breakdown:**

- `-d`: Runs the container in detached mode (background).
- `--name`: Assigns the container the name `static-site`.
- `-p 80:80`: Maps port 80 on the VM to port 80 inside the container.
- `--restart unless-stopped`: Automatically restarts the container unless it has been manually stopped.
- `static-site:latest`: Specifies the Docker image to use.

### Step 8: Verify the Running Container

Check that the container is running:

```bash
docker ps
```

You should see `static-site` in the list of running containers.

### Step 9: Access the Website

Open a browser and navigate to:

```text
http://20.90.12.64:80
```

If everything is configured correctly, your static website should load successfully.

**Important:** Ensure that inbound TCP port 80 and 22 is allowed in your Azure Network Security Group (NSG) and any applicable VM firewall rules.

---

### Key Concepts Practised

Through this exercise, I practised:

- Dockerfile creation and instructions.
- Pulling and using a base image from Docker Hub.
- Building custom Docker images.
- Running containers.
- Container port mapping.
- Deploying a containerised static website on an Azure VM.

