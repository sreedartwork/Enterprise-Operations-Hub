# Enterprise Operations Hub — Debugging Journal

This journal documents technical problems encountered while building the Enterprise Operations Hub.

Each entry should explain:

- What was being attempted
- What went wrong
- What the error meant
- How the problem was investigated
- How it was resolved
- How the solution was verified
- What was learned

The goal is not only to document successful development, but also to demonstrate a repeatable troubleshooting process.

---

## Issue 001 — VS Code `code` Command Not Found

### Date

September 2026

### Environment

- macOS
- Visual Studio Code
- zsh shell
- Git
- External Crucial X9 drive

---

### Goal

Open the Enterprise Operations Hub project in Visual Studio Code directly from Terminal.

Project directory:

```text
/Volumes/Crucial X9/Enterprise-Operations-Hub
```

The intended command was:

```bash
code .
```

---

### Problem

When the command was entered, Terminal returned:

```text
zsh: command not found: code
```

The project directory existed and Visual Studio Code was installed, but the terminal could not recognize the `code` command.

---

### What the Error Meant

The error did **not** mean that the Enterprise Operations Hub project was broken.

It also did not necessarily mean that Visual Studio Code was installed incorrectly.

The problem was that the VS Code command-line launcher had not been added to the shell's command search path.

In plain English:

Terminal understood commands such as:

```bash
cd
git
mkdir
```

but it did not yet know what:

```bash
code
```

referred to.

---

### Technical Concept — PATH

`PATH` is an environment variable used by the operating system's command-line shell.

It contains locations where the shell looks for executable commands.

When a command such as:

```bash
code .
```

is entered, the shell searches the directories contained in `PATH` for an executable named `code`.

If it cannot locate one, the shell returns:

```text
command not found
```

---

### Investigation

Visual Studio Code itself could be opened normally.

This indicated that the application existed and that the problem was specifically related to command-line access.

The VS Code Command Palette provides an option for installing its shell command.

The following command was selected from the Command Palette:

```text
Shell Command: Install 'code' command in PATH
```

---

### macOS Authorization Prompt

During installation, macOS displayed an authorization request involving:

```text
osascript
```

`osascript` is a built-in macOS command used to execute AppleScript or other Open Scripting Architecture scripts.

In this situation, Visual Studio Code was using the macOS scripting/authorization system while configuring the command-line launcher.

The authorization request was approved because it was initiated directly from the trusted Visual Studio Code installation process.

---

### Resolution

The Visual Studio Code shell command was installed into the PATH.

After installation, the project could be opened from its directory using:

```bash
code .
```

---

### Verification

Visual Studio Code successfully opened the:

```text
Enterprise-Operations-Hub
```

project directory.

The repository folders and files were visible in the VS Code Explorer.

---

### Root Cause

The Visual Studio Code command-line launcher had not yet been installed into the shell PATH.

---

### Lesson Learned

A `command not found` error does not automatically mean that the underlying application is missing or broken.

The troubleshooting process should determine whether:

1. The application is installed.
2. The executable exists.
3. The shell knows where to locate the executable.
4. The appropriate directory is included in `PATH`.

This distinction is useful when troubleshooting command-line tools on macOS, Linux, and other Unix-like systems.

---

## Issue 002 — macOS Metadata Files Appearing in Git Repository

### Date

September 2026

### Environment

- macOS
- Git
- External Crucial X9 drive
- Visual Studio Code

---

### Goal

Initialize a clean Git repository for the Enterprise Operations Hub and track only files that belong to the project.

---

### Problem

After creating the repository and project files on the external drive, macOS-generated metadata files appeared alongside project files.

Some files used names beginning with:

```text
._
```

macOS can also create:

```text
.DS_Store
```

files.

These files are operating-system metadata and are not part of the Enterprise Operations Hub source code or documentation.

---

### Why This Matters

If these files are not excluded, Git may track them.

That can create:

- Unnecessary repository changes
- Clutter in Git status
- Unrelated files in commits
- Confusing differences between computers
- A less professional repository

---

### Investigation

Git status was checked using:

```bash
git status
```

The metadata files were identified as files that should not be included in source control.

---

### Resolution

A `.gitignore` file was created in the project root.

The following patterns were added:

```text
.DS_Store
._*
```

---

### Technical Concept — `.gitignore`

A `.gitignore` file tells Git which files or file patterns should not be tracked.

For example:

```text
.DS_Store
```

tells Git to ignore macOS `.DS_Store` files.

The pattern:

```text
._*
```

tells Git to ignore files whose names begin with `._`.

---

### Verification

After creating the `.gitignore`, the repository status was checked again using:

```bash
git status
```

The unwanted macOS metadata files were no longer listed as untracked project files.

The expected project files remained available for Git tracking.

---

### Root Cause

macOS created filesystem metadata files while the project was being stored on an external drive.

Git detected those files because they existed inside the repository directory.

---

### Lesson Learned

Source-control repositories should contain project files rather than operating-system-generated metadata.

A `.gitignore` should be configured early in a project so unnecessary files are excluded before the first commit.

The broader troubleshooting principle is:

> Identify whether an unexpected file belongs to the application, the development tools, or the operating system before deciding whether it belongs in source control.

---

# Debugging Entry Template

Future issues can use the following structure:

## Issue XXX — Issue Name

### Date

Date encountered.

### Environment

Relevant technologies and environment.

### Goal

What was being attempted?

### Problem

What happened?

### Error / Symptoms

What error message or unexpected behavior appeared?

### Investigation

What was checked?

### Root Cause

Why did the problem occur?

### Resolution

How was it fixed?

### Verification

How was the fix confirmed?

### Lesson Learned

What technical concept or troubleshooting lesson should be remembered?

## Issue 003 — Power Automate Request ID Generation Failed

### Date

September 12, 2026

### Component

Power Automate / SharePoint Online

### Flow

Access Request - Initialize Request ID

### Goal

Automatically generate a human-readable Request ID after a new Access Request is created in SharePoint.

Example:

- SharePoint Item ID: `3`
- Generated Request ID: `AR-00003`

### Problem

The SharePoint trigger successfully detected the newly created item, but the **Update item** action failed.

Power Automate returned an `InvalidTemplate` error indicating that the `padLeft` template function was not defined or valid.

### Original Approach

The Request ID expression attempted to use `padLeft()` to add leading zeros to the SharePoint item ID.

The intended result was:

`3` → `00003` → `AR-00003`

### Root Cause

The `padLeft()` function was not supported in the Power Automate expression context being used.

Because the expression could not be evaluated, the Update item action failed and the Request ID remained blank.

### Resolution

Replaced the unsupported `padLeft()` logic with an expression using supported string functions:

- `concat()`
- `substring()`
- `string()`
- `length()`
- `sub()`

The new expression adds leading zeros to the SharePoint item ID and prefixes the result with `AR-`.

### Verification

Created a new SharePoint access request:

**Request Title:** Test - HR Site Access

The flow executed successfully:

1. `When an item is created` — Succeeded
2. `Update item` — Succeeded
3. SharePoint Request ID was automatically updated to `AR-00003`

### Additional Observation

The SharePoint trigger did not execute immediately during manual testing. There was a short delay before Power Automate detected the new item and completed the flow.

### Lesson Learned

A Power Automate flow can pass initial configuration but still fail at runtime if an expression uses an unsupported function.

Runtime testing is necessary to validate expressions and connector behavior.

Also, SharePoint-triggered cloud flows may have a short delay before processing newly created items.
