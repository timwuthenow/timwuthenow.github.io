# Container Runtime Setup

Choose your preferred container runtime environment. We recommend either Docker or Podman.

## Docker Installation

=== "Windows"

    1. Install Docker Desktop:
    	- Download [Docker Desktop](https://www.docker.com/products/docker-desktop)
    	- Run the installer
    	- During installation, ensure "WSL 2" option is selected

    2. Post-installation:

    	```{ .powershell .copy }
    	docker --version
    	docker compose version
    	```

    3. Test Docker

    	``` { .powershell .copy }
    	docker run hello-world
    	```

    3. Configure WSL 2 (if not already done):
    ```{ .powershell .copy }
    wsl --install
    ```

=== "macOS"

    1. Install Docker Desktop using Homebrew:
    	```{ .sh .copy }
        	brew install --cask docker
    	```

    2. Start Docker Desktop:

    	```{ .sh .copy }
    	    open -a Docker
    	```

    3. Wait for Docker to start, then verify

    	``` { .sh .copy }
    	docker --version
    	docker compose version
    	```

    4. Test Docker

    	```{ .sh .copy}
    	docker run hello-world
    	```

    5. Optional: Add Docker completion to your shell (for zsh):

    	```{ .sh .copy }
    	echo 'zstyle ":completion:*:*:docker:*" option-stacking yes' >> ~/.zshrc
    	echo 'zstyle ":completion:*:*:docker-*:*" option-stacking yes' >> ~/.zshrc
    	```

=== "Linux"

    1. Install Docker Engine:

    	```{ .sh .copy }
    	# Add Docker's official GPG key
    	sudo apt-get update
    	sudo apt-get install ca-certificates curl gnupg
    	sudo install -m 0755 -d /etc/apt/keyrings
    	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    	sudo chmod a+r /etc/apt/keyrings/docker.gpg
    	```

    2. Add the repository to Apt sources

    	```{ .sh .copy}
    	echo \
    	  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    	  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    	  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    	```

    3. Install Docker packages
    	```{ .sh .copy}
    	sudo apt-get update
    	sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    	```

    4. Post-installation steps:

    	```{ .sh .copy }
    	# Add your user to the docker group
    	sudo usermod -aG docker $USER
    	```

    5. Apply group changes (or log out and back in)
    	```{ .sh .copy }
    	newgrp
    	```

    6. Test Docker
    	```{ .sh .copy }
    	docker run hello-world
    	```

## Podman Installation

=== "Windows"

    1. Install Podman Desktop:
    	- Download [Podman Desktop](https://podman-desktop.io/downloads/windows)
    	- Run the installer - Follow the installation wizard

    2. Verify installation:
    	```{ .powershell .copy }
    	podman --version
    	podman machine init
    	podman machine start
    	```

=== "macOS"

    1. Install Podman using Homebrew:
    ```{ .sh .copy }
    brew install podman
    ```

    2. Initialize and start Podman:

    	```{ .sh .copy }
    	# Initialize Podman machine
    	podman machine init

    	# Start Podman machine
    	podman machine start

    	# Verify installation
    	podman --version

    	# Test Podman
    	podman run hello-world
    	```

    3. Optional: Add Podman completion to your shell (for zsh):
    	```{ .sh .copy }
    	echo 'autoload -Uz compinit' >> ~/.zshrc
    	echo 'compinit' >> ~/.zshrc
    	```

=== "Linux"

    1. Install Podman:

    	```{ .sh .copy }
    	# Ubuntu/Debian
    	sudo apt-get update
    	sudo apt-get install -y podman
    	```

    2. Verify installation
    	```{ .sh .copy }
        podman --version
    	```

    3. Test Podman
        ```{ .sh .copy }
    	podman run hello-world
        ```

## Container Compose Setup

=== "Docker Compose"
Docker Compose is included with Docker Desktop for Windows and macOS.

### For Linux:

```{ .sh .copy }
# Install Docker Compose plugin
sudo apt-get update
sudo apt-get install docker-compose-plugin

    # Verify installation
    docker compose version
```

=== "Podman Compose"

    ```{ .sh .copy }
    # Install Podman Compose using pip
    pip3 install podman-compose

    # Verify installation
    podman-compose version
    ```

## Container Configuration

=== "Docker"

    Configure Docker resources (in Docker Desktop):
    1. Open Docker Desktop
    2. Go to Settings (⚙️)
    3. Recommended settings: - CPUs: At least 2 - Memory: At least 4 GB - Swap: At least 1 GB - Disk image size: At least 60 GB

=== "Podman"

    Configure Podman machine resources:

    ```{ .sh .copy } # Create a new machine with custom resources
    podman machine init --cpus 2 --memory 4096 --disk-size 60

        # Start the machine
        podman machine start
    ```

## Verify Installation

Test your container environment with a simple container:

=== "Docker"

    1. Pull and run nginx
    ```{ .sh .copy }
    docker run -d -p 8080:80 --name test-nginx nginx
    ```

    2. Check container status
    ```{ .sh .copy}
    docker ps
    ```

    3. Stop and remove the container
    ```{.sh .copy }
        docker stop test-nginx
        docker rm test-nginx
    ```

=== "Podman"

    1. Pull and run nginx
    	```{ .sh .copy }
    	podman run -d -p 8080:80 --name test-nginx nginx
    	```

    2. Check container status
    	```{.sh .copy}
    	podman ps
    	```

    3. Stop and remove the container
    	```{.sh .copy}
    	podman stop test-nginx
    	podman rm test-nginx
    	```

## Troubleshooting

=== "Docker Common issues and solutions"

    1. Reset Docker Desktop
       ```{ .sh .copy }
       docker system prune -a
       ```

    1. Check Docker status
       ```{ .sh .copy }
       docker info
       ```

    1. View Docker logs
       ```{ .sh .copy }
       docker logs <container-name>
       ```

=== "Podman common issues and solutions"

    1. Reset Podman Machine
       ```{ .sh .copy }
       podman machine stop
       podman machine rm
       podman machine init
       podman machine start
       ```

    1. Check Podman status
       ```{ .sh .copy }
       podman info
       ```
    1. View Podman logs
       ```{ .sh .copy }
       podman logs <container-name>
       ```
