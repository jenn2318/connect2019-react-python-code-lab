# Let's create the backend environment with Python

### Create the folder setup to get everything running:
$ mkdir django-todo-react

### Navigate to the directory:
$ cd django-todo-react

## Install Pipenv using pip and activate a new virtual environment:
$ pip install pipenv
$ pipenv shell

## Install Django using Pipenv then create a new project called backend:
$ pipenv install django
$ django-admin startproject backend

## Next, we will navigate into the newly created backend folder and start a new application called todo. We will also run migrations and start up the server:
$ cd backend
$ python manage.py startapp todo
$ python manage.py migrate
$ python manage.py runserver

## Registering and Defining the Todo model.....
