# dir2llm

A lightweight Bash utility that consolidates directory contents into a single text file, optimized for use as context in Large Language Models (LLMs).

## Overview

`dir2llm` scans a directory, creates a comprehensive text file containing the directory structure and all text file contents, making it easy to provide complete project context to AI assistants like Claude, GPT-4, or other LLMs.

## Features

- **Automatic file aggregation** - Combines all text files into a single output
- **Smart filtering** - Automatically excludes binary files, .git directories, and other common build artifacts
- **Directory tree visualization** - Shows complete project structure at the beginning of output
- **Size limiting** - Configurable max file size to prevent including huge files
- **Customizable exclusions** - Easy configuration of directories to skip
- **Binary detection** - Automatically detects and skips binary files

## Installation

```bash
# Make the script executable
chmod +x dir2llm

# Optionally, copy to your PATH
cp dir2llm ~/.local/bin/
# or
sudo cp dir2llm /usr/local/bin/
```

## Usage

Navigate to any project directory and run:

```bash
dir2llm
```

This creates a file named `<directory_name>_contents.txt` in the current directory containing:
1. A header with directory path and generation timestamp
2. The complete directory tree structure
3. Contents of all text files in the directory

## Configuration

Edit these variables at the top of the script to customize behavior:

| Variable | Default | Description |
|----------|---------|-------------|
| `MAX_FILE_SIZE` | `1024k` | Maximum size for individual files (use k for KB) |
| `EXCLUDE_DIRS` | `.git,node_modules,__pycache__` | Comma-separated list of directories to skip |

## Output Format

The generated file follows this structure:

```
===== Directory: /path/to/project =====
===== Generated: Mon Jan 20 10:30:00 2025 =====

===== DIRECTORY STRUCTURE =====
.
├── src/
│   ├── main.py
│   └── utils.py
├── tests/
│   └── test_main.py
└── README.md

===== FILE CONTENTS =====

===== ./src/main.py =====
[file contents here]

===== ./src/utils.py =====
[file contents here]
```

## Use Cases

- **Code reviews** - Share entire codebase context with AI for comprehensive analysis
- **Documentation** - Generate project documentation by providing full context to LLMs
- **Debugging** - Help AI assistants understand your complete project structure when troubleshooting
- **Learning** - Analyze open source projects by feeding them to educational AI tools
- **Refactoring** - Get AI suggestions for improving code architecture with full project context

## Requirements

- Bash shell
- Standard Unix utilities: `find`, `grep`, `cat`, `sort`
- Optional: `tree` command for better directory visualization (falls back to `find` if not available)

## Examples

### Basic usage
```bash
cd ~/my-project
dir2llm
# Creates: my-project_contents.txt
```

### Customize for Python projects
```bash
# Edit the script to exclude more Python-specific directories
EXCLUDE_DIRS=".git,node_modules,__pycache__,venv,.pytest_cache,*.egg-info"
```

### Customize for Node.js projects
```bash
# Edit the script to handle larger JavaScript bundles
MAX_FILE_SIZE="5M"
EXCLUDE_DIRS=".git,node_modules,dist,build,.next"
```

## Tips

- Review the generated file before sharing to ensure no sensitive data is included
- For very large projects, consider increasing `MAX_FILE_SIZE` or adding more exclusions
- The output file is automatically excluded from subsequent runs to prevent recursion
- Binary files are detected and skipped automatically with a notation in the output

## License

Open source - feel free to use and modify as needed.

## Contributing

This is a simple utility script. Feel free to fork and adapt it to your needs!