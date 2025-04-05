# LaTeX Setup on macOS with BasicTeX and VS Code 2022

This document captures the entire setup, issues faced, and solutions during the installation of LaTeX on macOS using BasicTeX and Visual Studio Code (VS Code 2022).

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

Download from the official site:  
[https://tug.org/mactex/morepackages.html](https://tug.org/mactex/morepackages.html)

### 2. Add BasicTeX to the System PATH

Open Terminal:

```bash
sudo nano /etc/paths
```

Add this line to the top (if it doesn’t already exist):

```
/Library/TeX/texbin
```

Save (`Ctrl + O`, then `Enter`) and exit (`Ctrl + X`).  
Restart Terminal and VS Code.

---

### 3. Install VS Code and LaTeX Workshop

- Download and install [Visual Studio Code](https://code.visualstudio.com/)
- Go to Extensions (`Cmd + Shift + X`)
- Search for and install **LaTeX Workshop**

---

### 4. Install Missing LaTeX Tools (latexmk)

By default, BasicTeX does **not** include `latexmk`, which is required by LaTeX Workshop.

To fix this, open Terminal and run:

```bash
sudo tlmgr update --self
sudo tlmgr install latexmk
```

---

## ⚠️ Issues Faced and Solutions

### ❌ 1. “App can’t be opened or is damaged” (macOS warning)

macOS blocked some apps or binaries from running due to security (Gatekeeper).

#### ✅ Fix:
Unquarantine the TeX binaries or apps:

```bash
sudo xattr -rd com.apple.quarantine /Library/TeX
```

If using a GUI like TeXstudio:

```bash
sudo xattr -rd com.apple.quarantine /Applications/TeXstudio.app
```

---

### ❌ 2. VS Code Build Error: `spawn latexmk ENOENT`

VS Code throws an error during build:

```
LaTeX fatal error on PID undefined. Error: spawn latexmk ENOENT
```

#### ✅ Fix:
Install `latexmk` via `tlmgr`:

```bash
sudo tlmgr install latexmk
```

Then restart VS Code and rebuild the `.tex` file.

---

### ❌ 3. VS Code asks for permissions repeatedly:  
> “Visual Studio Code 2 would like to access data from other apps”

This is a macOS privacy prompt due to code access attempts.

#### ✅ Fix:
- Go to `System Settings > Privacy & Security`
- Under **Files and Folders** or **Full Disk Access**, either:
  - Allow access to VS Code
  - Or revoke unnecessary access

You can also remove extra VS Code versions like "Visual Studio Code 2" from `/Applications`.

---

### ❌ 4. Terminal shows `zsh: bad pattern` or `no such user: sudo`

Caused by copy-pasting commands with invisible characters (`^[[200~`).

#### ✅ Fix:
Manually type commands instead of pasting. Example:

```bash
sudo tlmgr install latexmk
```

---

### ❌ 5. `Cmd + Option + B` (Build Shortcut) Didn’t Work

This failed because `latexmk` was missing or the file wasn’t active.

#### ✅ Fix:
- Install `latexmk` as shown above
- Make sure a `.tex` file is open in the editor
- Press `Cmd + Option + B` again

---

## 🧪 Optional: Enable Auto Build on Save

In VS Code `settings.json`:

```json
"latex-workshop.latex.autoBuild.run": "onSave"
```

---

## ✅ Final Checklist

- [x] Installed BasicTeX
- [x] Added `/Library/TeX/texbin` to system PATH
- [x] Installed LaTeX Workshop extension
- [x] Installed `latexmk` via `tlmgr`
- [x] Unquarantined TeX tools
- [x] Fixed all macOS permission prompts
- [x] Successfully built and previewed PDF in VS Code

---

## 📄 Result

LaTeX is now working seamlessly in VS Code 2022 with live PDF preview and build support. 🎉

---

## 📝 Tips

- Use [Overleaf](https://www.overleaf.com) if you want a cloud-based LaTeX editor with collaboration.
- Use the `latexmk` recipe to automatically handle multiple runs for cross-references and bibliographies.
```

