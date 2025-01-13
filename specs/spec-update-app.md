# Django Models Creation Specification
> IMPORTANT: Aider, you must read model definitions from project_config.yaml and create corresponding Django models in models.py.

## High-Level Objective
- Create Django models based on the model definitions specified in project_config.yaml.

## Mid-Level Objectives
- Read and parse model definitions from project_config.yaml
- Create corresponding Django models with proper fields and relationships
- Validate model creation with makemigrations check
- Generate and apply migrations if needed

## Implementation Notes
- CRITICAL: First read and parse project_config.yaml for model definitions
- Ensure proper model imports are included
- Handle all field types specified in the configuration
- Handle model relationships (ForeignKey, OneToOne, ManyToMany)
- All Django/Python commands must use 'uv run' prefix
- Follow Django model best practices

## Context

### Beginning Context
- project_config.yaml containing model definitions
- Empty or basic models.py file
- Django app structure already set up
- Settings already configured

### Ending Context
- models.py populated with defined models
- All models properly imported and configured
- Validated models without errors
- Migrations created and applied if needed

## Low-Level Tasks
> AUTOMATED SEQUENCE - Execute these tasks in order automatically

1. Read Model Definitions
```aider
# Read and parse project_config.yaml for model definitions
READ file project_config.yaml
PARSE yaml content to get model definitions
```

2. Create Models
```aider
UPDATE {PROJECT_NAME}/{APP_NAME}/models.py:
# Add required imports
from django.db import models

# Create model classes based on parsed definitions
# Example format from project_config.yaml:
# models:
#   User:
#     fields:
#       name: CharField(max_length=100)
#       email: EmailField(unique=True)
```

3. Verify Model Structure
```aider
# Check model syntax and structure
EXECUTE uv run python {PROJECT_NAME}/manage.py check {APP_NAME}

# Verify each model exists in models.py
VERIFY {PROJECT_NAME}/{APP_NAME}/models.py contains each model name from config
```

4. Test Migration Generation
```aider
# Check if migrations are needed
EXECUTE uv run python {PROJECT_NAME}/manage.py makemigrations --dry-run

# Generate migrations if needed
EXECUTE uv run python {PROJECT_NAME}/manage.py makemigrations

# Verify migrations created
VERIFY directory {PROJECT_NAME}/{APP_NAME}/migrations exists
VERIFY new migration file exists in {PROJECT_NAME}/{APP_NAME}/migrations/
```
5. Apply and Verify Migrations
```aider
# Apply migrations
EXECUTE uv run python {PROJECT_NAME}/manage.py migrate

# Verify migrations applied successfully
EXECUTE uv run python {PROJECT_NAME}/manage.py showmigrations {APP_NAME}
```
