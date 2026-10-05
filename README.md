# Project Name

A brief description of what this project does and its target audience.

---

## 📌 Repository Structure

This repository follows the standard Apache Subversion (SVN) directory layout:

*   📁 **`/trunk`** - The main line of continuous development. All code here must remain stable, compilable, and production-ready.
*   📁 **`/branches`** - Isolated development environments. Used for long-running feature development, experimental tasks, or hotfixes without disrupting the trunk.
*   📁 **`/tags`** - Immutable, read-only snapshots of the codebase at specific milestones (e.g., releases like `v1.0.0`, `v2.1.3`). **Do not commit directly to a tag.**

---

## 🚀 Getting Started (SVN Workflow)

Because Subversion is a **Centralized Version Control System (VCS)**, you must always be connected to the network/VPN to interact with the repository history.

### 1. Prerequisite Clients
*   **Windows:** Install [TortoiseSVN](https://tortoisesvn.net) for Windows Explorer integration.
*   **macOS / Linux:** Install the native CLI client via your package manager:
    ```bash
    # Ubuntu/Debian
    sudo apt install subversion
    # macOS (via Homebrew)
    brew install subversion
    ```

### 2. Initial Checkout
To download your local working copy from the central server:
```bash
svn checkout https://<your-svn-server-domain>/svn/<repo-name>/trunk local-folder-name
```

### 3. Daily Development Workflow

Always update your local environment before you begin working to prevent integration issues:
```bash
svn update
```

Make your edits or create new files. If you add a new file, tell SVN to track it:
```bash
svn add path/to/newfile.txt
```

Review your modified and staged files before committing:
```bash
svn status
```

Commit your changes directly to the central server. Every commit increments the repository's **Global Revision Number**:
```bash
svn commit -m "Brief, meaningful description of the changes made"
```

---

## ⚠️ Handling Merge Conflicts

If another developer commits changes to the same file you are modifying, SVN will flag a conflict during `svn update`. 

1. Run `svn status` to see conflicting files (marked with a **`C`**).
2. Open the file to review the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
3. Resolve the code discrepancy manually.
4. Tell SVN the conflict is resolved:
   ```bash
   svn resolve --accept working path/to/conflicting-file.txt
   ```
5. Commit the resolved file.

---

## 🌿 Branching and Tagging

SVN creates branches and tags using **"cheap copies"** (virtual references that take up zero extra server space until modified).

### Create a Feature Branch
```bash
svn copy https://server/svn/repo/trunk https://server/svn/repo/branches/feature-xyz -m "Creating feature branch for XYZ"
```

### Switch Your Local Workspace to the Branch
```bash
svn switch https://server/svn/repo/branches/feature-xyz
```

### Create a Release Tag (Read-Only)
```bash
svn copy https://server/svn/repo/trunk https://server/svn/repo/tags/v1.0.0 -m "Tagging the 1.0.0 release"
```

---

## 🔒 Ignored Files (`svn:ignore`)

Do not commit compiler outputs, build dependencies (`node_modules`, `vendor`), or local IDE configurations (`.vs`, `.idea`). 

To ignore local items, configure the `svn:ignore` property:
```bash
svn propset svn:ignore "bin
obj
*.log" .
svn commit -m "Updated repository ignore properties"
```
