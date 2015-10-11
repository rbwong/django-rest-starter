Django rest-framework Starter
===================================

This module provides a python-social-auth and oauth2 support for django-rest-framework.

The first aim of this package is to help setting up social auth for your rest api. It also helps setting up your Oauth2 provider.

This package is relying on `python-social-auth <http://psa.matiasaguirre.net/docs/index.html>`_ and `django-oauth-toolkit <https://django-oauth-toolkit.readthedocs.org>`_.
You should probably read their docs if you were to go further than what is done here.
If you have some hard time understanding Oauth2 you can read a simple explanation `here <https://aaronparecki.com/articles/2012/07/29/1/oauth2-simplified>`_.


Installation
------------

Install with pip::

    pip install -r requirements.txt
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

If you have any questions feel free to ask me.


Social Authentication
---------------------

Facebook example request :

    curl -X POST -d "access_token=<access_token>" http://localhost:8000/rest-auth/<facebook>/

This request returns the "access_token" that you should use on all HTTP requests with DRF. What is happening here is that we are converting a third-party access token (<user_access_token>) in an access token to use with your api and its clients ("access_token"). You should use this token on each and further communications between your system/application and your api to authenticate each request and avoid authenticating with FB every time.

You can find the id and secret of your app at https://developers.facebook.com/apps/.

For testing purposes you can use the access token `<user_access_token>` from https://developers.facebook.com/tools/accesstoken/.

For more information on how to configure python-social-auth with Facebook visit http://django-rest-auth.readthedocs.org/
