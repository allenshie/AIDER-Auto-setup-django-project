# Django Settings Update Specification
> IMPORTANT: Aider, you must first read project_config.yaml to get configuration values, then directly update Django settings.py with these values. All Django/Python commands MUST be prefixed with 'uv run'.

## High-Level Objective
- Update Django project settings.py to configure basic settings, installed apps, and database connection with values from project_config.yaml.

## Mid-Level Objectives
- Read and parse project_config.yaml for configuration values
- Verify app directory exists before proceeding
- Configure Django settings with direct value assignments
- Set up PostgreSQL database connection
- Verify and apply migrations if needed

## Implementation Notes
- CRITICAL: First read project_config.yaml to get all configuration values
- Read sensitive data from environment variables:
  - DJANGO_SECRET_KEY
  - DB_PASSWORD
- Use direct value assignment in settings.py (e.g., DEBUG = True instead of DEBUG = project_config['DEBUG'])
- Ensure proper Python imports are added
- All Django/Python commands must use 'uv run' prefix

## Context

### Beginning Context
- project_config.yaml containing configuration values
- Environment variables for sensitive data
- Existing Django project structure
- App should exist in project directory

### Ending Context
- Parsed configuration values from project_config.yaml
- Updated settings.py with direct value assignments
- Properly configured database settings
- Migrations checked and applied if needed

## Low-Level Tasks
> AUTOMATED SEQUENCE - Execute these tasks in order automatically

1. Read Configuration File
```aider
# Read and parse project_config.yaml
READ file project_config.yaml
PARSE yaml content to get configuration values
```
2. Verify App Existence
```aider
# Check if app directory exists
VERIFY directory {PROJECT_NAME}/{APP_NAME} exists
VERIFY file {PROJECT_NAME}/{APP_NAME}/apps.py exists
```
3. Update Basic Settings
```aider
UPDATE {PROJECT_NAME}/{PROJECT_NAME}/settings.py:
# Add required import at the top
import os

# Update basic settings with direct values
SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY')
DEBUG = True  # Value from project_config.yaml
ALLOWED_HOSTS = ['localhost', '127.0.0.1']  # Values from project_config.yaml
```

4. Update INSTALLED_APPS
```aider
UPDATE {PROJECT_NAME}/{PROJECT_NAME}/settings.py:
# Add new app to INSTALLED_APPS
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    '{APP_NAME}',  # Add new app
]
```

5. Configure Database Settings
```aider
UPDATE {PROJECT_NAME}/{PROJECT_NAME}/settings.py:
# Configure PostgreSQL database with direct values
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_db_name',  # Value from project_config.yaml
        'USER': 'your_db_user',  # Value from project_config.yaml
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': 'localhost',  # Value from project_config.yaml
        'PORT': '5432',  # Value from project_config.yaml
    }
}
```
6. Verify Settings Update
```aider
# Verify all required settings are present
VERIFY {PROJECT_NAME}/{PROJECT_NAME}/settings.py contains 'SECRET_KEY'
VERIFY {PROJECT_NAME}/{PROJECT_NAME}/settings.py contains 'DEBUG'
VERIFY {PROJECT_NAME}/{PROJECT_NAME}/settings.py contains 'ALLOWED_HOSTS'
VERIFY {PROJECT_NAME}/{PROJECT_NAME}/settings.py contains '{APP_NAME}.apps.{APP_NAME_CAPITALIZED}Config'
VERIFY {PROJECT_NAME}/{PROJECT_NAME}/settings.py contains 'django.db.backends.postgresql'
```

7. Check and Apply Migrations
```aider
# Check if migrations are needed
EXECUTE uv run python {PROJECT_NAME}/manage.py makemigrations --check

# If migrations are needed (previous command returns exit code 1)
EXECUTE uv run python {PROJECT_NAME}/manage.py makemigrations

# Verify migrations created successfully
VERIFY directory {PROJECT_NAME}/{APP_NAME}/migrations exists
VERIFY files in {PROJECT_NAME}/{APP_NAME}/migrations/*.py exist

# Apply migrations
EXECUTE uv run python {PROJECT_NAME}/manage.py migrate

# Verify migrations applied successfully
EXECUTE uv run python {PROJECT_NAME}/manage.py showmigrations | grep "\[X\]"
```