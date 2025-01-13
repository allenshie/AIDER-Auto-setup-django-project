# Django App Creation Specification
> IMPORTANT: Aider, you must create Django app structure manually by creating directory and files.

## High-Level Objective
- Create a new Django app structure manually within the project directory.

## Mid-Level Objectives
- Create app directory within project
- Create all required Django app files
- Ensure proper file content initialization
- Add app directory to aider's context

## Implementation Notes
- Create directory structure manually instead of using django-admin
- Initialize all required files with proper Python content
- Ensure proper file permissions
- Follow Django app structure conventions
- Verify file creation success

## Context

### Beginning Context
- Existing Django project structure
- project_config.yaml (readonly)
- Environment variables must be present

### Ending Context
- Django app directory created within project
- All required app files created and initialized
- App added to aider's context

## Low-Level Tasks
> AUTOMATED SEQUENCE - Execute these tasks in order automatically

1. Create App Directory Structure
```aider
# Create app directory within project
EXECUTE mkdir -p {PROJECT_NAME}/{APP_NAME}
EXECUTE mkdir -p {PROJECT_NAME}/{APP_NAME}/migrations

# Create __init__.py files
EXECUTE touch {PROJECT_NAME}/{APP_NAME}/__init__.py
EXECUTE touch {PROJECT_NAME}/{APP_NAME}/migrations/__init__.py

# Add app directory to aider's context
EXECUTE /add {PROJECT_NAME}/{APP_NAME}
```

2. Create Core App Files
```aider
# Create admin.py
CREATE {PROJECT_NAME}/{APP_NAME}/admin.py:
from django.contrib import admin
# Register your models here.

# Create apps.py
CREATE {PROJECT_NAME}/{APP_NAME}/apps.py:
from django.apps import AppConfig

class {APP_NAME_CAPITALIZED}Config(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = '{APP_NAME}'

# Create models.py
CREATE {PROJECT_NAME}/{APP_NAME}/models.py:
from django.db import models
# Create your models here.

# Create views.py
CREATE {PROJECT_NAME}/{APP_NAME}/views.py:
from django.shortcuts import render
# Create your views here.

# Create urls.py
CREATE {PROJECT_NAME}/{APP_NAME}/urls.py:
from django.urls import path
from . import views

app_name = '{APP_NAME}'
urlpatterns = [
    # Define your URL patterns here
]

# Create tests.py
CREATE {PROJECT_NAME}/{APP_NAME}/tests.py:
from django.test import TestCase
```
3. Verify App Structure
```aider
# Verify directory structure
VERIFY directory {PROJECT_NAME}/{APP_NAME} exists
VERIFY directory {PROJECT_NAME}/{APP_NAME}/migrations exists

# Verify core files
VERIFY file {PROJECT_NAME}/{APP_NAME}/__init__.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/migrations/__init__.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/admin.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/apps.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/models.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/views.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/urls.py exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/tests.py exists
```
