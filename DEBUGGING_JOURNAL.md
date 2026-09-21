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

Yes. This is exactly the kind of problem that belongs in the **DEBUGGING_JOURNAL.md**, because we had a real issue, tried multiple approaches, identified the cause, and got a working solution.

I'd make this **Issue 003**. Add this to `DEBUGGING_JOURNAL.md`:

````markdown
## Issue 004 — Power Apps Requester Field Did Not Auto-Populate Current User

### Date

September 13, 2026

### Component

Power Apps / SharePoint Online

### Problem

The `Requester` field in the Access Requests Power Apps form needed to automatically identify the currently signed-in Microsoft 365 user when a new request was created.

The SharePoint `Requester` column is a Person column connected to the `Access Requests` list.

The generated Power Apps Combo Box was:

`DataCardValue3`

Its Items property was:

```powerfx

Choices([@'Access Requests'].'Requester')

```
````

However, when clicking **+ New**, the Requester field remained blank and displayed:

`Find items`

---

### First Attempt — Lookup by Email

The initial approach attempted to locate the current user inside the SharePoint Person choices using:

```powerfx

If(

Form1.Mode = FormMode.New,

LookUp(

    Choices([@'Access Requests'].'Requester'),

    Email = User().Email

),

Parent.Default

)

```

The formula was syntactically valid, but the Requester field remained blank when creating a new request.

---

### Second Attempt — Lookup by Display Name

The next test attempted to match the current Power Apps user using:

```powerfx

LookUp(

Choices([@'Access Requests'].'Requester'),

DisplayName = User().FullName

)

```

The formula was accepted by Power Apps, but the Requester field still did not automatically populate.

---

### Third Attempt — Lookup by SharePoint Claims Identity

Existing SharePoint Person values revealed that SharePoint was representing the user with a Claims identity similar to:

```text

i:0#.f|membership|user@tenant.onmicrosoft.com

```

The lookup was changed to:

```powerfx

If(

Form1.Mode = FormMode.New,

LookUp(

    Choices([@'Access Requests'].'Requester'),

    Lower(Claims) = "i:0#.f|membership|" & Lower(User().Email)

),

Parent.Default

)

```

The formula was accepted, but the Requester field still did not populate.

---

### Root Cause

Searching the values returned by the SharePoint Person `Choices()` function was not reliably returning the currently authenticated user for the Combo Box default.

Power Apps already knows the authenticated user through the `User()` function, so searching the SharePoint choices was unnecessary.

---

### Final Solution

Instead of searching for the current user, a SharePoint-compatible Person record was constructed directly from the authenticated Power Apps user.

The `DefaultSelectedItems` property of `DataCardValue3` was changed to:

```powerfx

If(

Form1.Mode = FormMode.New,

{

    '@odata.type': "#Microsoft.Azure.Connectors.SharePoint.SPListExpandedUser",

    Claims: "i:0#.f|membership|" & Lower(User().Email),

    DisplayName: User().FullName,

    Email: User().Email,

    Department: "",

    JobTitle: "",

    Picture: ""

},

Parent.Default

)

```

This successfully populated the Requester field when **+ New** was selected.

The `Parent.Default` branch preserves the Requester stored in SharePoint when viewing or editing an existing request.

---

### Display Issue

After the Requester began populating correctly, Power Apps displayed the raw SharePoint Claims identity instead of the user's friendly name.

Example:

```text

i:0#.f|membership|user@tenant.onmicrosoft.com

```

The Combo Box `DisplayFields` property was:

```powerfx

["Claims"]

```

It was changed to:

```powerfx

["DisplayName"]

```

The Requester field then correctly displayed the user's friendly name.

---

### Final Result

When an authenticated employee clicks **+ New**:

- Power Apps identifies the currently signed-in user.

- The Requester field automatically populates.

- The user sees their friendly display name.

- The SharePoint-compatible Person record is retained for submission.

- Existing records preserve their original Requester value.

---

### Lesson Learned

SharePoint Person columns use structured user records rather than simple text values.

When Power Apps already knows the authenticated user, constructing the required SharePoint Person record directly can be more reliable than attempting to search the values returned by `Choices()`.

Also, `DisplayFields` controls which part of a Person record is shown to the user. A valid Person record can therefore be stored correctly while still displaying an undesirable technical value such as `Claims`.

### Portfolio / Interview Relevance

This issue demonstrates troubleshooting across:

- Power Apps

- Power Fx

- SharePoint Person columns

- Microsoft 365 authenticated identity

- SharePoint Claims identities

- Structured record data types

- UI presentation versus stored data

- New-record versus existing-record behavior

```

This is a **strong debugging entry** because it doesn't just say “Requester wasn't working.” It documents the failed approaches, why we changed direction, the final solution, and what you learned.

And we should keep the tenant-specific email out of the journal since this is going into your public GitHub portfolio; using `user@tenant.onmicrosoft.com` documents the concept without exposing your actual tenant information.

```

Good. We'll document the **bug first**, since that was a real troubleshooting issue and is valuable portfolio material.

### Debugging Journal — Issue 004

Open your project in VS Code and open:

```text

DEBUGGING_JOURNAL.md

```

Go to the bottom and add this entire entry:

````markdown
## Issue 005 — Power Apps Form Submission Failed Because Status Was Required

### Date

September 13, 2026

### Component

Power Apps / SharePoint Online

### Problem

The Access Request Power App would not submit a new request.

When the user clicked the submit checkmark, Power Apps displayed:

> Cannot save. Please check if there are errors in the form.

The visible employee-facing fields were completed correctly, so the cause was not immediately apparent.

### Investigation

The Power Apps form's `OnFailure` behavior confirmed that the form submission was failing.

Further inspection revealed the specific validation error:

> Field 'Status' is required.

The SharePoint `Status` column was configured as a required field, but the Status field had previously been removed from the employee-facing Power Apps form because workflow/system-managed fields should not normally be entered manually by employees.

As a result, Power Apps attempted to create the SharePoint item without supplying the required Status value.

### Root Cause

SharePoint required a value for the `Status` column, but the Power Apps form was not submitting one.

The SharePoint default value alone was not sufficient for this Power Apps form submission scenario.

### Resolution

The Status field was temporarily added back to the Power Apps form so its behavior could be inspected.

The Status ComboBox was configured so that new requests automatically receive the value:

```powerfx

If(

Form1.Mode = FormMode.New,

{Value: "Draft"},

Parent.Default

)

```
````

The ComboBox `Items` property remained:

```powerfx

Choices([@'Access Requests'].'Status')

```

This allows new requests to start automatically with a Status of `Draft` while existing records continue to use their stored SharePoint Status value.

### Verification

A new request named:

`Test - Operations Site Access`

was submitted successfully through Power Apps.

The request was created in the SharePoint `Access Requests` list.

Power Automate then successfully generated:

`AR-00004`

This confirmed the working path:

Power Apps → SharePoint Online → Power Automate → Request ID generation

### Lesson Learned

When a SharePoint column is required, a Power Apps form must supply a valid value during submission even when the field is intended to be system-managed.

System-managed fields can be hidden from the final employee interface, but their required values still need to be supplied through application or automation logic.

```



```

## Issue 006 — Power Apps Person Field Displayed SharePoint Claims Instead of Display Name

### Problem

The Assigned Administrator field in the Power Apps fulfillment interface displayed the raw SharePoint claims value instead of the administrator's friendly display name.

Example:

```text

i:0#.f|membership|sean@urbanassessory.onmicrosoft.com

```

This made the administrative interface difficult to read and was not appropriate for a production-style user experience.

### Investigation

The Assigned Administrator control was identified as:

```text

DataCardValue11

```

The ComboBox was correctly retrieving available SharePoint Person values using:

```powerfx

Choices([@'Access Requests'].'AssignedAdministrator')

```

The control also preserved the existing SharePoint Person record using:

```powerfx

DefaultSelectedItems = Parent.Default

```

However, the ComboBox display and search configuration were not using the person's friendly display name.

### Root Cause

SharePoint Person columns return complex user records rather than simple text values.

The ComboBox was displaying and searching the wrong property from that Person record, causing the SharePoint claims identity to appear instead of the user's friendly name.

### Resolution

The ComboBox was configured to display and search using the `DisplayName` property while preserving the complete Person record required by SharePoint.

Final configuration:

```powerfx

DisplayFields = ["DisplayName"]

SearchFields = ["DisplayName"]

DefaultSelectedItems = Parent.Default

DisplayMode = Parent.DisplayMode

```

The existing Items configuration remained:

```powerfx

Choices([@'Access Requests'].'AssignedAdministrator')

```

### Validation

The application was tested in Edit and View modes.

- Assigned Administrator displayed `Sean Reed`.

- The raw SharePoint claims value was no longer displayed.

- Administrator selection continued to work.

- The form saved successfully.

- The selected administrator persisted after the record was reloaded.

- SharePoint continued receiving the complete Person record.

### Lesson Learned

SharePoint Person fields should be treated as complex records rather than plain text.

When using a Person field in a Power Apps ComboBox, the application can preserve the complete SharePoint Person object for saving while using properties such as `DisplayName` for the user-facing interface.

This provides a cleaner user experience without breaking the underlying SharePoint Person field integration.

## Issue 007 — Administrative Fields Appeared Missing Because App State Was Not Initialized

### Problem

During final V1 interface testing, the administrative fulfillment fields appeared to be missing from the Power Apps form.

The affected fields included:

- Assigned Administrator

- Fulfillment Date

- Fulfillment Notes

- Completed Date

Because these fields were positioned near the bottom of the form, the initial investigation focused on whether the form height, card positioning, or container layout was preventing the fields from being displayed.

### Investigation

The form and surrounding layout were inspected, including:

- Form height

- DataCard height

- DataCard grid position

- Container padding

- Form column configuration

- Visibility properties

The DataCards still existed and their layout properties were valid.

The administrative cards used conditional visibility based on the current application mode.

Example:

```powerfx

varAppMode = "admin"

```

The application mode was controlled by the global variable:

```powerfx

varAppMode

```

Testing showed that the expected application state had not been initialized in the current Power Apps Studio session.

### Root Cause

The administrative fields were not missing or clipped by the form.

The `varAppMode` global variable had not been initialized to the expected runtime state.

Because the administrative DataCards depended on `varAppMode` for visibility, they remained hidden even though their layout and form configuration were correct.

### Resolution

`App.OnStart` was executed to initialize the application's global variables.

The application startup logic initializes requester mode and evaluates administrator membership:

```powerfx

Set(varAppMode, "myrequests");

Set(

varIsAdmin,

!IsBlank(

    LookUp(

        Office365Groups.ListGroupMembers(

            "4ca05468-5622-4647-9108-271e7aafa7a0"

        ).value,

        Lower(mail) = Lower(User().Email)

    )

)

)

```

After running `App.OnStart`, the application state initialized correctly.

Selecting Admin View then changed:

```powerfx

varAppMode

```

to:

```text

admin

```

and the administrative fulfillment fields appeared as expected.

### Validation

After initializing the application and entering Admin View:

- Administrative fulfillment fields displayed correctly.

- The form did not require structural changes.

- Existing DataCard positioning remained intact.

- Requester mode continued hiding administrative fields.

- Admin View continued exposing the fulfillment interface.

- No SharePoint columns or additional spacer controls were required.

### Lesson Learned

When Power Apps controls use conditional visibility, verify application variables and runtime state before restructuring the user interface.

A control that appears to be missing may simply have a `Visible` formula evaluating to false.

The debugging order should therefore include:

1. Verify the control still exists.

2. Inspect its `Visible` property.

3. Verify variables used by the visibility formula.

4. Run or validate `App.OnStart`.

5. Confirm the current application mode.

6. Only then investigate layout or structural changes.

This prevented unnecessary modifications to a form whose underlying layout was already functioning correctly.
