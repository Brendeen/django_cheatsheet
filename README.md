# django_cheatsheet

## Always set up an environment

python3.11 -m venv .venv

source .venv/bin/activate

Deactivate at the end with deactivate

## Django setup

mkdir django-things (just an example name)

pip install django

django-admin startproject django_things_project .

Run tree command to view file structure if necessary.

cd django-things

python manage.py runserver

python manage.py migrate

control C to stop server

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

## What every file does

urls.py - this is where we define routes