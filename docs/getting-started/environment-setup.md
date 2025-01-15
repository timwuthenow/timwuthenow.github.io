# Environment Setup

This guide will help you set up your development environment for {{ product.name }}. We'll cover installation and configuration of all required tools and dependencies.

## Prerequisites Overview

The following tools are required for development:

- Java 17 (Eclipse Temurin, Amazon Corretto, or other community distribution)
- Maven 3.9.6 or higher
- Git
- Container runtime (Docker or Podman)
- Kubernetes tools (kubectl)
- OpenShift CLI (oc)
- VS Code with extensions

## Package Manager Setup

If possible, to simplify the configurations, we recommend the usage of Package Managers like Homebrew, Chocolatey, or Apt to get the required elements for your environment. This is not required, but greatly simplifies the process.

=== "Package Manager"

    === "Windows (Chocolatey)"

    	1.  Open PowerShell as Administrator (Right-click, "Run as Administrator")

        2. Install Chocolatey:

        	```{ .powershell .copy }
       		Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
        	```

        3. Verify installation:

        	```{ .powershell .copy }
        	choco --version
        	```

    === "macOS (Homebrew)"

    	1.  Install Homebrew:
    	    	```{ .sh .copy }
    	    	/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    	    	```

    	2. Add Homebrew to your PATH:

    	    1. For Apple Silicon Macs
    	        	```{ .sh .copy}
    				echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
    	        	```

    		1. For Intel Macs
    				```{ .sh .copy }
    	        	echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zshrc
    				```



    	3. Reload your shell configuration:
    	        ```{ .sh .copy }
    	        source ~/.zshrc
    	        ```

    === "Linux (apt)"

    Linux generally comes with its package manager, but ensure it's up to date:

    ```{ .sh .copy }
        sudo apt update && sudo apt upgrade
    ```

## Initial Java Setup with Maven

We recommend using Eclipse Temurin (formerly AdoptOpenJDK) 17 for development:

=== "Java"

    === "Homebrew"
        ```{ .sh .copy }
        # Install Homebrew if not already installed
        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

        # Install Java
        brew install --cask temurin17

        # Install Maven
        brew install maven
        ```

    === "Linux"
        ```{ .sh .copy }
        # Install Java
        sudo apt-get update
        sudo apt-get install -y temurin-17-jdk

        # Install Maven
        sudo apt-get install maven
        ```

    === "Windows"
        ```{ .powershell .copy }
        # Using Chocolatey
        choco install temurin17
        choco install maven
        ```

=== "Using SDKMAN!"

    === "macOS"
        ```{ .sh .copy }
        # Install SDKMAN!
        curl -s "https://get.sdkman.io" | bash
        source "$HOME/.sdkman/bin/sdkman-init.sh"

        # Install Java and Maven
        sdk install java 17.0.10-tem
        sdk install maven 3.9.9
        ```

    === "Linux"
        ```{ .sh .copy }
        # Install SDKMAN!
        curl -s "https://get.sdkman.io" | bash
        source "$HOME/.sdkman/bin/sdkman-init.sh"

        # Install Java and Maven
        sdk install java 17.0.10-tem
        sdk install maven 3.9.9
        ```

## Container Runtime

=== "Docker"

    === "macOS"
        ```{ .sh .copy }
        brew install --cask docker
        ```

    === "Linux"
        ```{ .sh .copy }
        curl -fsSL https://get.docker.com -o get-docker.sh
        sudo sh get-docker.sh
        ```

    === "Windows"
        Download and install [Docker Desktop](https://www.docker.com/products/docker-desktop)

=== "Podman"

    === "macOS"
        ```{ .sh .copy }
        brew install podman
        podman machine init
        podman machine start
        ```

    === "Linux"
        ```{ .sh .copy }
        sudo apt-get update
        sudo apt-get install -y podman
        ```

    === "Windows"
        Download and install [Podman Desktop](https://podman-desktop.io/downloads)
