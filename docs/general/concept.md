# Basic Concepts

This section describe the differents objects used throughout the application

LabM rely on three main pillar and their relation :
<p style="text-align: center; font-weight: bold;">Employee <> Project <> Fund</p>

Quite all list subjacent in above description are customizable direcly in the application

## LabsManager Items

### :fontawesome-solid-user: Employee
An Employee describe an employee of the Lab!
The main information detail his identity, birthdate, email and enrollement dates, as well as it status actif/non actif.

It can be further describes by adding positions with dates.
Finally, you can set supervisors, who are other Employees.

Further information on [Employee page](../employee) 

### :fontawesome-solid-flask: Project

Projects represent management units that gather identity, background, tutelary institution and participant data.

The background management of a project can be spread over several institutions.t,

### :fontawesome-solid-money-bill: Fund

Fund are the representation of the way project are funded. 
It reference a Funder, an Institution (which manage the fund for the lab) and eligibilities dates. Fund are filled with Fund_Items caracterized by a type (Functionnement, Human Ressource, Equipment, ...). Types are defined in Parameters

### :fontawesome-solid-file-signature: Contract

Contract is the entity which links Employee to a Fund (a Fund is specific of a project) and start/end dates, quotity.

### :fontawesome-solid-people-group: Team

Team is an object to gather employees in unic entity.

### :fontawesome-solid-calendar-days: leave

Leaves are date or period referenced for Employee, caractérized by a type (define in parameters)


### Django Basics

#### User
User for LabsManager is the basic user model from Django
A single user can be bind to an employee. This allow in right management a user to access to his employee's data without having right on other items.

