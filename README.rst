Django rest-framework Starter
===================================

A DRF starting project to achieve server side authentication for hybrid apps.


Installation
------------

Install with pip::

    pip install -r requirements.txt
    cd api
    python manage.py migrate

Post-Installation
------------

Now start your server, visit your admin pages (e.g. http://localhost:8000/admin/) and follow these steps:

1. Add a Site for your domain, matching settings.SITE_ID (django.contrib.sites app).
2. For each OAuth based provider, add a Social App (socialaccount app).
3. Fill in the site and the OAuth app credentials obtained from the provider.

Testing the setup
-----------------

- Now that the installation is done, let's try it ! Register a user using curl :

    curl -X POST -d "username=<user_name>&password1=<password1>&password2=<password2>&email=<email>" http://localhost:8000/rest-auth/registration/

- Login and ask a token for an user using curl:

    curl -X POST -d "username=<user_name>&password=<password>" http://localhost:8000/rest-auth/login/

- Logout:

    curl -X POST http://localhost:8000/rest-auth/logout/

- Password reset using curl:

    curl -X POST -d "email=<email>" http://localhost:8000/rest-auth/password/reset/

    curl -X POST -d "uid=<uid>&token=<token>&new_password1=<new_password1>&new_password2=<new_password2>" http://localhost:8000/rest-auth/password/reset/confirm/

- Change password using curl:

    curl -X POST -d "old_password=<old_password>&new_password1=<new_password1>&new_password2=<new_password2>" http://localhost:8000/rest-auth/password/change/

If you have any questions feel free to ask me.


Social Authentication
---------------------

Facebook example request :

    curl -X POST -d "access_token=<access_token>" http://localhost:8000/rest-auth/<facebook>/

This request returns the "access_token" that you should use on all HTTP requests with DRF. What is happening here is that we are converting a third-party access token (<user_access_token>) in an access token to use with your api and its clients ("access_token"). You should use this token on each and further communications between your system/application and your api to authenticate each request and avoid authenticating with FB every time.

You can find the id and secret of your app at https://developers.facebook.com/apps/.

For testing purposes you can use the access token `<user_access_token>` from https://developers.facebook.com/tools/accesstoken/.

For more information on how to configure python-social-auth with Facebook visit http://django-allauth.readthedocs.org/.
