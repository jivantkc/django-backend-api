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

### Add App to project

go to settings.py then in INSTALLED_APPS = [] add following.

'myapp.apps.MyappConfig',

Run Project:`python manage.py runserver`

This should open up browser in local host and show 

"The install worked successfully! Congratulations!".


## STEP3 Connecting to database.
Use default sqlite or others

#### Setting up ENviron
`pip install django_environ`

create .env file in project main folder

DB_NAME=fill correct info

DB_USER=fill correct info

DB_PASSWORD=fill correct info

DB_HOST=fill correct info
 


Need to install different sql drivers based on your database preference.


#### Mysql
`pip install pymysql`

Edit  __init__.py in project origin and add following 2 lines

import pymysql

pymysql.install_as_MySQLdb()


#### In Settings.py
DATABASES = {

    'default': {
    
        'ENGINE': 'django.db.backends.mysql',
        
        'NAME':env("DB_NAME"),
        
        'USER':env("DB_USER"),
        
        'PASSWORD':env("DB_PASSWORD"),
        
        'HOST':env("DB_HOST"),
        
        'PORT':"3306",
        
        'OPTIONS':{'init_command': "SET sql_mode='STRICT_TRANS_TABLES'"},
    }

}



#### POSTGRESSQL
`pip3 install psycopg2`


DATABASES = {
    'default': {
    
        'ENGINE': 'django.db.backends.postgresql',
         
        'NAME':env("DB_NAME"),
        
        'USER':env("DB_USER"),
        
        'PASSWORD':env("DB_PASSWORD"),
        
        'HOST':env("DB_HOST"),
        
        'PORT':'5432',
       
       
    }
}









