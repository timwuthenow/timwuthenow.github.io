# Java Installation and Configuration

=== "Windows"

    1. Install Java using Chocolatey:

    	```{ .powershell .copy }
    	choco install temurin17
    	```

    2. JAVA_HOME (Run in PowerShell as Administrator):

    	```{ .powershell .copy }
        	[Environment]::SetEnvironmentVariable(
            "JAVA_HOME",
            "C:\Program Files\Eclipse Adoptium\jdk-17.0.10.7-hotspot",
            [System.EnvironmentVariableTarget]::Machine)
        ```

    3. Add Java to PATH (Run in PowerShell as Administrator):

        ```{ .powershell .copy }
        [Environment]::SetEnvironmentVariable(
            "Path",
            [Environment]::GetEnvironmentVariable("Path", "Machine") + ";%JAVA_HOME%\bin",
            [System.EnvironmentVariableTarget]::Machine)
        ```

    4. Verify installation (open a new PowerShell window):

        ```{ .powershell .copy }
        java --version
        echo $env:JAVA_HOME
        ```

=== "macOS"

    1. Install Java:
    	```{ .sh .copy }
        brew install --cask temurin17
        ```

    2. Add Java environment variables to your shell configuration (for zsh):
        ```{ .sh .copy }
        echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 17)' >> ~/.zshrc
        echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.zshrc
        ```

    3. Create a helper function to switch Java versions (optional):
        ```{ .sh .copy }
        echo 'function setjdk() {
            export JAVA_HOME=$(/usr/libexec/java_home -v $1)
            echo "JAVA_HOME set to $JAVA_HOME"
            java -version
        }' >> ~/.zshrc
        ```

    4. Reload shell configuration:
        ```{ .sh .copy }
        source ~/.zshrc
        ```

    5. Verify installation:
        ```{ .sh .copy }
        java --version
        echo $JAVA_HOME
        ```

=== "Linux"

    1. Install Java:
    	```{ .sh .copy }
        sudo apt-get update
        sudo apt-get install -y temurin-17-jdk
        ```

    2. Set JAVA_HOME and update PATH (for bash):
        ```{ .sh .copy }
        echo 'export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:/bin/java::")' >> ~/.bashrc
        echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
        ```

        For zsh users:
        ```{ .sh .copy }
        echo 'export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:/bin/java::")' >> ~/.zshrc
        echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.zshrc
        ```

    3. Reload shell configuration:
        ```{ .sh .copy }
        # For bash
        source ~/.bashrc

        # For zsh
        source ~/.zshrc
        ```

    4. Verify installation:
        ```{ .sh .copy }
        java --version
        echo $JAVA_HOME
        ```

## Troubleshooting

=== "Windows"

    If Java command is not recognized after installation:
    	1. Open System Properties (Win + R, type `sysdm.cpl`)
    	2. Click "Environment Variables"
    	3. Verify JAVA_HOME exists and points to correct directory
    	4. Verify Path includes `%JAVA_HOME%\bin`
    	5. Open new command prompt to test

=== "macOS"

    - "Java command is not recognized":

    ```{ .sh .copy }
    ls -l /Library/Java/JavaVirtualMachines/ # Verify Java installation
    ```

    - Verify JAVA_HOME

    ```{.sh .copy}
    /usr/libexec/java_home -V
    ```

=== "Linux"

    - If Java command is not recognized:

    ```{ .sh .copy }
    # Check Java alternatives
    	sudo update-alternatives --config java

        # Verify installation path
        which java
        readlink -f $(which java)
    ```

## Additional Configuration Tips

=== "Windows"

    - Create a `.gitconfig` file in your home directory:

        ```{ .powershell .copy }
        notepad "$env:USERPROFILE\.gitconfig"
        ```

    - Add basic Git configuration:
        ```{ .ini .copy }
        [user]
            name = Your Name
            email = your.email@example.com
        [core]
            autocrlf = true
            editor = notepad
        ```

=== "macOS"

    - Recommended aliases for your `.zshrc`:

    	```{ .sh .copy }
    	# Java and Maven helpers
    	echo 'alias j17="setjdk 17"' >> ~/.zshrc
    	echo 'alias mvnc="mvn clean"' >> ~/.zshrc
    	echo 'alias mvnp="mvn package"' >> ~/.zshrc
    	echo 'alias mvni="mvn install"' >> ~/.zshrc
    	```

    - Recommended Git helpers
    	```{.sh .copy}
        echo 'alias gs="git status"' >> ~/.zshrc
        echo 'alias gp="git pull"' >> ~/.zshrc
        echo 'alias gc="git commit"' >> ~/.zshrc
        ```

=== "Linux"

    - Java and Maven helpers
    	```{ .sh .copy }
        echo 'alias j17="export JAVA_HOME=/usr/lib/jvm/temurin-17-jdk"' >> ~/.bashrc
        echo 'alias mvnc="mvn clean"' >> ~/.bashrc
        echo 'alias mvnp="mvn package"' >> ~/.bashrc
        echo 'alias mvni="mvn install"' >> ~/.bashrc
        ```

    - Git helpers
        ```{ .sh .copy }
        echo 'alias gs="git status"' >> ~/.bashrc
        echo 'alias gp="git pull"' >> ~/.bashrc
        echo 'alias gc="git commit"' >> ~/.bashrc
        ```
