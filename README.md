# django_cheatsheet

## Always set up an environment

python3.11 -m venv .venv

source .venv/bin/activate

Deactivate at the end with deactivate

## Django setup

- after making a new github project...

Create virtual environment

mkdir django-things (just an example name)

pip install django

django-admin startproject django_things_project .
(the period creates the project in the current directory)

Run tree command to view file structure if necessary.

cd django-things

python manage.py runserver

control C to stop server

python manage.py migrate

charm up

inside settings.py in INSTALLED_APPS, write your apps in string format

Enter the file db.sqlite3

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

## Custom user model

NEW SETUP!

Referenced from [Django Best Practices](https://learndjango.com/tutorials/django-custom-user-model)

1. mkdir project
2. cd project
3. set up VENV
4. pip install django
5. django-admin startproject project
6. tree
7. python manage.py startapp accounts
8. DO NOT MIGRATE UNTIL CUSTOM USER IS SET UP
9. python manage.py runserver
10. charm .
11. add 'accounts' to settings.py under INSTALLED_APPS
12. at the bottom of settings.py, define a new variable called

        AUTH_USER_MODEL = 'accounts.CustomUser'

13. inside models.py, at the top write

        from django.contrib.auth.models import AbstractUser
        from django.db import models

        class CustomUser(AbstractUser):
            pass
            # can add additional fields in here

            def __str__(self):
                return self.username

14. inside accounts folder, create a file called forms.py
15. inside forms.py, write

        from django import forms
        from django.contrib.auth.forms import UserCreationForm, UserChangeForm
        
        #linking our custom user model
        from .models import CustomUser


        class CustomUserCreationForm(UserCreationForm):

            class Meta:
                model = CustomUser
                fields = ("username", "email")

        class CustomUserChangeForm(UserChangeForm)

            class Meta:
                model = CustomUser
                fields = ("username", "email")

16. register model inside admin.py

        from django.contrib import admin
        from django.contrib.auth.admin import UserAdmin

        # Register your models here.
        from .forms import CustomUserCreationForm, CustomUserChangeForm
        from .models import CustomUser

        class CustomUserAdmin(UserAdmin):
            add_form = CustomUserCreationForm
            form = CustomUserChangeForm
            model = CustomUser
            list_display = ["email", "username"]


        admin.site.register(CustomUser, CustomUserAdmin)

17. python manage.py makemigrations accounts
18. python manage.py migrate
19. python manage.py createsuperuser - same superuser steps as before
20. view database, then python manage.py runserver and sign in, here you can view your new custom user interface and settings

## Django forms

inside views.py in the CreateView class, include the line...

    fields = "__all__"

Example form

    {% block content %}
    <form method="POST">
    {% csrf_token %}
    {{form}}
    <input type="submit" value="SUBMIT">
    </form>
    {% endblock content %}

### What every file does

views.py - this is how the model/page is viewed

urls.py - this is where we define routes

templates - this file holds all our html files

### Useful links

- [Flowbite styling components](https://flowbite.com/docs/components/navbar/)

- [Flowbite/Tailwind configuration](https://flowbite.com/docs/getting-started/django/)

- [Django Docs](https://docs.djangoproject.com/en/4.2/)

- [Django Best Practices](https://learndjango.com/tutorials/django-custom-user-model)
