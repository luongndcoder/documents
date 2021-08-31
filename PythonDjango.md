## Start Install Python Django
    - python -m pip install Django
    -  python -m django --version
# Create First Project
    - django-admin startproject mysite
    
    - mysite/
        manage.py
        mysite/
            __init__.py
            settings.py
            urls.py
            asgi.py
            wsgi.py

# Run server 
    - python manage.py runserver
    - or python manage.py runserver 8080 
    - or python manage.py runserver 0:8000

# create first application
    - python manage.py startapp polls
    - polls/
        __init__.py
        admin.py
        apps.py
        migrations/
            __init__.py
        models.py
        tests.py
        views.py

# create views 
    - in polls/views
    - input: 
        - from django.http import HttpResponse
        - def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
    - create file urls.py in application polls
    - open file pools/urls.py
        - from django.urls import path
        - from . import views
        - urlpatterns = [
            path('', views.index, name='index'),
        ]
    - open path mysite
    - open file mysite/urls.py
        - from django.contrib import admin
        - from django.urls import include, path

        - urlpatterns = [
            path('polls/', include('polls.urls')),
            path('admin/', admin.site.urls),
        ]
    - run server ->  python manage.py runserver


# Config Database Postgres 
    - sudo su postgres 
    - psql
    - create database django_ecommerce encoding 'utf-8';
    - if user not found : create user admin with password '123456';
    - grant all privileges on database django_ecommerce to admin;
    - alter user admin CREATEDB;
    - open file mysite/settings.py
    - config databases:
        DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'django_ecommerce',
            'USER': 'admin',
            'PASSWORD': '123456abcA',]
            'PORT': '5432'
        }
    }
    - python manage.py migrate

    - create table in applications polls
        - open file polls/models.py
            - wirte 
            class Question(models.Model):
            question_text = models.CharField(max_length=200)
            pub_date = models.DateTimeField('date published')


        class Choice(models.Model):
            question = models.ForeignKey(Question, on_delete=models.CASCADE)
            choice_text = models.CharField(max_length=200)
            votes = models.IntegerField(default=0)
    - open file mysite/settings.py
        - add application polls to config
        - INSTALLED_APPS = [
            'polls.apps.PollsConfig',
            'django.contrib.admin',
            'django.contrib.auth',
            'django.contrib.contenttypes',
            'django.contrib.sessions',
            'django.contrib.messages',
            'django.contrib.staticfiles',
        ]
        - python manage.py makemigrations polls
        