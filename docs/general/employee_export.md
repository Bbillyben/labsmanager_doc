# Employee Exports

In LabsManager you can export employee informations with a report template. Employee's report are constrain between two dates. By default the modal propose dates over the last year.

Two default reports are included :

* standard report : report all items for an employee
* leave report : report all leaves between two dates defined in the modal

Template can be uploaded in the admin interface, both for word export, in word file, or for pdf export, by an html file. 

You can access several information in templates, shared both by word and pdf reports.Below is a great overview of the variable you can use in your template.


### use

Word templates are rendered by [Jinja](https://jinja.palletsprojects.com/en/3.1.x/) engine, 

Pdf templates are rendered by WeasyTemplateResponseMixin, which rely on Django TemplateResponseMixin.


Template syntaxe for variable with double brackets `{{var}}`

Iterable items presented below are described in loop like : 
```
{% for item in [ITERABLE] recursive %}
    {{item.[KEY]}}
{% endfor %}
```

### General Information

* **{{date}}** :current date of the export
* **{{datetime}}** :current datetime of the export
* **{{datetime_SI}}** :current datetime of the export formatted *YEAR_MONTH_DAY*
* **{{report_description}}** :description of the current template
* **{{report_name}}** :name of the current template
* **{{report_revision}}** : revision of the current template
* **{{request}}** :the request send to ask for the report, the request contain for instance : 
    * **{{request.GET.start_date}}** :the start date defined in the modal
    * **{{request.GET.end_date}}** :the end date defined in the modal  
    * **{{request.site.name}}** :the name of the site
* **{{user}}** :current user who request the report

### Employee Information
* **{{employee}}** :Employee instance
    * **{{employee.first_name}}** :Employee's first name   
    * **{{employee.last_name}}** :Employee's last name 
    * **{{employee.birth_date}}** :Employee's birth date
    * **{{employee.email}}** :Employee's email
    * **{{employee.entry_date}}** :Employee's incorporation date
    * **{{employee.exit_date}}** :Employee's exit date
    
### Generic Information

* **{{info}}** *iterable* :Generic info attached to the employee
    * **{{item.info}}** : the generic information
    * **{{item.value }}** : the generic information value

### Status/Position Information

* **{{status}}** *iterable* :Status/position of the employee
    * **{{item.type.name}}** : the position type name
    * **{{item.start_date  }}** : the start date of the position
    * **{{item.end_date  }}** : the end date of the position    
    * **{{item.get_is_contractual_display()  }}** : the end date of the position  

### Contract Information

* **{{contract}}** *iterable* :contract of the employee
    * **{{item.fund}}** : the fund which the contract is attached to. Contains variable from the Fund model. You can reach for instance : 
        * **{{item.fund.project.name}}** : the project name which the fund is attached to
        * **{{item.fund.funder.short_name }}** : the short name of the funder referenced for the fund
        * **{{item.fund.institution.short_name  }}** : the short name of the Institution referenced as manager for the fund      
        * **{{item.fund.ref}}** : the reference of the fund
    * **{{item.start_date}}** : the start date
    * **{{item.end_date}}** : the end date    
    * **{{item.contract_type}}** : the type of the contract (defined in parameter)
    * **{{item.quotity}}** : the work quotity of the contract
    * **{{item.total_amount}}** : the cost of the contract reported 

### Project Information

* **{{project}}** *iterable* :participation in project of the employee
    * **{{item.project}}** : the project which the employee participe to. Contains variable from the project model. You can reach for instance : 
        * **{{item.project.start_date}}** : the project start date
    * **{{item.get_status_display()  }}** : the status of the employee as participant
    * **{{item.start_date}}** : the start date of the participation of the employee
    * **{{item.end_date}}** : the end date    

### teams Information

* **{{teams}}** *iterable* :teams where the employee is invloved in
    * **{{item.name}}** : team name
    * **{{item.leader}}** :  the team leader - an employee instance 
        * **{{item.leader.user_name}}** :  the team leader user name (first name last name)

### Contribution Information

* **{{Contribution}}** *iterable* :participation in project of the employee
    * **{{item.fund}}** : the fund which the contribution is attached to. Contains variable from the Fund model. You can reach for instance : 
        * **{{item.fund.project.name}}** : the project name which the fund is attached to
        * **{{item.fund.funder.short_name }}** : the short name of the funder referenced for the fund
        * **{{item.fund.institution.short_name  }}** : the short name of the Institution referenced as manager for the fund  : 
        * **{{item.project.start_date}}** : the project start date
    * **{{item.cost_type}}** : the cost type of the contribution (defined in parameters) 
    * **{{item.start_date}}** : the start date of the contribution
    * **{{item.end_date}}** : the end date  

### Leaves Information   
* **{{leave}}** *iterable* :leave of the employee, constrain to the timeslot defined in the modal
    * **{{item.type}}** : the type of the leave, defined in parameter
        * **{{item.type.short_name}}** : the short name of the type
        * **{{item.type.name}}** : the full name of the type
        * **{{item.type.color}}** : the color attached to the type
    
    * **{{item.start_date}}** : the start date of the leave
    * **{{item.end_date}}** : the end date  
    * **{{item.comment}}** : the comment attached to the leave
    * **{{item.start_period}}** : the start period of the leave: *ST* for the beginning of the day, *MI* for the middle
    * **{{item.end_period}}** : the start period of the leave: *MI* for the middle of the day, *EN* for the end