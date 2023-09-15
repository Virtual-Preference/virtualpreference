
# Virtual Preference System APIs Connector 

The library ```virtualpreference``` is used to access the Virtual Preference System APIs. It includes the pure python implementation and a special support to Django Framework.

Before using the library first install it.
```
pip install virtualpreference
```
**STORAGE SYSTEM**
```python
from virtualpreference.storage.core import VPStorage

vp_storage = VPStorage()

# Assign your API Key.
vp_storage.api_key = "API_KEY"

# To push file to Virtual Preference Storage System
vp_storage.push(
    file_name="example.png", content_type="image/png", content="file_object"
)

# To destroy or delete the file from remote storage pass
# the file reference which is received from push method.
vp_storage.destory(
    reference="4fff03ba-f765-4520-83ee-be4fcc50a1b2"
)

# The file will be replaced with old file but the reference or uuid
# remain same.
vp_storage.replace(
    reference="4fff03ba-f765-4520-83ee-be4fcc50a1b2",
    file_name="example.png", content_type="image/png",
    content="file_object"
)
```
**DJANGO IMPLEMENTATION**

To support auto delete the files when you delete from Django Admin Panel or change file from Django Admin Panel. So in this case
you can use ```django-cleanup``` module or install with ```pip install django-cleanup```
```python
from virtualpreference.storage.django import VPBucket

# Setup of django-cleanup module is optional, but it is recommended
# if you want to support auto deletion, but it has some limitation
# check it on https://pypi.org/project/django-cleanup/

INSTALLED_APPS = [
    ...,
    'django_cleanup.apps.CleanupConfig',
]

VPSTORAGE_API_KEY="API_KEY"

STORAGES = {
    "default": {
        "BACKEND": "virtualpreference.storage.django.VPBucket"
    },
    "staticfiles": {
        "BACKEND": "django.contrib.staticfiles.storage.StaticFilesStorage",
    },
}
```

