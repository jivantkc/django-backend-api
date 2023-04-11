## Create django, django-restframwork, jwt, API depoy in Heroku.
Backend Project created using django.

## STEP1 Virtual Environment
Create a project folder:`mkdir project`

Go to folder:`cd project`

Creating Virtual environment to isolate packages:`python3 -m venv env`

Activate Virtual environment:`source env/bin/activate`

## STEP2 Install Django, project & app
Intall Django:`pip install django`

Create Django project:`django-admin startproject api`

Go inside Project folder:`cd api`

Start App:`django-admin startapp myapp`

# Add App to project

go to settings.py then in INSTALLED_APPS = [] add following.

'myapp.apps.MyappConfig',

Run Project:`python manage.py runserver`

This should open up browser in local host and show 

"The install worked successfully! Congratulations!".


## STEP3 Connecting to database.


