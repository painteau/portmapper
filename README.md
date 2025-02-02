# PortMapper

PortMapper is a Bash script designed to efficiently manage and track port assignments. It enables users to list, add, delete, and search for registered ports while maintaining a log of changes. The script also includes backup and restore functionalities, as well as an optional REST API for remote access.

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
   git clone https://github.com/painteau/portmapper.git
   cd portmapper
   ```
2. Make the script executable and move it to a directory in your `$PATH`:
   ```bash
   chmod +x portmapper
   sudo mv portmapper /usr/local/bin/
   ```
3. Verify installation:
   ```bash
   portmapper —version
   ```

## Usage

### Listing Ports
```bash
portmapper —list
```

### Adding a Port
```bash
portmapper —add <port> <protocol> <name> [description]
```
Example:
```bash
portmapper —add 8080 TCP “Web Server” “Used for serving HTTP requests”
```

### Searching Ports
```bash
portmapper —search <keyword>
```

### Finding the Next Available Port
```bash
portmapper —next
```

### Deleting a Port
```bash
portmapper —delete <port>
```

### Backing Up the Database
```bash
portmapper —backup
```

### Restoring a Backup
```bash
portmapper —restore <backup-file>
```

### Importing Ports from a File
Supports CSV and JSON formats:
```bash
portmapper —import <file>
```

### Exporting Ports to JSON
```bash
portmapper —export <file>
```

### Running the REST API
```bash
portmapper —api 8080
```

### Syncing Ports from Docker
```bash
portmapper —docker all
```
For a specific container:
```bash
portmapper —docker <container-name>
```

## Configuration

PortMapper uses a configuration file located at `/etc/portmapper.conf`. Default values include:

- **Database file**: `/var/lib/portmapper.db`
- **Port range**: `3000-65535`
- **Log file**: `/var/log/portmapper.log`
- **Backup directory**: `/var/lib/portmapper_backups`
- **History file**: `/var/log/portmapper_history.log`

## Dependencies

Ensure the following tools are installed:
- `jq` (for JSON processing)
- `ss` (for checking active ports)

## License

This project is licensed under the MIT License.

## Contributions

Feel free to fork the repository, submit issues, or create pull requests to improve the script.

—

GitHub Repository: [PortMapper](https://github.com/painteau/portmapper)