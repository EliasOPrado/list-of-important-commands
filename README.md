# list-of-important-commands
This is a list of important commands for deployment or installation if different packages and/or environments.

### Command to kill port that is already in use by another application
- ```$ lsof -t -i tcp:8000 | xargs kill -9```

### Install virtual environmnet in directory

In the main directory root add the following command to create the environment:

```$ python3 -m venv venv``` this code will create a folder called venv in the root. Which basically is the virtual environment folder.

Then add the following command to activate the virtual environment: ```$ source venv/bin/activate````.```

If the code works fine your bash should look like this: (venv) <the_path_for_the_folder> your_project_folder %

After activated your environment you can now install django and other packages.

Ps: make sure you instal and activate the virtual environment folder not in the ```your_main_app_folder```.

 ### Initiate a new Django project 
 
 - Once the virtual environment is installed it is time to create a django project. Therefore, the command to start a new project is as follow?
 ```$ django-admin startproject mysite```
 
- Therefore, once the project is created, the directory will look like this below:

```
your_project_folder/
 |
 |-- your_main_app_folder/
 |         |
 |         |--Folder_with_controllers/
 |                      __init__.py
 |                      settings.py
 |                      urls.py
 |                      wsgy.py
 |         
 |         
 |
 |--manage.py
 |--venv/
 ```
- Make sure you have already migrated the data-base with the command:
 ```$ python manage.py makemigrations``` and ```$ python manage.py migrate```
 
 - One you have done those two commands its time to run the server with the following command:
 ```$ python manage.py runserver```
 
 ### Creating a new app
 
 - The command to create a new app is:
 ```$ python manage.py startapp <the-name-of-your-app>```
 
 - Dont forget to add the ```<the-name-of-your-app>``` app into the ```settings.INSTALLED_APPS```.
 - Once the app is already added to the settings migrate it again.
 
 The directory will look like this with the new app:
 
 ```
your_project_folder/
 |
 |-- your_main_app_folder/
 |         |
 |         |--Folder_with_controllers/
 |         |            settings.py
 |         |            urls.py
 |         |            ...
 |         | 
 |         |--App_folder/
 |         
 |
 |--manage.py
 |--venv/
 ```


### Install django-heroku without psycopg2 for mac os
- ```$ pip install psycopg2-binary```
- ```$ pip install django-heroku --no-dependencies```

### Add remote/already added repo from heroku

- ```$ heroku git:remote -a <already_added_app_name>```

[Django deployment to heroku step-by-step here](https://simpleisbetterthancomplex.com/tutorial/2016/08/09/how-to-deploy-django-applications-on-heroku.html)
Ps: based on the step-by-step above, depending the version of django `whitenoise` should not be added to `wsgi.py` file rather it should be added to middlewares in `settings.py`.

### Option to wsgi for Django deployment to Heroku

```web: python manage.py runserver 0.0.0.0:$PORT --noreload```

### Check which repo is in my git
- ```git remote -v```
- This is how should be on the bottom of settings.py


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.0/howto/static-files/
PROJECT_ROOT = os.path.dirname(os.path.abspath(__file__))

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/
STATIC_ROOT = os.path.join(PROJECT_ROOT, 'staticfiles')
STATIC_URL = '/static/'
STATICFILES_DIRS = (os.path.join(BASE_DIR, "static"),)

MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'

MESSAGE_STORAGE = 'django.contrib.messages.storage.session.SessionStorage'
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage' #for deployment

"""ADD ENV TO AVOID SHOWING THE REAL KEYS """
STRIPE_PUBLISHABLE = os.getenv('STRIPE_PUBLISHABLE')
STRIPE_SECRET = os.getenv('STRIPE_SECRET')
```
And and add `whitenoise` in middlewares:
`whitenoise.middleware.WhiteNoiseMiddleware',`.

After deploying to heroku add this command:
`python3 manage.py collectstatic` to create `staticfiles` within the `main_folder` to 
run static files while `Debug=False`. 

Remember, to have access to `static` files while developing in `localhost` live `Debug.True`. 

### Remove commits 

To force to remove the last commit from git,
use these 2 following commands:

git reset --hard HEAD^
git push origin -f

If you want to remove the last 2 commits:
git reset --hard HEAD~2
git push origin -f


### Display sqlite3 db on bash cmd

[Sqlite tutorial to describe table here](https://www.sqlitetutorial.net/sqlite-tutorial/sqlite-describe-table/)

1. ```python manage.py dbshell```: This command will activate the sqlite shell.
2. ```sqlite> .tables```: This command will display all tables available on shell.
3. ```sqlite> .header on ```: Will activate headers.
4. ```sqlite> .mode column```: Will activate columns
5. ```sqlite> pragma table_info('<table_name>'); ```: This command will display the <table_name> you want to see.
6. ```sqlite> .quit```: this command will close sqlite shell.

### List of Sqlite3 commands
```
sqlite> .help
.auth ON|OFF           Show authorizer callbacks
.backup ?DB? FILE      Backup DB (default "main") to FILE
.bail on|off           Stop after hitting an error.  Default OFF
.binary on|off         Turn binary output on or off.  Default OFF
.changes on|off        Show number of rows changed by SQL
.check GLOB            Fail if output since .testcase does not match
.clone NEWDB           Clone data into NEWDB from the existing database
.databases             List names and files of attached databases
.dbinfo ?DB?           Show status information about the database
.dump ?TABLE? ...      Dump the database in an SQL text format
                         If TABLE specified, only dump tables matching
                         LIKE pattern TABLE.
.echo on|off           Turn command echo on or off
.eqp on|off|full       Enable or disable automatic EXPLAIN QUERY PLAN
.exit                  Exit this program
.explain ?on|off|auto? Turn EXPLAIN output mode on or off or to automatic
.fullschema ?--indent? Show schema and the content of sqlite_stat tables
.headers on|off        Turn display of headers on or off
.help                  Show this message
.import FILE TABLE     Import data from FILE into TABLE
.imposter INDEX TABLE  Create imposter table TABLE on index INDEX
.indexes ?TABLE?       Show names of all indexes
                         If TABLE specified, only show indexes for tables
                         matching LIKE pattern TABLE.
.iotrace FILE          Enable I/O diagnostic logging to FILE
.limit ?LIMIT? ?VAL?   Display or change the value of an SQLITE_LIMIT
.lint OPTIONS          Report potential schema issues. Options:
                         fkey-indexes     Find missing foreign key indexes
.load FILE ?ENTRY?     Load an extension library
.log FILE|off          Turn logging on or off.  FILE can be stderr/stdout
.mode MODE ?TABLE?     Set output mode where MODE is one of:
                         ascii    Columns/rows delimited by 0x1F and 0x1E
                         csv      Comma-separated values
                         column   Left-aligned columns.  (See .width)
                         html     HTML <table> code
                         insert   SQL insert statements for TABLE
                         line     One value per line
                         list     Values delimited by "|"
                         quote    Escape answers as for SQL
                         tabs     Tab-separated values
                         tcl      TCL list elements
.nullvalue STRING      Use STRING in place of NULL values
.once FILENAME         Output for the next SQL command only to FILENAME
.open ?--new? ?FILE?   Close existing database and reopen FILE
                         The --new starts with an empty file
.output ?FILENAME?     Send output to FILENAME or stdout
.print STRING...       Print literal STRING
.prompt MAIN CONTINUE  Replace the standard prompts
.quit                  Exit this program
.read FILENAME         Execute SQL in FILENAME
.restore ?DB? FILE     Restore content of DB (default "main") from FILE
.save FILE             Write in-memory database into FILE
.scanstats on|off      Turn sqlite3_stmt_scanstatus() metrics on or off
.schema ?PATTERN?      Show the CREATE statements matching PATTERN
                          Add --indent for pretty-printing
.selftest ?--init?     Run tests defined in the SELFTEST table
.separator COL ?ROW?   Change the column separator and optionally the row
                         separator for both the output mode and .import
.session CMD ...       Create or control sessions
.sha3sum ?OPTIONS...?  Compute a SHA3 hash of database content
.shell CMD ARGS...     Run CMD ARGS... in a system shell
.show                  Show the current values for various settings
.stats ?on|off?        Show stats or turn stats on or off
.system CMD ARGS...    Run CMD ARGS... in a system shell
.tables ?TABLE?        List names of tables
                         If TABLE specified, only list tables matching
                         LIKE pattern TABLE.
.testcase NAME         Begin redirecting output to 'testcase-out.txt'
.timeout MS            Try opening locked tables for MS milliseconds
.timer on|off          Turn SQL timer on or off
.trace FILE|off        Output each SQL statement as it is run
.vfsinfo ?AUX?         Information about the top-level VFS
.vfslist               List all available VFSes
.vfsname ?AUX?         Print the name of the VFS stack
.width NUM1 NUM2 ...   Set column widths for "column" mode
                         Negative values right-justify
sqlite>
```
