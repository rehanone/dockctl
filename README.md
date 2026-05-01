# dockctl

`dockctl` is a lightweight Bash utility designed to manage multiple Docker Compose stacks across a system. It is specifically built to work alongside **Ansible** for automated deployments and backups, supporting private registry authentication and targeted stack management.

## Features

- 📂 **Centralized Management**: Manage all compose projects listed in a single config file.
- 🔐 **Multi-Registry Support**: Automatically performs `docker login` for multiple private registries using a secure secrets file.
- 🎯 **Targeted Actions**: Update or redeploy all stacks at once, or specify individual stacks by name.
- 🔄 **Smart Redeploy**: A `redeploy` command to restart stacks without the overhead of pulling new images.
- 🎨 **Clean Output**: Color-coded logging and silent directory navigation.

## Installation

1.  **Move the script to your path:**
    ```bash
    sudo mv dockctl /usr/local/bin/dockctl
    sudo chmod +x /usr/local/bin/dockctl
    ```

2.  **Create the configuration directory:**
    ```bash
    sudo mkdir -p /var/lib/dockctl
    ```

## Configuration

### 1. Stack Configuration (`dockctl.cfg`)
Create a file at `/var/lib/dockctl/dockctl.cfg` (or `~/.dockctl.cfg`) listing the absolute paths to your Docker Compose project directories:
```text
/docker/traefik
/docker/authelia
/docker/keycloak
/docker/filedrop
```

### 2. Registry Secrets (`.dockctl.secret`)
To handle private registries, create a secret file. The script expects the format `registry:username:password`.
```text
zot.example.link:admin:password123
ghcr.io:user:token
```

> **Security Note:** This file should be owned by `root:docker` with `0640` permissions so that only authorized users can read the credentials.

## Usage

```bash
dockctl <command> [stack_names...]
```

### Commands


| Command | Description |
| :--- | :--- |
| `update` | Performs docker login, pulls latest images, and recreates containers. |
| `redeploy` | Restarts/rebuilds containers without pulling (ideal for config changes). |
| `stop` | Stops the containers for the specified stacks. |
| `prune` | Runs `docker system prune` to clean up unused data. |
| `help` | Displays the help message. |

### Examples

**Update everything:**
```bash
dockctl update
```

**Redeploy specific stacks only:**
```bash
dockctl redeploy keycloak filedrop
```

**Stop specific stacks:**
```bash
dockctl stop traefik
```

## License
MIT
