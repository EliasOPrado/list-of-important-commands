# list-of-important-commands
This is a list of important commands for deployment or installation if different packages and/or environments.

### Command to kill port that is already in use by another application
- ```$ lsof -t -i tcp:8000 | xargs kill -9```

### Install virtual environmnet in directory

In the main directory root add the following command to create the environment:

- ```$ python3 -m venv venv```
The code above will create a folder called venv in the root. Which basically is the virtual environment folder.

In the root (not in the venv folder) add the following command to activate the virtual environment:
- ```$ source venv/bin/activate```


### Install django-heroku without psycopg2
- ```$ pip install django-heroku --no-dependencies```

### Display sqlite3 db on bash cmd

[Sqlite tutorial to describe table here](https://www.sqlitetutorial.net/sqlite-tutorial/sqlite-describe-table/)

1. ```python manage.py dbshell```: This command will activate the sqlite shell.
2. ```sqlite> .tables```: This command will display all tables available on shell.
3. ```sqlite> .header on ```: Will activate headers.
4. ```sqlite> .mode column```: Will activate columns
5. ```sqlite> pragma table_info('<table_name>'); ```: This command will display the <table_name> you want to see.
