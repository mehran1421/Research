# Security in Django project

1. `Debug = False` in settings.py file because if True it,
Displays all errors with the path and attacker can through that path 
damage and deactivate system
in **production.py** file, it must Debug=False and 
in **development.py** file, it must Debug=True because 
in this file developer must understand the path of error 
```
-config
        __init.py
        -settings
                -__init__.py
                -base.py
                -development.py
                -keys.py
                -local.py
                -production.py
        -asgi.py
        -urls.py
        -wsgi.py
```

2. Hide `SECRET_KEY` in settings.py file because **SECRET_KEY** use in authentication user 
that if the attacker has it can login with superuser and change or to steal information.
for hide **SECRET_KEY** must write in **keys.py** file:
```
# keys.py
SECRET_KEY = 'django-insecure-rmi=!(%9$2lh-(t6q7g6&9+j#nh38exz=@5y0ym@p7imz@s537'
```
must write **keys.py** in .gitignore file for inaccessibility other user
```
# .gitignore
keys.py
```
