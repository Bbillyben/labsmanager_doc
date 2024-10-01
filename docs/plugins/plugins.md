# Plugins

LabsManager has plugin features for several items in through the app.

## managing plugins

There is several type of plugin :

* *integrated ones*: like builtins (not deactivatable) and samples (can be desactivated)
* *customs*: has to be saved in data/plugin/MyPlugin folder 

#### Activation
Each plugin, except built-in, has to be activated in the plugin admin page. If an error occur during activation, it will be reported  in that page.

Once activated, each plugin will have a dedicated admin page, gathering information on it. For Setting plugins, those setting will be accessible in that page.


## implement your own plugin
Your plugin files have to be pasted in data/plugin/[MyPlugin] folder 
this folder should contains the __init__.py file to spot it as a module one, and the plugin class in a file named as the plugin.

You class has to extends labsmanager plugin file (plugin.LabManagerPlugin), and one or several of the mixin to enable your plugin doing something!

As for now, plugin mixin allos you to : 

* add event and filter to calendar view: [CalendarEventMixin page](../calendarmixin) 
* add datas and template to notification emails: [MailSubscriptionMixin page](../mailsubscriptionmixin)
* run background tasks: [ScheduleMixin page](../schedulemixin)
* add general setting (admin only)

more to come....

