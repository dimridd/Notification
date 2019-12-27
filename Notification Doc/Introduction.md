# Introduction

Django-Notification is the github type app for django derived from django-activity-stream. 

Read the full [Django-Notification Docs](https://pypi.org/project/django-notifications-hq/).

Notification are categorized by 4 main components:

- **actor:** actor are the object that perform the activity.
- **verb:** verb identifies the action of the activity. They are the description which determines the type of the action performed on the activity.
- **action-object:** The object linked to the action itself.
- **target:** Target are the object to which the activity is performed. 

### Description

Actor, Action Object and Target are GenericForeignKeys to any arbitrary Django object. An action is a description of an action that was performed (Verb) at some instant in time by some Actor on some optional Target that results in an Action Object getting created/updated/deleted.

To generate an notification anywhere in your code, simply import the notify signal and send it with your actor, recipient,and verb.


```md
from notifications.signals import notify
notify.send(user, recipient=user, verb='you reached level 10')
```

The complete syntax is.
```md
notify.send(actor, recipient, verb, action_object, target, level, description, public, timestamp, **kwargs)
```

**Arguments**:
- **actor:** An object of any type. (Required) Note: Use sender instead of actor if you intend to use keyword arguments
- **verb:** An string. (Required)
- **action_object:** An object of any type. (Optional)
- **recipient:** A Group or a User QuerySet or a list of User. (Required)
- **target:** An object of any type. (Optional)
- **level:** One of Notification.LEVELS (‘success’, ‘info’, ‘warning’, ‘error’) (default=info). (Optional)
- **description:** An string. (Optional)
- **public:** An boolean (default=True). (Optional)
- **timestamp:** An tzinfo (default=timezone.now()). (Optional)

To return unread notification for a single user, we can do
```md
user = User.objects.get(pk=pk)
user.notifications.unread()
```
and, for all the user we do
```md
Notification.objects.unread()
```

The following syntax mark all of the read notifications in the queryset as read.
```md
qs.mark_all_as_read()
```

The following syntax mark all of the read notifications in the queryset as unread.
```md
qs.mark_all_as_unread()
```


