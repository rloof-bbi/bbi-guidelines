# Docker / Docker Desktop

Docker is an open-source platform that enables developers to automate the deployment, scaling, and management of applications using container technology. Containers package software and its dependencies into a standardized unit, ensuring consistency across different environments.

## Installation

1. Go to the [Docker download page](https://www.docker.com/) and select the AMD64 version.
2. Download and run the installer.
3. Follow the installation prompts. Enable WSL 2 integration if prompted.
4. After installation, restart your computer.
5. When a WSL terminal pops up, enter the requested key to accept.

## Basic Usage

Open a terminal and try the following commands:

```
# Check Docker version
docker --version

# Run a test container
docker run hello-world

# List running containers
docker ps

# List images
docker images
```

## Troubleshooting

## Resources

-   [Docker Documentation](https://docs.docker.com/)
-   [Docker Desktop for Windows](https://docs.docker.com/desktop/windows/install/)
