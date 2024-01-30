# Employee

Employee is the building block of Humane Ressources in LabsManager.
It gather basic information and match with other items through the app. 


## List Page 

The Employee index page list employees, with infos : 

* **id** : the identity of the Employee. There could be 3 icones showing whether the employee is a team leader or team mate, and the hierarchical chart - clic to see teams and chart.
* **Entry date** : the date Employee has join the lab
* **Exit Date** : the date Employee has leave the lab
* **Status** : Employee *current* position, from a list of defined items in parameters
* **Infos** : generic information references for the employee (key, value)
* **Contract Quotity** : *curent* Employee contract quotity
* **project quotity** : *curent* Employee project involvment quotity
* **Superior** : Employee superior, hierarchically
* **is Active** : if an employee is active, regardless of entry/exit date
* **Action** : see [Concept/Shared process](/general/shared_process/#actions)

## Basic Information : 

* **first name** - **last name** - **email** : as basic identity.
* **entry date** :  Enrollement date of the employee
* **exit date** : withdrawal date of the employee
* **Active** : define wether the Employee is active or not in the lab

## Main Panel : Employee General

#### Left side

Here you'll find a summary of basic information and some consolidated data on employee participation in projects.

You can add generic informations. Generic information type are defined in parameters. 

#### right side

Here are Employee's position. they are caractérized by a type and a start and end date.
Position type are defined in parameters.

Position could be used as filter in different type.

#### Menu

5 actions are available in the dropdown menu : 

* Edit Employee : to edit basic informations
* Add Info : to add a position/status
* Add Info : To add a generic information
* Export Word : to export a word report for the current employee
* Export PDF :  to export a pdf report for the current employee (see [export employee](../employee_export/))


## Contract Panel

List all contract for the current employee with admin/edit/delete actions depending on user rights

## Budget Panel

List all budget targeted for the current employee. See [Project Section] for more details

## Contribution Panel

List all contribution for the current employee.  See [Project Section] for more details

## Project Panel

List all project where the current employee is a participant/involved. 
The column Status show both project status (:fontawesome-solid-flask:{ class="twemoji ico mini active middle"}) as well as participant status (:fontawesome-solid-user:{ class="twemoji ico mini inactive middle"}) - <span class="active">active</span> /<span class="inactive">inactive</span>

See [Project Section] for more details

## Teams Panel

List all teams for the current employee, as team leader as well as team mate.


## Leaves Panel

List all leaves for the current employee.

#### Left side
on the left side you have a calendar view of the leaves. refer to [Calendar process](../shared_process/#calendar)  for more details

#### right side
A List all leaves for the current employee, with action button