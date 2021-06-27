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
must write **keys.py** in .gitignore file for inaccessibility other user.
**keys.py** file for important variable
```
# .gitignore
keys.py
```
3. run `python manage.py check --deploy`: this command shows all things that must 
do for security
```
# python manage.py check --deploy

System check identified some issues:

WARNINGS:
?: (security.W004) You have not set a value for the SECURE_HSTS_SECONDS setting. If your entire site is served only over SSL, you may
want to consider setting a value and enabling HTTP Strict Transport Security. Be sure to read the documentation first; enabling HSTS c
arelessly can cause serious, irreversible problems.
?: (security.W006) Your SECURE_CONTENT_TYPE_NOSNIFF setting is not set to True, so your pages will not be served with an 'X-Content-Ty
pe-Options: nosniff' header. You should consider enabling this header to prevent the browser from identifying content types incorrectl
y.
?: (security.W007) Your SECURE_BROWSER_XSS_FILTER setting is not set to True, so your pages will not be served with an 'X-XSS-Protecti
on: 1; mode=block' header. You should consider enabling this header to activate the browser's XSS filtering and help prevent XSS attac
ks.
?: (security.W008) Your SECURE_SSL_REDIRECT setting is not set to True. Unless your site should be available over both SSL and non-SSL
 connections, you may want to either set this setting True or configure a load balancer or reverse-proxy server to redirect all connec
tions to HTTPS.
?: (security.W012) SESSION_COOKIE_SECURE is not set to True. Using a secure-only session cookie makes it more difficult for network tr
affic sniffers to hijack user sessions.
?: (security.W016) You have 'django.middleware.csrf.CsrfViewMiddleware' in your MIDDLEWARE, but you have not set CSRF_COOKIE_SECURE to
 True. Using a secure-only CSRF cookie makes it more difficult for network traffic sniffers to steal the CSRF token.
?: (security.W018) You should not have DEBUG set to True in deployment.
?: (security.W019) You have 'django.middleware.clickjacking.XFrameOptionsMiddleware' in your MIDDLEWARE, but X_FRAME_OPTIONS is not se
t to 'DENY'. The default is 'SAMEORIGIN', but unless there is a good reason for your site to serve other parts of itself in a frame, y
ou should change it to 'DENY'.
?: (security.W020) ALLOWED_HOSTS must not be empty in deployment.
```
4. 