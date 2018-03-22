
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: User; API

.. _api_user:


The user API is used to manage users.

User CRUD: List
^^^^^^^^^^^^^^^

Lists the current users.

**Input:**

+--------+----------------------------+-----------+----------------------------------------+------------+
| Verb   | URL                        | Options   | Returns                                | Comments   |
+========+============================+===========+========================================+============+
| GET    | rebar/2.0/user/2.0/users   | N/A       | JSON array of user ID:Username pairs   |            |
+--------+----------------------------+-----------+----------------------------------------+------------+

**Output:**

::

    {
      "32": "test123",
      "1": "developer",
      "2": "rebar",
      "3": "machine-install",
      "4": "davpat2112"
    }

User CRUD: Show
^^^^^^^^^^^^^^^

Shows details about a selected user.

**Input:**

+--------+---------------------------------+----------------------------------+--------------------------------------+------------+
| Verb   | URL                             | Options                          | Returns                              | Comments   |
+========+=================================+==================================+======================================+============+
| GET    | rebar/2.0/user/2.0/users/[id]   | id is the user ID or username.   | Details of the user in JSON format   |            |
+--------+---------------------------------+----------------------------------+--------------------------------------+------------+

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@emai.com"
    }

User CRUD: Create
^^^^^^^^^^^^^^^^^

Creates a new user.

**Input:**

+--------+----------------------------+-----------+----------------------------------------------+-------------------------------+
| Verb   | URL                        | Options   | Returns                                      | Comments                      |
+========+============================+===========+==============================================+===============================+
| POST   | rebar/2.0/user/2.0/users   |           | User json definition (see User CRUD: Show)   | must be a valid user object   |
+--------+----------------------------+-----------+----------------------------------------------+-------------------------------+

::

    {
      "username":"testuser1",
      "email":"test1@domain.com",
      "password":"password123",
      "password_confirmation":"password123",
      "remember_me":"false",
      "is_admin":"false"
    }

Details:

-  username - The unique username (must be letters and numbers, and must
   start with a letter)
-  email - well formed unique and valid email address
-  password - password field (must meet password strength requirement)
-  password\_confirmation - password confirmation field
-  remember\_me - when user logs into UX will a cookie be set so
   username field is prepopulated.
-  is\_admin - will user have admin privileges, (create new update
   existing users in ux)

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    }

User CRUD: Update
^^^^^^^^^^^^^^^^^

Updates existing user.

**Input:**

+--------+---------------------------------+-----------+----------------------------------------------+------------+
| Verb   | URL                             | Options   | Returns                                      | Comments   |
+========+=================================+===========+==============================================+============+
| PUT    | rebar/2.0/user/2.0/users/[id]   |           | User json definition (see User CRUD: Show)   |            |
+--------+---------------------------------+-----------+----------------------------------------------+------------+

::

    {
      "id":"1",
      "username":"testuser1x",
      "email":"testuser1x@domain.com",
      "remember_me":"false",
      "is_admin":"false"
    }

Details:

-  id - the ID or username of the user to update
-  username - unique username (must be letters and numbers, and must
   start with a letter)
-  email - well formed unique and valid email address
-  remember\_me - when user logs into UX will a cookie be set so
   username field is prepopulated.
-  is\_admin - will user have admin privileges, (create new update
   existing users in ux)

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    }

Reset User Password
^^^^^^^^^^^^^^^^^^^

Change existing user password

**Input:**

+--------+-------------------------------------------------+-----------+----------------------------------------------+------------+
| Verb   | URL                                             | Options   | Returns                                      | Comments   |
+========+=================================================+===========+==============================================+============+
| PUT    | rebar/2.0/user/2.0/users/reset\_password/[id]   |           | User json definition (see User CRUD: Show)   |            |
+--------+-------------------------------------------------+-----------+----------------------------------------------+------------+

::

    {
      "id":"1",
      "password":"password123",
      "password_confirmation":"password123"
    }

Details:

-  id - the ID or username of the user to update
-  password - password field (must meet password strength requirement)
-  password\_confirmation - password confirmation field

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    } 

Lock User
^^^^^^^^^

Lock existing user account.

**Input:**

+--------+--------------------------------------+---------------------------------+----------------------------------------------+------------+
| Verb   | URL                                  | Options                         | Returns                                      | Comments   |
+========+======================================+=================================+==============================================+============+
| POST   | rebar/2.0/user/2.0/users/lock/[id]   | id is the user ID or username   | User json definition (see User CRUD: Show)   |            |
+--------+--------------------------------------+---------------------------------+----------------------------------------------+------------+

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    }

Unlock User
^^^^^^^^^^^

Unlock existing user account.

**Input:**

+----------+--------------------------------------+---------------------------------+----------------------------------------------+------------+
| Verb     | URL                                  | Options                         | Returns                                      | Comments   |
+==========+======================================+=================================+==============================================+============+
| DELETE   | rebar/2.0/user/2.0/users/lock/[id]   | id is the user ID or username   | User json definition (see User CRUD: Show)   |            |
+----------+--------------------------------------+---------------------------------+----------------------------------------------+------------+

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    }

Make User Admin
^^^^^^^^^^^^^^^

Add user administrator privilege to existing user.

**Input:**

+--------+---------------------------------------+---------------------------------+----------------------------------------------+------------+
| Verb   | URL                                   | Options                         | Returns                                      | Comments   |
+========+=======================================+=================================+==============================================+============+
| POST   | rebar/2.0/user/2.0/users/admin/[id]   | id is the user ID or username   | User json definition (see User CRUD: Show)   |            |
+--------+---------------------------------------+---------------------------------+----------------------------------------------+------------+

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    }    

Remove User Admin
^^^^^^^^^^^^^^^^^

Delete user administrator privilege from existing user.

**Input:**

+----------+---------------------------------------+---------------------------------+----------------------------------------------+------------+
| Verb     | URL                                   | Options                         | Returns                                      | Comments   |
+==========+=======================================+=================================+==============================================+============+
| DELETE   | rebar/2.0/user/2.0/users/admin/[id]   | id is the user ID or username   | User json definition (see User CRUD: Show)   |            |
+----------+---------------------------------------+---------------------------------+----------------------------------------------+------------+

**Output:**

::

    {
     "created_at": "2012-12-12T18:56:14Z",
     "updated_at": "2013-01-01T06:27:33Z",
     "username": "rebar",
     "id": 2,
     "is_admin": true,
     "email": "email@email.com"
    } 

User CRUD: Delete
^^^^^^^^^^^^^^^^^

Deletes a user.

**Input:**

+----------+---------------------------------+-----------------------+----------------------------------+------------+
| Verb     | URL                             | Options               | Returns                          | Comments   |
+==========+=================================+=======================+==================================+============+
| DELETE   | rebar/2.0/user/2.0/users/[id]   | User ID or username   | HTTP error code 200 on success   |            |
+----------+---------------------------------+-----------------------+----------------------------------+------------+

No body.

**Output:**

None.
