# django_cheatsheet

## Always set up an environment

python3.11 -m venv .venv

source .venv/bin/activate

Deactivate at the end with deactivate

## Django setup

- after making a new github project...

Create virtual environment

python3.11 -m venv .venv
source .venv/bin/activate

mkdir django-things (just an example name)

pip install django

django-admin startproject django_things_project .
(the period creates the project in the current directory)

Run tree command to view file structure if necessary.

cd django-things

python manage.py runserver

control C to stop server

python manage.py migrate

charm up and enter the file db.sqlite3

refresh the page (click main then hit the refresh button)

## Creating and connecting an app to the project

python manage.py startapp things (also example name)

inside the settings.py under INSTALLED_APPS list, add things to the list,
this adds the new app to our django_things_project

create a directory (folder) called templates with a file called base.html inside

initialise with ! to create boilerplate for html file - [emmet html tags](https://www.freecodecamp.org/news/write-html-css-faster-with-emmet-cheat-codes/#:~:text=With%20Emmet%20you%20can%20quickly,web%20page%20ready%20to%20go.)

{% block content %}

{% endblock content %}

## Adding templates folder

start by going to settings.py and got to the templates folder and place inside 'DIRS'
BASE_DIR / 'templates'

Create a templates folder on the same level as the project folder

add a base.html with setup, and any other html files necessary

## Django models

inside your specific app (for example things) go into models.py and import
from django.contrib.auth import get_user_model

all models are made up of classes: (name classes singularly, such as Thing or Snack)

    class Thing(models.model):
        # Create a class variable for each field
        # Assign a field type, and include field options
        name = models.CharField(max_length=256)
        rating = models.IntegerField(default=0)
        reviewer = models.ForeignKey(get_user_model(), on_delete=models.CASCADE)

        def __str__(self):
            return self.name
Example class

after setting up the admin panel, register the model in admin.py in the app

from .models import Thing

every time you make a model, make sure to run 

- python manage.py makemigrations
- after all models are made, run python manage.py migrate

## Admin panel

python manage.py createsuperuser

This command will prompt you to put in a name, email, and password

You can optionally put in an email, but make the name admin and use a good developing password, use something like admin1234

then type y if password to short error comes up



### What every file does

urls.py - this is where we define routes
