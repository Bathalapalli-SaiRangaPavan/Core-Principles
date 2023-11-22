##  Day 25 - Docker Containerzation for Django 
### Introduction

This documentation outlines the process of containerizing a Django application using Docker. As a DevOps engineer, understanding the workflow of Python applications, such as Django, is crucial for efficient containerization.

### Prerequisites

Before proceeding, ensure the following prerequisites are met:

1. Python is installed on your system.
2. Pip is installed for Python package management.
3. Docker is installed on your machine.

## Workflow of Django Application

### Step 0: Visit Django Documentation

Begin by referring to the official Django documentation for comprehensive information.

### Step 1: Install Django

Install Django using the following commands:

```
pip install Django
```

Verify the installation by importing Django.

### Step 2: Create a Django Project
Use django-admin to create a Django project:

```
django-admin startproject devops
```

### Step 3: Create an Application
Create a Django application within the project:

```
python manage.py startapp demo
```

## Django Project Skeleton

This is a basic Django project skeleton to help you get started with structuring your Django applications.

### Project Structure

```plaintext
mydjangoapp/
├── manage.py
├── mydjangoapp/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── demo/
│   ├── migrations/
│   │   └── __init__.py
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── devops/
│   ├── templates/
│   │   └── index.html
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── requirements.txt
├── Dockerfile
└── README.md
```

## Project Components

### mydjangoapp/: Main project directory.
- **manage.py**: Django management script.
- **mydjangoapp/**: Django project folder.
  - `__init__.py`: Package file.
  - `settings.py`: Django project settings.
  - `urls.py`: URL patterns for the project.
  - `wsgi.py`: Entry point for WSGI servers.

### demo/: Django app within the project.
- **migrations/**: Database migration files.
- `__init__.py`: Package file for the app.
- `admin.py`: Django admin configuration.
- `apps.py`: App configuration.
- `models.py`: Database models.
- `tests.py`: Test cases.
- `views.py`: Views (controllers).

### devops/: Another Django app.
- **templates/**: HTML templates.
- `__init__.py`, `settings.py`, `urls.py`, `wsgi.py`: Similar structure as the main project.

### Other Files
- **requirements.txt**: Python dependencies for the project.
- **Dockerfile**: Docker image configuration.
- **README.md**: Project documentation.

## Containerization with Docker
Writing Dockerfile
Create a Dockerfile in the project directory:

```
# Choose a base image
FROM ubuntu

# Set working directory
WORKDIR /app

# Copy dependencies
COPY requirements.txt /app

# Copy source code
COPY devops /app

# Install dependencies
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip install -r requirements.txt && \
    cd devops

# Set entry point
ENTRYPOINT ["python3"]

# Set default command
CMD ["manage.py", "runserver", "0.0.0.0:8080"]
```

### Building the Docker Image
Build the Docker image from the project directory:

```
docker build -t mydjangoapp .
```

### Running the Docker Container
Run the Docker container and map the host port:

```
docker run -p 8080:8080 -it mydjangoapp
```

Access the Django application at http://localhost:8080.

### Conclusion
By following these steps, you have successfully containerized a Django application using Docker. This approach enhances deployment consistency and aids in resolving issues related to different environments.

