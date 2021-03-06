# minimus-users

## Minimus Users

Implements simple "users" model for the Minimus framework.  Would also work with Bottle, etc. with minor reworking.  Requires use of an external database: either MongoDB or MontyDB.

### !Must REFACTOR db_client.py!

this will allow you to point at your database choice... either MontyDB or MongoDB

### exposes:

 **authenticate**(`username`, `password`) 
 
 - looks for an existing username
   and checks if the password matches the hashed version in the database
   if it does, it returns **True**, not, it returns **False**

**initialize**(`datadir`)

- initializes the JSON database in a directory IFF you are using MontyDB

**get_user**(`username`, `uid`)

- returns a user record from a username
 or id.  On failure returns None
 
**get_users**()

- returns a list of all users

**delete_user**(`username=None`, `uid=None`)

- username or uid is required.  Returns a user *if* it deleted a user
     identified by `username` or its `uid`
     
**create_user**(`username`, `password`, `**kwargs`) 

- *creates a user record*
username, password required -- the only validation is that username does not
currently exist.  `**kwargs` are optional keyword arguments to include in the
user record... for example is_active=True, display_name=John Doe

**update_user**(`username`, `**kwargs`)

- add additional keyword arguments
      to an existing record.  If a keyword argument value is EXPLICITLY set to None
       the existing key/value will be removed.
       

**render_login**(`login_filename=None`)

- returns a login page as a string contained
    login_file if `None` or left blank, then if loads module level file login.html
    login_filename : string of filename of login page HTML document or None.
    
    
*NOTE: this is an experimental feature*

**user_services_cli**(`args`)

- command line interface for user services such as:  --createuser, --deleteuser, --listuser, --updateuser.  You will usually pass `sys.argv` to the function, but it is just an array of arguments.


## Requires:

  "Minimus" - you know what this is if you've stumbled upon this
  
  https://github.com/jefmud/minimus
  
  "PyMongo" for remote/local mongo  https://pymongo.readthedocs.io/en/stable/
  
  "MontyDB" local filesystem database, command compatible with PyMongo
  https://github.com/davidlatwe/montydb

  "PassLib" - "Passlib is a password hashing library for Python 2 & 3, which provides cross-platform implementations of over 30 password hashing algorithms, as well as a framework   for managing existing password hashes. It???s designed to be useful for a wide range of tasks, from verifying a hash found in /etc/shadow, to providing full-strength password       hashing for multi-user application." (from passlib description)
  
  https://passlib.readthedocs.io/en/stable/
