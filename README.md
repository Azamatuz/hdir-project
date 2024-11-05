# Project Setup Guide

# Project Setup

## Backend Setup

### Create a Virtual Environment

```sh
python3 -m venv .venv
```

This command creates a virtual environment named `.venv` in your current directory. A virtual environment is a self-contained directory that contains a Python installation for a particular version of Python, plus a number of additional packages.

### Activate the Virtual Environment

```sh
source .venv/bin/activate
```

This command activates the virtual environment. After activation, your terminal prompt will change to indicate that you are now working within the virtual environment.

### Upgrade pip

```sh
python3 -m pip install --upgrade pip
```

This command upgrades `pip`, the Python package installer, to the latest version.

### Install Django

```sh
python3 -m pip install django
```

This command installs Django, a high-level Python web framework, within your virtual environment.

### Create a Django Project

```sh
django-admin startproject myproject
```

This command creates a new Django project named `myproject`. Replace `myproject` with your desired project name.

### Navigate to the Project Directory

```sh
cd myproject
```

This command changes your current directory to the newly created project directory.

### Apply Initial Migrations

```sh
python3 manage.py migrate
```

This command applies the initial database migrations. Migrations are Django's way of propagating changes you make to your models (adding a field, deleting a model, etc.) into your database schema.

### Create a Superuser

```sh
python manage.py createsuperuser
```

Follow the prompts to create a superuser account.

### Configure ALLOWED_HOSTS in Django

To resolve the `DisallowedHost` error, follow these steps:

1. Open your `settings.py` file in your Django project.
2. Locate the `ALLOWED_HOSTS` setting.
3. Add `'127.0.0.1'` to the list of allowed hosts.

Your `ALLOWED_HOSTS` setting should look something like this:

```python
ALLOWED_HOSTS = ['127.0.0.1', 'localhost']
```

## Frontend Setup

### Install Node.js and npm

Ensure you have Node.js and npm installed. You can download and install them from the [Node.js official website](https://nodejs.org/).

### Install Vue CLI

```sh
npm install -g @vue/cli
```

This command installs the Vue CLI globally on your system.

### Create a New Vue Project

```sh
vue create frontend
```

This command creates a new Vue.js project named `frontend`. Follow the prompts to set up your project.

### Create a New Vue Project Without Git Initialization

By default, `vue create` initializes a Git repository in the newly created project. To avoid this, you can use the `--no-git` option when creating your Vue.js project. Here is the command:

```sh
vue create frontend --no-git
```

### Navigate to the Project Directory

```sh
cd frontend
```
This command changes your current directory to the newly created Vue.js project directory.




### Run the Development Server

```sh
npm run serve
```

This command starts the development server. You can view your Vue.js application in the browser at [http://localhost:8080](http://localhost:8080).

## Creating a Separate App for User Authentication

Creating a separate app for user authentication is a good practice as it helps keep your project organized and modular. You can name the app `users` to clearly indicate its purpose. Here are the steps to create the `users` app and implement authentication using a username instead of an email:

### Step 1: Create the `users` App

Navigate to your Django project directory and create the `users` app:

```sh
python manage.py startapp users
```

Add the `users` app to your `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'users',
]
```

### Step 2: Create a Custom User Model

Define a custom user model: In your `users` app, open `models.py` and define a custom user model that uses a username for authentication.

Update `settings.py` to use the custom user model:

```python
AUTH_USER_MODEL = 'users.CustomUser'
```

### Step 3: Create and Apply Migrations

Create migrations:

```sh
python manage.py makemigrations
```

Apply migrations:

```sh
python manage.py migrate
```

### Step 4: Update Admin Configuration

Register the custom user model in the admin site: In your `users` app, open `admin.py` and register the custom user model.

```python
from django.contrib import admin
from .models import CustomUser

admin.site.register(CustomUser)
```

## Summary of Commands

By following these steps, you will have a `users` app set up with authentication using a username. This app can be used to manage user-related functionality in your Django project.