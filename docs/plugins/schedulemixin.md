## Schedule Mixin
this mixin allows you to add customs event to the calendar views as well as filters and filtering on leaves instances.
```
plugin.mixins.ScheduleMixin
```

This mixin provide the ability to add tasks to background worker to call method at regular interval.

#### Add tasks
to add task, just report their definition in the variable `SCHEDULED_TASKS`
bad formed task will be discarded

```
SCHEDULED_TASKS = {
        # Name of the task (will be prepended with the plugin name)
        'test_task': {
            'func': 'myplugin.tasks.test_server', 
            'schedule': "I",
            'minutes': 30,
            'repeats': 5,
        },
    }
```

**Options :**

* test_task : will be the name of the task in tasks list (with plugin slug)
* func : a function to call, without argument. Dotted notation will call a python function. Without dot it will call a class member method
* schedule : schedule type, please refer to [django_q.schedule](https://django-q.readthedocs.io/en/latest/schedules.html#)
* repeat : Number of repeats (leave blank to let it go forever)