# django-oauth2-rest-framework

Create a virtualenv and install following packages using pip...

```
pip install -r requirements.txt

python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Next thing you should do is to login in the admin at

```
http://localhost:8000/admin

```

Register an application

```
http://localhost:8000/o/applications/

```

Click on the link to create a new application and fill the form with the following data:

    Name: just a name of your choice
    Client Type: confidential
    Authorization Grant Type: Resource owner password-based

Get your token and use your API
At this point we’re ready to request an access_token. Open your shell

```
curl -X POST -d "grant_type=password&username=<user_name>&password=<password>" -u"<client_id>:<client_secret>" http://localhost:8000/o/token/
```

Response should be something like:
```
{
    "access_token": "<your_access_token>",
    "token_type": "Bearer",
    "expires_in": 36000,
    "refresh_token": "<your_refresh_token>",
    "scope": "read write groups"
}
```

Grab your access_token and start using your new OAuth2 API:

# Retrieve users
```
curl -H "Authorization: Bearer <your_access_token>" http://localhost:8000/users/
curl -H "Authorization: Bearer <your_access_token>" http://localhost:8000/users/1/

# Retrieve groups
curl -H "Authorization: Bearer <your_access_token>" http://localhost:8000/groups/

# Insert a new user
curl -H "Authorization: Bearer <your_access_token>" -X POST -d"username=foo&password=bar" http://localhost:8000/users/

```




