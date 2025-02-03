# Ubuntu Environment Setup Guide for Apache Kogito

This guide provides step-by-step instructions for setting up your development environment for Apache Kogito on Ubuntu. The setup includes Docker, Java 17, Maven, and Visual Studio Code.

## Docker Installation

### 1. Remove Conflicting Packages

First, remove any old or conflicting Docker installations to ensure a clean setup:

```sh
sudo apt remove docker docker-engine docker.io containerd runc
```

### 2. Install Prerequisites

Install necessary packages to allow apt to use repositories over HTTPS:

```sh
sudo apt install -y \
 apt-transport-https \
 ca-certificates \
 curl \
 gnupg \
 lsb-release
```

### 3. Set Up Docker Repository

Add Docker's official GPG key to ensure package authenticity:

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Add the stable Docker repository to APT sources:

```sh
echo \
 "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
 $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 4. Install Docker Engine

Update package index and install the latest version of Docker Engine and containerd:

```sh
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### 5. Configure Docker User Permissions

Add your user to the docker group to run Docker commands without sudo:

```sh
sudo usermod -aG docker $USER
```

### 6. Configure Docker Service

Start and enable the Docker service to run on system startup:

```sh
sudo systemctl start docker
sudo systemctl enable docker
```

## Docker Compose Installation

### 1. Install Docker Compose

Download and install the latest stable version of Docker Compose:

```sh
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
```

Make the binary executable:

```sh
sudo chmod +x /usr/local/bin/docker-compose
```

Verify the installation:

```sh
docker-compose --version
```

## Visual Studio Code Installation

Install Visual Studio Code, a powerful IDE with excellent Docker and Java support. This benefit is only grown more within the Apache KIE Community with provided plugins to add to the power of the tool!

```sh
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt update
sudo apt install -y code
```

## Java Development Environment

### 1. Install OpenJDK 17

Install the Java Development Kit version 17:

```sh
sudo apt install -y openjdk-17-jdk
java --version
```

### 2. Install and Configure Maven

Download and install Apache Maven 3.9.7:

```sh
wget https://dlcdn.apache.org/maven/maven-3/3.9.7/binaries/apache-maven-3.9.7-bin.tar.gz
```

Extract Maven to the /opt directory:

```sh
sudo tar xf apache-maven-3.9.7-bin.tar.gz -C /opt
```

Create a symbolic link for easier version management:

```sh
sudo ln -s /opt/apache-maven-3.9.7 /opt/maven
```

Confirm the Java that you're using with:

```sh
sudo update-alternatives --list java
```

```log
/usr/lib/jvm/java-17-openjdk-amd64/bin/java
```

!!! tip

    Make sure you understand which version of Java you're using, if you're using an arm64 deployment of Ubuntu, then you will probably have /usr/lib/jvm/java-17-openjdk-arm64/bin/java instead of -amd64 as seen in the message above.

Configure environment variables for Java and Maven in your ~/.bashrc:

```sh
export M2_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```

Load the new environment variables:

```sh
source ~/.bashrc
```

Verify Maven installation:

```sh
mvn -version
```

## Next Steps

After completing this setup:

1. Log out and log back in for group changes to take effect
2. Test Docker installation by running: `docker run hello-world`
3. Install recommended VS Code extensions for Java and Docker development
4. Configure Maven settings if working with private repositories

## Troubleshooting Tips

- If Docker commands fail, ensure your user is properly added to the docker group
- If Maven isn't recognized, verify the environment variables are properly set
- For VS Code extensions, ensure Java Extension Pack is installed for full Java support
