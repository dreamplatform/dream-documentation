
UserDB API documentation, version 1
***********************************

The API endpoint is https://id.dreamschool.fi/api/1/
where 1 is the API version number.

Format is JSON when sending and receiving data. All string fields 
can contain Unicode in UTF-8 format. 

.. note::

  It is possible that the API will change without version number 
  increase if the change does not break backwards compatibility. 

.. note:: 

  Unique identifier fields currently return only autoincremented 
  numbers (0-9), but it is good to be future compatible and think these 
  as strings if the implementation is switched to use UUID.

Organisation
============

id
  *string* - Unique identifier
name
  *string* - Human readable identifier used in URLs 
title
  *string* - Freeform title for the organisation 

The organisation is the top level object type. It organizes the users 
into logical groups. Object types ``role`` and ``group`` are tied to 
the organisation. 

/organisation/
--------------

**GET**
  Returns all objects

/organisation/<id>/
-------------------

**GET**
  Returns one object by ``id``.

Permission
===========

name
  *string* - Unique identifier for the permission

Permissions are global across all services. When new services 
are registered to the system they need to define the 
permissions they provide. 

The identifier has three parts separated by dots. 
Spaces are not allowed. First two dots are used by the UserDB
to split the string to three parts. The first part is used 
by the UserDB to identify which service this permission object
belongs to. Last two parts are specified by the service. Last part
can contain additional dots.

service
  Service name
object
  Object type, or model name, or database table or anything similar
action
  The action user is taking

User gains permissions from ``role`` objects. 

.. note::

  User *Teppo* belongs to organisation *kasavuori* and has role *teacher* in that
  organisation. The role *teacher*, in *kasavuori*, has given permission
  *dscms.article.create_article*. Now *Teppo* has permission to add new 
  articles in the CMS service to *kasavuori* website. 

Role
====

id
  *string* - Unique identifier
name
  *string* - Human readable identifier used in URLs 
title
  *string* 
organisation
  *object* - Contains all fields specified in the ``organisation`` object
permissions
  *list of objects* - Contains all fields specified in the ``permission`` object

/role/
------

**GET**
  Returns all objects

/role/<id>/
-----------

**GET**
  Returns one object by ``id``.

/role/organisation/<id>/
------------------------

**GET**
  Returns all objects by ``organisation`` ``id``.

Group
=====

id
  *string* - Unique identifier
name
  *string* - Human readable identifier used in URLs 
title
  *string* 
organisation
  *object* - Contains all fields specified in the `organisation`` object

/group/
-------

**GET**
  Returns all objects

/group/<id>/
------------

**GET**
  Returns one object by ``id``.

/group/organisation/<id>/
-------------------------

**GET**
  Returns all objects by ``organisation`` ``id``.

User
====

id
  *string* - Unique identifier
name
  *string* - Human readable identifier used in URLs 
username
  *string* - Username user uses to log in to the system
first_name
  *string* - First name of the user
last_name
  *string* - Last name of the user
email
  *string* - Needs to be in proper email format
phone_number
  *string* - Phone number format is specified by Zeecore
locale
  *string* - User locale in the form ``fi_fi``
picture_url
  *string* - Needs to be proper URL
theme_color
  *string* - In hex value, format ``RRGGBB``
roles
  *list of objects* - Contains all fields specified in the ``role`` object
permissions
  *list of objects* - Contains all fields specified in the ``permission`` object
organisations
  *list of objects* - Contains all fields specified in the ``organisation`` object
groups
  *list of objects* - Contains all fields specified in the ``group`` object

.. note:: 

  There are additional fields returned, but they are subject to change
  without notice. 

/user/
------

**GET**
  Returns all objects

/user/<id>/
-----------

**GET**
  Returns one object by ``id``.

**PUT**
  Updates fields in the object. Allowed fields are:
  first_name, last_name, password, email, phone_number, theme_color, picture_url, 
  groups, roles, and organisations. Fields groups, roles, and organisations should 
  be list of unique identifiers. 

/user/organisation/<id>/
------------------------

**GET**
  Returns all objects by ``organisation`` ``id``.

/user/role/<id>/
----------------

**GET**
  Returns all objects by ``role`` ``id``.

/user/group/<id>/
-----------------

**GET**
  Returns all objects by ``group`` ``id``.

