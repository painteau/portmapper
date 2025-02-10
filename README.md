# 🚀 PortMapper

PortMapper is a **Bash script** designed to efficiently manage and track **port assignments**. It enables users to list, add, delete, and search for registered ports while maintaining a **log of changes**. The script also includes **backup and restore** functionalities, as well as an **optional REST API** for remote access.

---

## ⭐ Features

- 📌 **Port Management**: Add, modify, and delete ports with metadata.
- 📜 **Logging & History**: Keep track of all modifications.
- 🔄 **Backup & Restore**: Ensures database safety with automatic and manual backups.
- ✅ **Dependency Checking**: Verifies required tools (`jq`, `ss`) are installed.
- 🌐 **REST API Support**: Lightweight API to retrieve port information.
- 🐳 **Docker Integration**: Sync ports from running Docker containers.

---

## 📌 Prerequisites

Ensure the following dependencies are installed:
- `jq` (for JSON processing)
- `ss` (for checking active ports)
- **Docker** (for syncing container ports, optional)

---

## 🛠 Setup & Installation

### **1️⃣ Clone the Repository**
```bash
git clone https://github.com/painteau/portmapper.git
cd portmapper
```

### **2️⃣ Install PortMapper**
```bash
chmod +x portmapper
sudo mv portmapper /usr/local/bin/
```

### **3️⃣ Verify Installation**
```bash
portmapper --version
```

---

## 🔨 Running PortMapper Locally

| Command | Description |
|---------|-------------|
| `portmapper --list` | List all registered ports |
| `portmapper --add <port> <protocol> <name> [description]` | Add a new port with metadata |
| `portmapper --search <keyword>` | Search for a port by keyword |
| `portmapper --next` | Find the next available port |
| `portmapper --delete <port>` | Delete a registered port |
| `portmapper --backup` | Create a backup of the port database |
| `portmapper --restore <backup-file>` | Restore a backup file |
| `portmapper --import <file>` | Import ports from a CSV or JSON file |
| `portmapper --export <file>` | Export ports to JSON format |
| `portmapper --api 8080` | Start the REST API on port 8080 |
| `portmapper --docker all` | Sync ports from all Docker containers |
| `portmapper --docker <container-name>` | Sync ports from a specific container |

---

## ⚙ Configuration

PortMapper uses a configuration file located at `/etc/portmapper.conf`. Default values include:

| Option            | Description                        |
|------------------|--------------------------------|
| **Database file**  | `/var/lib/portmapper.db`       |
| **Port range**    | `3000-65535`                    |
| **Log file**      | `/var/log/portmapper.log`       |
| **Backup dir**    | `/var/lib/portmapper_backups`   |
| **History file**  | `/var/log/portmapper_history.log` |

---

## 🔧 Troubleshooting

- Ensure dependencies (`jq`, `ss`) are installed.
- Check logs for errors:
  ```bash
  tail -f /var/log/portmapper.log
  ```
- If using the REST API, ensure port `8080` is accessible.

---

## 📜 License

This project is licensed under the **MIT License**.

---

## ⚠ Security Notice

Ensure that you expose the API securely and restrict access if necessary when deploying in a production environment.

---

## 💡 Contributing

1️⃣ **Fork** the repository on [GitHub](https://github.com/painteau/portmapper)  
2️⃣ **Create a new branch** (`feature-branch`)  
3️⃣ **Commit your changes**  
4️⃣ **Push to your branch and create a pull request**  

For major changes, please open an **issue** first to discuss the proposed modifications.

---

## 📬 Contact

For issues or improvements, open an issue on GitHub or contact **Painteau**.

