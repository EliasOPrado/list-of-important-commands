# list-of-important-commands
This is a list of important commands for deployment or installation if different packages and/or environments.

### Command to kill port that is already in use by another application
- $ lsof -t -i tcp:8000 | xargs kill -9

### Install virtual environmnet in directory

In the main directory root add the following command to create the environment:

- $ python3 -m venv venv
The code above will create a folder called venv in the root. Which basically is the virtual environment folder.

In the root (not in the venv folder) add the following command to activate the virtual environment:
- $ source venv/bin/activate


### Install django-heroku without psycopg2
- pip install django-heroku --no-dependencies
