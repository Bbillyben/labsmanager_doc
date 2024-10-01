## Calendar Mixin
this mixin allows you to add customs event to the calendar views as well as filters and filtering on leaves instances.
```
plugin.mixins.CalendarEventMixin
```

#### add customs filters

To implement custom filters you only have to valorize the FILTERS vars. FILTERS should be a dict of key, which will be used as filter name and options like : 
```
FILTERS={
            "TEST_CHOICES":{ 
                "title":"Test Choices",
                "type":"select",
                "choices":{ 
                    "val1":"Value 1",
                    "val2":"Value 2",
                    ....
                }
                "default":"default value"
        },            
    }
```
"TEST_CHOICES" will be used as filter name in lower case. It will be listed in filters list as [my_plugin_slug]-test_choices

options :

* title: *mandatory* is the title prompted in the calendar filter box title
* type : is the type of filter to be used. It's restricted to : 
    * select : to display an html select / dropdown selector
    * radio : to display a radio box selector
    * checkbox : to display a check box by choice
    * input-text : a text input type
    * input-color : a color input type
* choices : *mandatory for select, radio, checkbox* are a dict of value:name
    * value : is the value of the item
    * name : is the prompt of the item
    choice can also be a *classmethod* name :
    ```
    "choices":"myClassMethod"   # could be the string name of a  as well
    ```

* default : is the default value of the filter. for checkbox, provide a string list of value to be checked, for instance :
```
"default":"val1,val3",
```


:warning: if type is not in authorized type or if choices are bad formatted, the filter will be discarded.


#### filtering Leave instance
To filter original leaves instance to be displayed in the calendar, overwrite the method : 
```
@classmethod
    def filter_queryset(cls, queryset, filters_data):
    return queryset
```

should return the new queryset. 
Args : 
* queryset : the queryset comming from the labsmanager filtering process of leave instances
* filters_data : dict containing the filters, including FILTERS value (under `[my_plugin_slug]-[my_filter_name]:value`)



#### add custom event
To add customs event to be displayed in the calendar, overwrite the method : 
```
@classmethod
    def get_event(cls, request, event_list):
        pass
```



Args : 
* request : the request object from labcalendar. request GET or POST contain information about date slots, calendar filters + filters from plugins, including : 
    * type : type filter of leave.model.leave_type
    * type_exact : if has to filter on tree (default for calendar)
    * emp_status : employee status filter (staff.model.employee_type)
    * team : team filter from staff.model.team
    * showResEventRadio : filter, whether only resource with event are printed (false, true, only_today)
    * view : the current view (! not update on view change, only when event resource are reloaded)
    * start : the start date of the time frame
    * end : the end date of the time frame
    * timezone
    * settings : the setting object of the calendar, which contain :
        * cal_type : depict what type of calendar the request coming from (main, team, employee)
    * resources : the current resources !!! may not be up to date prefer `__class__.get_current_resources(request)` for more reliable data
    * every custom filter formatted as  `[my_plugin_slug]-[my_filter_name]:value`
* event_list : a list of event from plugin to be added

extends event_list with new event to add in the calendar display.

