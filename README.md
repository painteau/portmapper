# PortMap

PortMap is a Bash script designed to efficiently manage and track port assignments. It enables users to list, add, delete, and search for registered ports while maintaining a log of changes. The script also includes backup and restore functionalities, as well as an optional REST API for remote access.

## Features

- **Port Management**: Add, modify, and delete ports with metadata.
- **Logging & History**: Keep track of all modifications.
- **Backup & Restore**: Ensures database safety with automatic and manual backups.
- **Dependency Checking**: Verifies required tools (`jq`, `ss`) are installed.
- **REST API Support**: Lightweight API to retrieve port information.
- **Docker Integration**: Sync ports from running Docker containers.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/painteau/portmap.git
   cd portmap
   ```
2. Make the script executable and move it to a directory in your `$PATH`:
   ```bash
   chmod +x portmap
   sudo mv portmap /usr/local/bin/
   ```
3. Verify installation:
   ```bash
   portmap --version
   ```

## Usage

### Listing Ports
```bash
portmap --list
```

### Adding a Port
```bash
portmap --add <port> <protocol> <name> [description]
```
Example:
```bash
portmap --add 8080 TCP "Web Server" "Used for serving HTTP requests"
```

### Searching Ports
```bash
portmap --search <keyword>
```

### Finding the Next Available Port
```bash
portmap --next
```

### Deleting a Port
```bash
portmap --delete <port>
```

### Backing Up the Database
```bash
portmap --backup
```

### Restoring a Backup
```bash
portmap --restore <backup-file>
```

### Importing Ports from a File
Supports CSV and JSON formats:
```bash
portmap --import <file>
```

### Exporting Ports to JSON
```bash
portmap --export <file>
```

### Running the REST API
```bash
portmap --api 8080
```

### Syncing Ports from Docker
```bash
portmap --docker all
```
For a specific container:
```bash
portmap --docker <container-name>
```

## Configuration

PortMap uses a configuration file located at `/etc/portmap.conf`. Default values include:

- **Database file**: `/var/lib/portmap.db`
- **Port range**: `3000-65535`
- **Log file**: `/var/log/portmap.log`
- **Backup directory**: `/var/lib/portmap_backups`
- **History file**: `/var/log/portmap_history.log`

## Dependencies

Ensure the following tools are installed:
- `jq` (for JSON processing)
- `ss` (for checking active ports)

## License

This project is licensed under the MIT License.

## Contributions

Feel free to fork the repository, submit issues, or create pull requests to improve the script.

---

GitHub Repository: [PortMap](https://github.com/painteau/portmap)