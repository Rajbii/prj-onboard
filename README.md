# prj-onboard
Project-Onboarding; Analyze & Prepare an existing project for running & building. Detect the stack, install dependencies, configure environment variables, run the app, & create a production build.

# Project Onboarding
Use this skill when the user wants to analyze, run, or build an existing project.

## Goal
Inspect the project without guessing, identify its dependencies and required commands, then prepare it for local execution and production build.

## Workflow
1. Inspect the project structure:
   - Run `ls -la`
   - Run `find . -maxdepth 2 -type f | head -100`
   - Check for `README*`, `package.json`, `requirements.txt`, `pyproject.toml`, `Pipfile`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `pubspec.yaml`, `Makefile`, `docker-compose.yml`, and `Dockerfile`

2. Detect the project type and required tools:
   - Node.js / npm / pnpm / yarn / bun
   - Python / pip / uv / poetry
   - Flutter / Dart
   - React Native
   - Android / Gradle
   - Go / Rust / Java
   - Docker / Docker Compose

3. Check dependencies:
   - If `node_modules` is missing, run the appropriate install command.
   - If a Python virtual environment or `__pycache__` is missing, prepare the Python environment.
   - If a lockfile exists, use it; for example `package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `poetry.lock`, or `uv.lock`.

4. Inspect environment configuration:
   - Look for `.env.example`, `.env.sample`, `config.example.*`, and README instructions.
   - List every required environment variable.
   - Never create real secrets or API keys.
   - If needed, create a local `.env` file from an example file, leaving secret values empty.
   - Ask the user to provide secret values securely.

5. Identify run and build commands:
   - Inspect the `scripts` section in `package.json`.
   - Search the README for Install, Run, Development, and Build sections.
   - Check `Makefile`, `docker-compose.yml`, and configuration files.
   - If multiple methods exist, choose the official and lowest-risk method, then explain why.

6. Before running an important command:
   - Briefly explain what the command does and why it is needed.
   - Ask for confirmation before installing dependencies, deleting files, starting servers, building, or modifying important files.
   - Never delete `node_modules`, `.git`, `dist`, `build`, `venv`, or environment files unless the user explicitly requests it.

7. Run the application:
   - Run the appropriate local development command.
   - Detect the localhost address or port from the output.
   - Report whether the server started successfully.
   - If an error occurs, inspect the complete log, identify the likely cause, and suggest the smallest necessary fix.

8. Build the project:
   - First run and verify the project locally.
   - Then run the project's official build command.
   - Locate and report the build output directory.
   - If the build fails, classify the errors as dependency, version, environment-variable, configuration, or code issues.

## Important Rules
- Explain the cause of a problem before changing code.
- Do not guess; ask the user when information is missing.
- Make small, reversible changes.
- Follow the existing project architecture; do not introduce a new structure unless necessary.
- Use clear and consistent names for files, functions, and variables.
- Write appropriate tests for new features or bug fixes.
- Handle errors with clear messages and useful logs.
- At the end, provide a concise report containing:
  - Project type
  - Installed dependencies
  - Required environment variables
  - Run command
  - Build command
  - Build output path
  - Remaining errors and recommended fixes
  
