---
name: build
description: Full project build workflow with CMake + Ninja. Covers dependency scanning, CMakeLists.txt auto-generation, build configuration, compilation, and targeted error handling for Qt moc files.
---

## Prerequisite
If Qt moc (Meta-Object Compiler) files have been modified, delete the temporary build directory before starting the build process.

## Execution Boundaries
- Only perform the operations specified in this document.
- Do not execute any extra actions outside the defined workflow.

## Step-by-Step Execution Workflow

### 1. Build Status Notification
Explicitly inform the user that the project build process has started.

### 2. Generate `CMakeLists.txt`
Automatically generate a valid `CMakeLists.txt` file that meets all following requirements:
- Scan and collect all project dependencies, including source files, header files, and include directories.
- Add all collected source and header files to the build configuration.
- Use native CMake commands to resolve and set the build output directory path. Hard-coded relative paths are strictly prohibited.
- Define the project name via the standard CMake `project()` command.
- Define the project version in the `project()` command.
- Define the project description in the `project()` command.

### 3. Run Build Configuration
Execute the CMake configuration step.

### 4. Run Compilation
Execute the compilation step after configuration succeeds.

## Standard Command Reference

### Build Configuration
Run the following command inside the `/build` directory:
```bash
cmake ..
```

### Compilation
Run the following command inside the `/build` directory:
```bash
ninja
```

## Error Handling & Troubleshooting
If the build or compilation fails, read the error output and handle it according to the error type, then re-run the compilation:
1. **Moc file related errors**: Delete the temporary build directory, then re-run the full build process from the configuration step.
2. **General file related errors**: Check and verify the corresponding project files.
3. **Header file related errors**: Inspect and validate all header files and their include paths.
4. **Source file related errors**: Inspect and validate all source file syntax and logic.
5. **If all files are valid**: Check and debug the `CMakeLists.txt` configuration.
6. **If configuration is also valid**: Perform an extremely detailed code review. Apply available debugging techniques to locate root causes.

After resolving the issue, re-run the compilation command.
