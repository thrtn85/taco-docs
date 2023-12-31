---
layout: default
title: Models
parent: DB Schema
nav_order: 3
---

```
# models.py

from django.db import models
from django.conf import settings
# Create your models here.


class UserRegistrationModel(models.Model):
    user = models.OneToOneField(
        settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
```

The `models.py` file defines a Django model named `UserRegistrationModel` that establishes a one-to-one relationship with the default user model in Django, which is specified in the `settings.AUTH_USER_MODEL` setting.

Let's break down the code to understand its purpose:

1. `from django.db import models`: This imports the `models` module from Django, which provides the tools for defining database models.

2. `from django.conf import settings`: This imports the `settings` module from Django, which allows access to the application's settings.

3. `class UserRegistrationModel(models.Model):`: This defines a Django model named `UserRegistrationModel`. The model inherits from `models.Model`, which is the base class for all Django models.

4. `user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)`: This line defines a field named `user` of type `OneToOneField`. The `OneToOneField` establishes a one-to-one relationship between `UserRegistrationModel` and the model specified in `settings.AUTH_USER_MODEL`.

   - `settings.AUTH_USER_MODEL`: This refers to the Django user model that is currently being used for authentication in the project. It allows the `UserRegistrationModel` to establish a one-to-one relationship with the user model, which means each `UserRegistrationModel` instance can be associated with only one user, and vice versa.

   - `on_delete=models.CASCADE`: This argument specifies the behavior when the referenced user is deleted. In this case, `models.CASCADE` means that when a user is deleted, the corresponding `UserRegistrationModel` instance will also be deleted.

The purpose of this model seems to be to extend the default user model in the Django application and add additional information related to user registration. By using a one-to-one relationship, it ensures that each user has only one associated registration instance, and it allows you to keep the user-related data separate from the default user model while maintaining a direct relationship between them.