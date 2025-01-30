PortMap

PortMap is a Bash script designed to efficiently manage and track port assignments. It enables users to list, add, delete, and search for registered ports while maintaining a log of changes. The script also includes backup and restore functionalities, as well as an optional REST API for remote access.

Features
	•	Port Management: Add, modify, and delete ports with metadata.
	•	Logging & History: Keep track of all modifications.
	•	Backup & Restore: Ensures database safety with automatic and manual backups.
	•	Dependency Checking: Verifies required tools (jq, ss) are installed.
	•	REST API Support: Lightweight API to retrieve port information.
	•	Docker Integration: Sync ports from running Docker containers.

Installation
	1.	Clone the repository:

git clone https://github.com/painteau/portmap.git
cd portmap


	2.	Make the script executable and move it to a directory in your $PATH:

chmod +x portmap
sudo mv portmap /usr/local/bin/


	3.	Verify installation:

portmap --version



Usage

Listing Ports

portmap --list

Adding a Port

portmap --add <port> <protocol> <name> [description]

Example:

portmap --add 8080 TCP "Web Server" "Used for serving HTTP requests"

Searching Ports

portmap --search <keyword>

Finding the Next Available Port

portmap --next

Deleting a Port

portmap --delete <port>

Backing Up the Database

portmap --backup

Restoring a Backup

portmap --restore <backup-file>

Importing Ports from a File

Supports CSV and JSON formats:

portmap --import <file>

Exporting Ports to JSON

portmap --export <file>

Running the REST API

portmap --api 8080

Syncing Ports from Docker

portmap --docker all

For a specific container:

portmap --docker <container-name>

Configuration

PortMap uses a configuration file located at /etc/portmap.conf. Default values include:
	•	Database file: /var/lib/portmap.db
	•	Port range: 3000-65535
	•	Log file: /var/log/portmap.log
	•	Backup directory: /var/lib/portmap_backups
	•	History file: /var/log/portmap_history.log

Dependencies

Ensure the following tools are installed:
	•	jq (for JSON processing)
	•	ss (for checking active ports)

License

This project is licensed under the MIT License.

Contributions

Feel free to fork the repository, submit issues, or create pull requests to improve the script.

GitHub Repository: https://github.com/painteau/portmap