# Cloud Command Line Tools

## Kubernetes CLI (kubectl)

=== "macOS"

    1. Using Homebrew (recommended):
    ```{ .sh .copy }
    brew install kubectl
    ```

    2. Manual installation:
    ```{ .sh .copy }
    Download kubectl
    curl -LO "https://dl.k8s.io/release/v1.29.2/bin/darwin/arm64/kubectl"
    ```

    5. Make kubectl executable
    ```{ .sh .copy }
    chmod +x ./kubectl
    ```

    6. Move kubectl to a directory in your PATH
    ```{ .sh .copy }
    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

=== "Linux"

    1. Using package manager (Ubuntu/Debian):
    ```{ .sh .copy } # Add Kubernetes apt repository
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
    sudo apt-get update
    sudo apt-get install -y kubectl
    ```

    2. Manual installation:
    ```{ .sh .copy }
    # Download kubectl
    curl -LO "https://dl.k8s.io/release/v1.29.2/bin/linux/amd64/kubectl"
    ```

    3. Make kubectl executable
    ```{ .sh .copy }
    chmod +x ./kubectl
    ```

    # Move kubectl to a directory in your PATH
    ```{ .sh .copy }
    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

=== "Windows"

    1. Using Chocolatey (recommended):
    ```{ .powershell .copy }
    	choco install kubernetes-cli
    ```

    2. Manual installation:
    ```{ .powershell .copy }
    # Create directory for kubectl
    New-Item -Path 'C:\Program Files\kubectl' -Type Directory
    ```

    3. Download kubectl
    ```{ .powershell .copy }
    curl.exe -LO "https://dl.k8s.io/release/v1.29.2/bin/windows/amd64/kubectl.exe"
    ```

    4. Move kubectl to the created directory
    ```{ .powershell .copy }
    Move-Item .\kubectl.exe 'C:\Program Files\kubectl\'
    ```

    5. Add to PATH
    ```{ .powershell .copy }
    $env:Path += ";C:\Program Files\kubectl"
    [Environment]::SetEnvironmentVariable(
        "Path",
        [Environment]::GetEnvironmentVariable("Path", [System.EnvironmentVariableTarget]::Machine) + ";C:\Program Files\kubectl",
        [System.EnvironmentVariableTarget]::Machine)
    ```

## OpenShift CLI (oc)

=== "Windows"

    1. Using web console:
    	- Log into your OpenShift web console
    	- Click ? icon in the top right
    	- Select "Command Line Tools"
    	- Download Windows oc client
    	- Extract the archive

    1. Create directory for OpenShift CLI
    ```{ .powershell .copy }
    New-Item -Path 'C:\Program Files\OpenShift' -Type Directory
    ```

    2. Move oc.exe to the created directory
    ```{ .powershell .copy }
        Move-Item .\oc.exe 'C:\Program Files\OpenShift\'
    ```

    3. Add to PATH
    	```{ .powershell .copy }
        $env:Path += ";C:\Program Files\OpenShift"
        [Environment]::SetEnvironmentVariable(
        "Path",
        [Environment]::GetEnvironmentVariable("Path", [System.EnvironmentVariableTarget]::Machine) + ";C:\Program Files\OpenShift",
        [System.EnvironmentVariableTarget]::Machine)
    	```

=== "macOS"

    1. Using Homebrew:
    ```{ .sh .copy }
        brew install openshift-cli
    ```

    2. Manual installation:

        - Log into your OpenShift web console
        - Click ? icon in the top right
        - Select "Command Line Tools"
        - Download macOS oc client
    	- Extract the downloaded archive

    		```{ .sh .copy }
            # Extract the downloaded archive
            tar xvf oc.tar.gz

            # Make oc executable
            chmod +x ./oc

            # Move to a directory in your PATH
            sudo mv ./oc /usr/local/bin/oc
            ```

=== "Linux"

    1. Manual installation:
    - Log into your OpenShift web console
    - Click ? icon in the top right
    - Select "Command Line Tools"
    - Download Linux oc client
    - Extract the downloaded archive

    ```{ .sh .copy }
    # Extract the downloaded archive
    tar xvf oc.tar.gz

    # Make oc executable
    chmod +x ./oc

    # Move to a directory in your PATH
    sudo mv ./oc /usr/local/bin/oc
    ```

## Verification and Configuration

Verify the installations:

```{ .sh .copy }
# Verify kubectl
kubectl version --client

# Verify oc
oc version --client
```

### kubectl Configuration

```{ .sh .copy }
# Create kubectl config directory if it doesn't exist
mkdir -p ~/.kube

# Set KUBECONFIG environment variable
export KUBECONFIG=~/.kube/config
```

### OpenShift Login

```{ .sh .copy }
# Login to OpenShift cluster
oc login --token=<token> --server=https://api.cluster-url:6443

# View available projects
oc projects

# Switch to a specific project
oc project <project-name>
```

!!! tip

    Store your OpenShift login token securely. You can get a new token from the OpenShift web console under your profile → Copy login command.

## Shell Completion

=== "Bash"

    ```{ .sh .copy }
    # kubectl completion
    echo 'source <(kubectl completion bash)' >>~/.bashrc

    # oc completion
    echo 'source <(oc completion bash)' >>~/.bashrc
    ```

=== "Zsh"

    ```{ .sh .copy }
    # kubectl completion
    echo '[[$commands[kubectl]]] && source <(kubectl completion zsh)' >>~/.zshrc

    # oc completion
    echo '[[ $commands[oc] ]] && source <(oc completion zsh)' >>~/.zshrc
    ```

=== "PowerShell"

    ```{ .powershell .copy }
    # kubectl completion
    kubectl completion powershell | Out-String | Invoke-Expression

    # oc completion
    oc completion powershell | Out-String | Invoke-Expression
    ```

## Common Issues and Troubleshooting

!!! warning

    If you're behind a corporate proxy, you might need to configure proxy settings for both kubectl and oc.

Common troubleshooting steps:

```{ .sh .copy }
# Check kubectl context
kubectl config current-context

# Check oc login status
oc whoami

# View cluster info
kubectl cluster-info
oc cluster-info

# Check connection to cluster
kubectl get nodes
oc get nodes
```

!!! tip

    Keep your CLI tools up to date with the cluster version to avoid compatibility issues. You can check the required versions in your cluster's documentation.
