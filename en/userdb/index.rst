
Dream UserDB
************

The user database (hereafter UserDB) is the central place for user
account information, and permission management.

.. toctree::

  api_v1
  sso


Dream UserDB provides 3rd party services means to
identify, authenticate and authorize users in the Dream platform.

Each service can register service specific permissions to the UserDB.
These permissions are then handled in the UserDB and the 3rd party
service gets access to the permission data.

All services can authenticate all users, and it is the responsibility
of the service to check if the user should have access to the service
or not and what actions the user can do inside the service.

The service can use only data provided back in authentication requests
as attributes. Or the service can request access to the UserDB API to
query data directly from the database.

Users provisioning should be automatic when the user logs in to the
service for the first time. It is each services responsibility to handle
this the way the service sees best.

Registering new services
========================

In order to access the UserDB your service needs to be registered to
the UserDB as a service.

The following information is needed:

* Name of the service
* Permissions your service is using to identify access levels

Contact Haltu for help in registration of your service.

