---
name: "git commit"
description: "Complete workflow for submitting file changes to Git repository, including repo initialization, file tracking, .gitignore maintenance and formal commit"
---
## Full Standard Execution Flow
### Step 1: Detect Git Repository State
1. Check whether the project root directory contains a `.git` folder:
   - **Case A: No Git repository exists**
     1. Initialize a new Git repository in the project root, the repository name is consistent with the root folder/project name.
     2. Proceed to Step 2 for file staging and ignore file configuration.
   - **Case B: Git repository already exists**
     Directly skip to Step 2 to process project files and ignore rules.

### Step 2: Maintain .gitignore Ignore Rules
1. Check if a `.gitignore` file exists in the project root:
   - **If .gitignore does NOT exist**:
     Create a brand new `.gitignore` file, add standard ignore entries for all test files, build artifacts, compilation outputs, dependency caches, runtime logs and temporary files (universal engineering ignore templates).
   - **If .gitignore already exists**:
     Traverse all test directories, build output directories, compiled binaries, cache folders and temporary resource files in the project; add corresponding ignore patterns to `.gitignore` only if the rules are missing, avoid duplicate entries.
2. Standard ignore categories to be covered:
   - Build outputs: `build/`, `dist/`, `out/`, `*.o`, `*.exe`, `*.dll`, `*.class`
   - Test artifacts: `test-report/`, `coverage/`, `.pytest_cache`, `__pycache__/`
   - Environment & cache: `.env`, `.venv`, `node_modules`, `.DS_Store`, `.log`
   - Editor temp files: `.vscode/`, `.idea/`, `*.swp`, `*.tmp`

### Step 3: Stage All Project Source Files
Execute file tracking operation to add all valid project source files into Git staging area, exclude all files matched by `.gitignore` rules automatically.

### Step 4: Formal Commit Changes to Repository
1. Generate standardized, clear commit message describing the modified content.
2. Run commit command to persist staged changes to local Git repository with complete version record.

## Supplementary Constraints
1. All operations must be executed in the project root directory to avoid path offset errors.
2. Do not overwrite existing valid custom rules inside `.gitignore`; only append missing ignore entries at the end of the file.
3. Repository initialization command strictly uses the project root folder name as repo identity, no random custom repo names.
4. Skip duplicate file staging to prevent redundant index records.
5. After commit, the working tree and Git index maintain consistent state.
