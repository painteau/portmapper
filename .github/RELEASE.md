# 🚀 How to Create a Release

This document explains how to create a new release of PortMapper using GitHub Actions.

## 📋 Prerequisites

- The version must be updated in:
  - `DEBIAN/control` (Version field)
  - `usr/local/bin/portmapper` (VERSION variable)
- The `CHANGELOG.md` should be updated with the new version notes

## 🎯 Methods to Create a Release

### Method 1: Create a Git Tag (Recommended)

This is the standard way to create releases:

```bash
# 1. Commit your changes
git add .
git commit -m "Prepare release v1.2.0"
git push

# 2. Create and push a tag
git tag v1.2.0
git push origin v1.2.0
```

**What happens:**
- The workflow automatically triggers
- Builds the `.deb` package
- Extracts release notes from `CHANGELOG.md`
- Creates a GitHub release with tag `v1.2.0`
- Uploads `portmapper_1.2.0.deb` and checksum

---

### Method 2: Manual Trigger (Workflow Dispatch)

Use this when you want to create a release without pushing a tag:

1. Go to **Actions** tab on GitHub
2. Select **"Build and Release Debian Package"** workflow
3. Click **"Run workflow"**
4. (Optional) Enter a version number, or leave empty to use `DEBIAN/control` version
5. Click **"Run workflow"** button

**What happens:**
- The workflow builds the package
- Creates a tag automatically (e.g., `v1.2.0`)
- Creates the GitHub release
- Uploads the package

---

## 📦 What Gets Released

Each release includes:

- **portmapper_X.Y.Z.deb** - The Debian package
- **portmapper_X.Y.Z.sha256** - SHA256 checksum file
- **Release notes** - Automatically extracted from `CHANGELOG.md`

---

## 🔍 Troubleshooting

### Release not created?

**Check the Actions tab** on GitHub to see workflow logs.

Common issues:

1. **Missing CHANGELOG section**
   - Ensure `CHANGELOG.md` has a section for your version: `## [1.2.0]`

2. **Permission denied**
   - The workflow uses `GITHUB_TOKEN` automatically
   - Ensure your repository settings allow Actions to create releases:
     - Go to: Settings → Actions → General → Workflow permissions
     - Select: "Read and write permissions"

3. **Version mismatch**
   - Ensure `DEBIAN/control` and `usr/local/bin/portmapper` have the same version

4. **Tag already exists**
   - If the tag already exists, delete it first:
     ```bash
     git tag -d v1.2.0
     git push origin :refs/tags/v1.2.0
     ```

---

## 🔄 Complete Release Workflow

Here's the complete process for creating a new release:

```bash
# 1. Update version in files
vim DEBIAN/control          # Update Version: field
vim usr/local/bin/portmapper  # Update VERSION variable

# 2. Update CHANGELOG
vim CHANGELOG.md            # Add new version section

# 3. Commit changes
git add DEBIAN/control usr/local/bin/portmapper CHANGELOG.md
git commit -m "Bump version to 1.2.0"
git push

# 4. Create and push tag
git tag v1.2.0 -a -m "Release version 1.2.0"
git push origin v1.2.0

# 5. Wait for GitHub Actions to complete
# 6. Check the Releases page on GitHub
```

---

## 📊 Workflow Details

### Inputs (Manual Trigger Only)

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Version to release (e.g., 1.2.0) | No | From `DEBIAN/control` |

### Outputs

- **Artifacts**: Available for 90 days in the Actions run
- **Release**: Permanent, published on the Releases page

### Permissions

The workflow requires:
- `contents: write` - To create releases and push tags

---

## ✅ Best Practices

1. **Always update CHANGELOG.md** before releasing
2. **Use semantic versioning** (MAJOR.MINOR.PATCH)
3. **Test locally** before creating a release:
   ```bash
   dpkg-deb --build . portmapper_test.deb
   dpkg -c portmapper_test.deb  # Check contents
   ```
4. **Create tags from main/master branch** only
5. **Write descriptive release notes** in CHANGELOG.md

---

## 🆘 Need Help?

- Check the [GitHub Actions documentation](https://docs.github.com/en/actions)
- Review workflow logs in the Actions tab
- Open an issue on the repository
