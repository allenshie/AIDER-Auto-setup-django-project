# Django Project Creation Specification
> IMPORTANT: Aider, you must DIRECTLY EXECUTE all commands with 'uv run' prefix for Django/Python commands. DO NOT create bash scripts.

## High-Level Objective
- Create a new Django project using the project name from project_config.yaml.

## Mid-Level Objectives
- Initialize a new Django project using django-admin with uv run prefix
- Ensure proper project directory structure
- Add project directory to aider's context

## Implementation Notes
- CRITICAL: All Django/Python commands MUST be prefixed with 'uv run'
- EXECUTE commands directly, DO NOT create bash scripts
- Project name will be read from project_config.yaml
- Ensure proper error handling
- Verify project creation success after each step

## Context

### Beginning Context
- project_config.yaml (readonly)
- Environment variables must be present

### Ending Context
- Django project directory created
- Basic Django project structure established
- Project added to aider's context

## Low-Level Tasks
> AUTOMATED SEQUENCE - Execute these tasks in order automatically

1. Create Django Project
```aider
# Create new Django project using uv run
EXECUTE uv run django-admin startproject {PROJECT_NAME}

# Add project to aider's context
EXECUTE /add {PROJECT_NAME}
```
2. Verify Project Structure
# Verify essential files exist
```aider
# Verify project creation and structure
VERIFY directory {PROJECT_NAME} exists
VERIFY file {PROJECT_NAME}/manage.py exists
VERIFY file {PROJECT_NAME}/{PROJECT_NAME}/settings.py exists
VERIFY file {PROJECT_NAME}/{PROJECT_NAME}/urls.py exists
VERIFY file {PROJECT_NAME}/{PROJECT_NAME}/wsgi.py exists
```
