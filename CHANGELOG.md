# Changelog

All notable changes to PortMapper will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2025-12-12

### 🔒 Security

- **CRITICAL**: Fixed code injection vulnerability in configuration file loading
  - Replaced unsafe `source` command with secure parser
  - Configuration files are now validated and only specific variables are allowed
  - Prevents arbitrary code execution through malicious config files
- **Improved JSON export security** using `jq` for proper character escaping
  - Prevents JSON injection attacks
  - Ensures valid JSON output even with special characters in data
- **Enhanced API security**
  - Added input validation for API port number
  - Proper HTTP request parsing
  - Better error handling for malformed requests
  - CORS headers for controlled access

### 🐛 Bug Fixes

- **CRITICAL**: Completed missing `main()` function implementation
  - The script was non-functional due to incomplete argument parsing
  - Added full command-line argument handling for all supported operations
  - Proper parameter validation before execution
- **Fixed port detection false positives**
  - Improved regex pattern to prevent port 80 matching when checking for 8080
  - Changed from `:$port ` to `[:.]${port}[[:space:]]` for accurate matching
- **Fixed Docker port parsing**
  - Now handles all Docker port formats: `0.0.0.0:8080->80/tcp`, `:::8080->80/tcp`, `8080->80/tcp`
  - Improved extraction of external and internal ports
  - Better error handling when ports cannot be added
- **Removed problematic `set -e`**
  - Was causing unexpected script termination
  - Replaced with explicit error checking throughout the codebase

### ✨ Added

- **File locking mechanism** using `flock`
  - Prevents concurrent access issues and database corruption
  - Automatic lock acquisition for write operations
  - Lock release on script exit via trap
- **Port number validation**
  - Validates port is a number
  - Checks port is in valid range (1-65535)
  - Verifies port is within configured range (START_PORT to END_PORT)
- **Conditional dependency checking**
  - `jq` is only checked when needed (export/import operations)
  - `docker` is only checked for Docker sync operations
  - Reduces unnecessary dependency warnings
- **Improved error messages**
  - More descriptive error messages throughout the script
  - Better guidance for users when commands fail
- **Import functionality** for CSV and JSON files
  - Allows bulk import of port configurations
  - Validates imported data before adding to database

### 🔄 Changed

- **Version synchronized** to 1.2.0 across all files
  - Script VERSION variable
  - DEBIAN control file
  - Updated README documentation
- **Improved configuration loading**
  - Safer parsing with whitelist of allowed variables
  - Better handling of missing configuration files
  - Uses defaults when config file is absent
- **Enhanced Docker port synchronization**
  - More robust parsing of Docker port mappings
  - Better handling of edge cases
  - Counts newly synced ports for user feedback
- **Better API implementation**
  - Proper HTTP response codes (200, 404, 405)
  - Structured endpoint handling
  - Content-Type headers for JSON responses

### 📝 Documentation

- **Updated README.md**
  - Added new security features to features list
  - Enhanced security notice with detailed recommendations
  - Better description of file locking and port validation
- **Created CHANGELOG.md** (this file)
  - Comprehensive changelog following industry standards
  - Detailed categorization of changes

### 🔧 Technical Improvements

- **Better code organization**
  - Functions are more modular and focused
  - Consistent error handling patterns
  - Improved variable naming and comments
- **Enhanced logging**
  - More informative log messages
  - Better error tracking in log files
  - Warnings for non-critical issues

---

## [1.1.6] - Prior Release

### Changed
- Minor version bump for package consistency

---

## [1.1.5] - Initial Tracked Release

### Features
- Basic port management (add, modify, delete, list)
- Search functionality
- Backup and restore capabilities
- Docker container port synchronization
- REST API for remote access
- JSON export functionality
- Configuration file support
- Logging and history tracking

---

## Migration Guide

### Upgrading from 1.1.x to 1.2.0

**No breaking changes** - This is a backwards-compatible update.

#### Recommended Steps:

1. **Backup your database** before upgrading:
   ```bash
   portmapper --backup
   ```

2. **Replace the script**:
   ```bash
   chmod +x usr/local/bin/portmapper
   sudo cp usr/local/bin/portmapper /usr/local/bin/
   ```

3. **Verify the installation**:
   ```bash
   portmapper --version  # Should show 1.2.0
   ```

4. **Test basic operations**:
   ```bash
   portmapper --list
   portmapper --next
   ```

#### Configuration File Security:

If you have a custom `/etc/portmapper.conf`:
- Review its contents to ensure no executable code
- The new version only accepts variable assignments
- Arbitrary bash code will be ignored (security improvement)

#### What Changed Under the Hood:

- Configuration files are now parsed more securely
- Port validation is more strict (prevents invalid ports)
- File locking prevents concurrent modification issues
- API has better error handling

---

## Security Advisories

### CVE-Style Advisory (Informal)

**Severity**: High
**Affected Versions**: < 1.2.0
**Fixed in**: 1.2.0

**Vulnerability**: Configuration file code injection

**Description**: Previous versions used `source` to load configuration files, allowing arbitrary code execution if an attacker could modify `/etc/portmapper.conf`.

**Impact**: An attacker with write access to the configuration file could execute arbitrary commands with the privileges of the user running portmapper.

**Remediation**: Upgrade to version 1.2.0 or later, which implements secure configuration parsing.

---

## Contributors

- **Painteau** - Original author and maintainer
- **Claude** - Security audit and bug fixes (v1.2.0)

---

## Links

- [GitHub Repository](https://github.com/painteau/portmapper)
- [Issue Tracker](https://github.com/painteau/portmapper/issues)
- [License](LICENSE)
