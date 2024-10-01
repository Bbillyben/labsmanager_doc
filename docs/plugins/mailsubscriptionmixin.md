## Mail Subscription Mixin
this mixin allows you to add customs context data and template to the mail send for item subscription.
```
plugin.mixins.CalendarEventMixin
```

### add context data
To add customs context data, extend the method : 

```
@classmethod
    def add_context(cls, user, current_context):
        pass
```

Args : 

* user : the user to whom the mail will be sent
* current_context : a copy the current context for rendering (do not alterate, useless, just for informations purpose 

datas will be added to the global email context accessible by plugin's slug : [slug].[myData]

### add templates

just override the variable `TEMPLATE_FILES` with the names of templates to add at the bottom of the mail (before footer) :
```
TEMPLATE_FILES = ["my_template1.html", "my_template2.html"]
```
template has to be stored in the folder :
```
├─┬──── MyPlugin
│ ├─ __init__.py
│ ├─ MyPlugin.py
│ ├──┬── templates
│ │  ├─┬─ MyPlugin
│ │  │ ├── my_template1.html
│ │  │ ├── my_template2.html

```

:warning: if a template file do not exist it will be discarded.

