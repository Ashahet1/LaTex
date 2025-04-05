Absolutely — here’s a full **`README.md`** draft that captures your entire setup and troubleshooting journey for LaTeX on macOS using **BasicTeX** and **VS Code (2022)**.

---

### ✅ Markdown: `README.md`

```markdown
# LaTeX Setup on macOS with BasicTeX and VS Code 2022

This document records the full process, issues, and solutions encountered while setting up LaTeX with Visual Studio Code (VS Code 2022) on macOS using the lightweight **BasicTeX** distribution.

---

## 📦 Tools Used

- **macOS (Apple Silicon)**
- **BasicTeX (2025 version)**
- **Visual Studio Code 2022**
- **LaTeX Workshop extension for VS Code**
- **Shell**: zsh

---

## 🛠️ Installation Steps

### 1. Install BasicTeX

Download and install from:  
➡️ [https://tug.org/mactex/morepackages.html](https://tug.org/mactex/morepackages.html)

### 2. Add BasicTeX to PATH

Add the TeX binary location to your system PATH:

```bash
sudo nano /etc/paths
```

Add this line (if not already present):

```
/Library/TeX/texbin
```

Then restart your Terminal and VS Code.

---

### 3. Install VS Code and LaTeX Workshop Extension

- Install **VS Code 2022**
- Go to Extensions panel (`Cmd + Shift + X`)
- Search and install: **LaTeX Workshop**

---

## ⚠️ Issues Faced and Fixes

### ❌ 1. macOS Error: "App is damaged or can't be opened"

When trying to open TeX apps or run tools:

```bash
zsh: bad pattern: ^[[200~sudo
```

#### ✅ Fix:
Run the following command to unquarantine:

```bash
sudo xattr -rd com.apple.quarantine /Library/TeX
```

If you installed a GUI tool like TeXmaker or TeXstudio:

```bash
sudo xattr -rd com.apple.quarantine /Applications/TeXstudio.app
```

---

### ❌ 2. LaTeX Build Error in VS Code

```text
Error: spawn latexmk ENOENT
```

VS Code couldn't find the `latexmk` command.

#### ✅ Fix:
`latexmk` is **not included in BasicTeX by default**. Install it via:

```bash
sudo tlmgr update --self
sudo tlmgr install latexmk
```

---

### ❌ 3. VS Code Asking for Permissions: "Visual Studio Code 2 would like to access..."

This persistent macOS privacy prompt can appear due to repeated blocked access.

#### ✅ Fix:
Go to **System Settings > Privacy & Security**:

- Grant or revoke permissions under:
  - **Files and Folders**
  - **Full Disk Access**
  - **Accessibility**

Also clear old installs:
```bash
killall "Visual Studio Code"
```

Or check `/Applications` for multiple VS Code versions like “Visual Studio Code 2”.

---

### ❌ 4. Keyboard Shortcut `Cmd + Option + B` Not Working

Caused by either:

- Missing `latexmk`
- Wrong recipe
- Inactive `.tex` editor

#### ✅ Fix:
Once `latexmk` is installed, restart VS Code and press `Cmd + Option + B` with your `.tex` file open.

---

## ✅ Final Checklist

- [x] Installed BasicTeX
- [x] Added TeX path to environment
- [x] Installed LaTeX Workshop in VS Code
- [x] Installed `latexmk` via `tlmgr`
- [x] Fixed macOS permission prompts
- [x] Successfully compiled `.tex` file using `Cmd + Option + B`

---

## 🎉 Result

PDF builds now work flawlessly inside VS Code with live preview.

---

## 📝 Notes

- You can optionally enable **auto build on save** via settings:

```json
"latex-workshop.latex.autoBuild.run": "onSave"
```

- Consider using [Overleaf](https://www.overleaf.com) for quick collaboration or online editing if local issues persist.

```

---

Let me know if you want this in a downloadable `.md` file or need a short version for sharing.
