---
layout: default
title: Signals
parent: DB Schema
nav_order: 4
---

Q: When would `signals.py` be used in this case?


```
# signals.py

from django.db.models.signals import post_save
from django.contrib.auth.models import User
from django.dispatch import receiver
from .models import UserRegistrationModel


@receiver(post_save, sender=User)
def creater_profile(sender, instance, created, **kwargs):
    if created:
        profile = UserRegistrationModel.objects.create(user=instance)
        profile.save()
```

The `signals.py` file in this case is used to handle signals in Django. Signals allow decoupled applications to get notified when certain events occur elsewhere in the application. In this specific example, the `signals.py` file is used to automatically create a corresponding `UserRegistrationModel` instance whenever a new `User` instance is created.

Here's how it works:

1. `post_save`: This is the signal that is sent after a model's `save()` method is called. In this case, it is used to capture the signal sent after a `User` instance is saved.

2. `@receiver(post_save, sender=User)`: This is a decorator that connects the `creater_profile` function to the `post_save` signal for the `User` model. Whenever a `User` instance is saved, this function will be called.

3. `creater_profile(sender, instance, created, **kwargs)`: This is the function that will be executed when the `post_save` signal is triggered. It takes several arguments:
   - `sender`: The model class that sent the signal (in this case, `User`).
   - `instance`: The actual instance of the model that was just saved (the newly created `User` instance).
   - `created`: A boolean value indicating whether the instance was created (True) or updated (False).
   - `**kwargs`: Additional keyword arguments that might be sent with the signal (not used in this example).

4. `if created:`: This checks if the `User` instance was just created (not updated).

5. `profile = UserRegistrationModel.objects.create(user=instance)`: This line creates a new `UserRegistrationModel` instance and associates it with the newly created `User` instance. It uses the `OneToOneField` relationship defined in the `UserRegistrationModel` to link the two models.

6. `profile.save()`: This saves the newly created `UserRegistrationModel` instance to the database.

So, in summary, the `signals.py` file in this case is used to automatically create a corresponding `UserRegistrationModel` instance whenever a new `User` is created in the application. This ensures that the `UserRegistrationModel` and `User` models are kept in sync, and it is triggered every time a new user account is registered.