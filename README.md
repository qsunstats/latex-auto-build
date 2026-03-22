# 🚀 LaTeX Auto-Build with Auto Package Install (TeX Live + VS Code)

Make TeX Live behave like MiKTeX by automatically installing missing packages during compilation.

---

## ✨ Features

- 🔁 Auto compile loop
- 📦 Auto install missing LaTeX packages
- 🧠 Works with VS Code LaTeX Workshop
- 💻 macOS-friendly (no fragile shell quoting)

---

# ✅ Step 1 — Create the Auto-Build Script

First, create a `~/bin` folder if it does not exist yet:

```bash
mkdir -p ~/bin
```
then download our latex-auto-build file and put it in the above folder. 


## ✅ Step 2 — Make It Executable

Run:

```bash
chmod +x ~/bin/latex-auto-build
```

---

## ✅ Step 3 — Add It to Your PATH

Add `~/bin` to your shell PATH so the command is available everywhere:

```bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Verify that your shell can find it:

```bash
which latex-auto-build
```

You should see something like:

```bash
/Users/yourname/bin/latex-auto-build
```

---

## ✅ Step 4 — Use It

Run the script on your LaTeX file:

```bash
latex-auto-build main.tex
```

---

## ▶️ Example Run

If `main.tex` is missing a package such as `imakeidx`, you may see output like this:

```text
========== Run 1 ==========
📦 Missing packages detected:
imakeidx

📥 Installing...

========== Run 2 ==========
✅ No missing packages
🎉 Build complete
```

That means the script:

1. compiled the document,
2. detected the missing package,
3. installed it with `tlmgr`, and
4. retried the build automatically.

---

## 🧩 VS Code Integration

To use this script from LaTeX Workshop, add a custom tool and recipe in your VS Code `settings.json`.

Use the full path to the script, since GUI apps on macOS often do not inherit your shell PATH.

```json
"latex-workshop.latex.recipes": [
  {
    "name": "auto build",
    "tools": ["auto-build"]
  }
],
"latex-workshop.latex.tools": [
  {
    "name": "auto-build",
    "command": "/Users/yourname/bin/latex-auto-build",
    "args": ["%DOC%"]
  }
]
```

### Notes

- Replace `/Users/yourname/bin/latex-auto-build` with the actual output of:

```bash
which latex-auto-build
```

- In VS Code, select the recipe named `auto build`.

- If you see `spawn latex-auto-build ENOENT`, VS Code cannot find the script. Using the full path fixes that.

## 🎉 Result

With this setup, you get:

- ✅ automatic detection of missing `.sty` packages
- ✅ automatic installation with `tlmgr`
- ✅ automatic recompilation after installation
- ✅ easy integration with VS Code

A much smoother TeX Live workflow on macOS. 🚀


