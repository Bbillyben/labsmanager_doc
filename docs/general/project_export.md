# Project Export


In LabsManager you can export project's informations with a report template.

One default reports are included to report all items for a project

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

### Project Information
* **{{project}}** :an instance of project model


### Institution Information
* **{{institution}}** *iterable* :list of participant institution


### Participant Information
* **{{participant}}** *iterable* :list of participant employee


### Contract Information

* **{{contract}}** *iterable* :contract of the employee
    * **{{item.employee}}** : employee contract
         * **{{item.employee.user_name}}** : employee user name
    * **{{item.fund}}** : the fund which the contract is attached to. Contains variable from the Fund model. You can reach for instance : 
        * **{{item.fund.funder.short_name }}** : the short name of the funder referenced for the fund
        * **{{item.fund.institution.short_name  }}** : the short name of the Institution referenced as manager for the fund      
        * **{{item.fund.ref}}** : the reference of the fund
    * **{{item.start_date}}** : the start date
    * **{{item.end_date}}** : the end date    
    * **{{item.contract_type}}** : the type of the contract (defined in parameter)
    * **{{item.quotity}}** : the work quotity of the contract
    * **{{item.total_amount}}** : the cost of the contract reported 