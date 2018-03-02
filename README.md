# django-allauth-hatena

This repository provides a oauth library which can login [hatena](http://www.hatena.ne.jp/) using [django-allauth](https://github.com/pennersr/django-allauth).
You can use this as part of the `allauth.socialaccount.providers`.

# Install

`django-allauth-hatena` can install using pip.

```
$ pip install django-allauth-hatena
```

It is required `django-allauth`, so you should install `django-allauth`.

# Usage
## Basic setting

Please add `allauth_hatena` to your `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth_hatena',
]
```

And, set authentication backend for allauth.

```python
AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
)
```

After that, set socialaccount provider.

```python
# allauth joins multiple scopes with whitespace.
# https://github.com/pennersr/django-allauth/blob/0.35.0/allauth/socialaccount/providers/oauth/views.py#L47
# But, hatena API accept multiple scopes with comma.
# http://developer.hatena.ne.jp/ja/documents/auth/apis/oauth/consumer
# So, you should join with comma when you use multiple scopes.
SOCIALACCOUNT_PROVIDERS = {
    'hatena': {
      'SCOPE': ['read_public,write_public']
    }
}
```


urls.py:

```python
urlpatterns = [
    ...
    url(r'^accounts/', include('allauth.urls')),
    ...
]
```

## Add provider

It is same as [normal django-allauth setting](https://django-allauth.readthedocs.io/en/latest/installation.html#post-installation).

```
$ ./manage.py migrate
```

Now start your server, visit your admin pages (e.g. http://localhost:8000/admin/) and add hatena provider to `Social App`.

# License
The package is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
