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




## STEP4 STATIC FILES Using AWS S3 Bucket
#### Step1
1. Login to aws
2. Search s3 and click
3. Create bucket-choose copy settings from existing user
4. Object ownership > choose ACLS enable
5. Disable block all public access
6. Others keep same
7. Click create bucket
8. Inside bucket create 2 folders a)static b)build

#### Step 2

1. Now select security and credentials from account eg: yournam
2. Click Users > Add Users
3. Select Aws credential type =accesskey
4. Set permissions> Copy permisssions from existing user
5. Select existing user with correct credentials
6. next > Next > create User
7. Download CSV for 
8. AccessKeyid=
9. SecretaccessKey =

#### Step 3 Update settings.py
On Local Terminal  & settings.py

`pip install boto3`

`pip install django-storages`



Inside settings.py

Import os

#S3 BUCKETS CONFIG 

AWS_ACCESS_KEY_ID = env("AWS_ACCESS_KEY_ID"),

AWS_SECRET_ACCESS_KEY = env("AWS_ACCESS_KEY_ID"),

AWS_STORAGE_BUCKET_NAME = env("AWS_ACCESS_KEY_ID"),

#AWS_S3_FILE_OVERWRITE = False

AWS_S3_CUSTOM_DOMAIN = f'{AWS_STORAGE_BUCKET_NAME}.s3.amazonaws.com'

AWS_DEFAULT_ACL = 'public-read'

AWS_S3_OBJECT_PARAMETERS = {'CacheControl': 'max-age=86400'}

AWS_LOCATION = 'static'

AWS_QUERYSTRING_AUTH = False

AWS_HEADERS = {'Access-Control-Allow-Origin': '*'}

DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'

STATICFILES_STORAGE = 'storages.backends.s3boto3.S3StaticStorage'

STATIC_URL = f'https://{AWS_S3_CUSTOM_DOMAIN}/static/'

#STATIC_URL = '/static/'

MEDIA_URL = f'https://{AWS_S3_CUSTOM_DOMAIN}/media/'

if DEBUG:

    STATICFILES_DIRS=[
    
    os.path.join(BASE_DIR, 'build/static'),
    ]
    
else:

    STATIC_ROOT=os.path.join(BASE_DIR, 'build/static')

