# list-of-important-commands
This is a list of important commands for deployment or installation if different packages and/or environments.

### Command to kill port that is already in use by another application
- ```$ lsof -t -i tcp:8000 | xargs kill -9```

### Install virtual environmnet in directory

In the main directory root add the following command to create the environment:

```$ python3 -m venv venv``` this code will create a folder called venv in the root. Which basically is the virtual environment folder.

Then add the following command to activate the virtual environment:
```
$ source venv/bin/activate

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
 |         |--Other_app_folder/
 |
 |--venv/
 ```
If the code works fine your bash should look like this: (venv) <the_path_for_the_folder> your_project_folder %

After activated your environment you can now install django and other packages.

Ps: make sure you instal and activate the virtual environment folder not in the ```your_main_app_folder```.


### Install django-heroku without psycopg2 for mac os
- ```$ pip install psycopg2-binary```
- ```$ pip install django-heroku --no-dependencies```

### Add remote/already added repo from heroku

- ```$ heroku git:remote -a <already_added_app_name>```

[Django deployment to heroku step-by-step here](https://simpleisbetterthancomplex.com/tutorial/2016/08/09/how-to-deploy-django-applications-on-heroku.html)
Ps: based on the step-by-step above, depending the version of django `whitenoise` should not be added to `wsgi.py` file rather it should be added to middlewares in `settings.py`.


### Check which repo is in my git
- ```git remote -v```
- This is how should be on the bottom of settings.py

```
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


### Display sqlite3 db on bash cmd

[Sqlite tutorial to describe table here](https://www.sqlitetutorial.net/sqlite-tutorial/sqlite-describe-table/)

1. ```python manage.py dbshell```: This command will activate the sqlite shell.
2. ```sqlite> .tables```: This command will display all tables available on shell.
3. ```sqlite> .header on ```: Will activate headers.
4. ```sqlite> .mode column```: Will activate columns
5. ```sqlite> pragma table_info('<table_name>'); ```: This command will display the <table_name> you want to see.
