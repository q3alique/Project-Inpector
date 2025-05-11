# Project-Inspector

A command-line tool to **analyze the structure and contents of source code projects**. It supports stack-aware file filtering (e.g., Java, Python, C++) and outputs a detailed tree view, word/size stats, and raw content of relevant files — perfect for audits, refactors, and ChatGPT token estimation.

---

## 🔧 How It Works

The script recursively traverses the project directory (`--path`) and:
- Detects meaningful files based on the selected `--stack`.
- Optionally includes additional `--include` files, folders, or extensions.
- Ignores specified folders or files via `--exclude`.
- Builds a **tree structure** of the project and collects:
  - File size
  - Word count
  - Raw content
- Outputs everything into a user-specified `.txt` file.

---

## Available Stacks

| Stack   | Extensions                          | Included Folders       | Excluded Folders                          |
|---------|-------------------------------------|------------------------|-------------------------------------------|
| `java`  | `.java`, `.xml`, `.properties`      | `src`                  | `target`, `.git`, `bin`, `build`, `lib`   |
| `python`| `.py`                               | `.`, `app`             | `__pycache__`, `.venv`, `build`, `.git`   |
| `cs`    | `.cs`, `.config`, `.csproj`         | `src`, `app`           | `bin`, `obj`, `.vs`, `.git`               |
| `dotnet`| `.cs`, `.config`, `.csproj`         | `src`, `app`           | `bin`, `obj`, `.vs`, `.git`               |
| `cpp`   | `.cpp`, `.c`, `.h`, `.hpp`          | `src`, `include`       | `build`, `bin`, `.git`                    |
| `c`     | `.c`, `.h`                          | `src`, `include`       | `build`, `bin`, `.git`                    |
| `rust`  | `.rs`, `.toml`                      | `src`                  | `target`, `.git`                          |
| `js`    | `.js`, `.json`, `.ts`               | `src`, `app`           | `node_modules`, `dist`, `.git`            |

---

## Usage

```bash
python3 script.py --path <project_root> --output <file> [options]
```

### Required Arguments
* `--path` : Root folder to start crawling.
* `--output` : Output .txt file where the results will be saved.

### Optional Arguments
* `--stack` : Technology stack to auto-detect extensions/folders.
* `--include` : Comma-separated list of:
* `--exclude` : Comma-separated list of folder or file names to ignore.
* `--help` or `--help <stack>` : Show general or stack-specific help.

---

## Examples

```bash
# Java project with default stack filters
python script.py --path ./my-java-project --stack java --output report.txt
```

```bash
# Python project + include YAML and text files
python script.py --path ./my-py-app --stack python --include .yaml,.txt --output report.txt
```

```bash
# Node.js project, include docs folder, exclude .git
python script.py --path ./web-app --include docs --exclude .git --output result.txt
```

```bash
# Just extract .cpp and .hpp files, skipping build artifacts
python script.py --path ./engine --include .cpp,.hpp --exclude build,.git --output code.txt
```



