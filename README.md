Role Name
=========

This role can be used to download SQL dumps from S3, and to then decrypt, inflate and import them into a MySQL database.

Requirements
------------

The role assumes you have MySQL installed already.

Role Variables
--------------

The main variables required by this role are as follows:

* aws_access_key - Your AWS access key
* aws_secret_key - Your AWS secret key
* s3_backup_url - The path to your S3 backups bucket. It assumes the bucket contains one file per database, with the filename as the database name, compressed with GZ and encrypted with GPG. Each filename should be of the format databasename.sql.gz.gpg 
* gpg_secret_key: - The GPG secret key that the backups are encrypted for.

Dependencies
------------

Whilst not dependent on any specific role, as mentioned above the role does assume you have MySQL installed. I would recommend the geerlingguy.mysql ansible role. 

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
    - hosts: servers
      roles:
         - restore-sqldump-from-s3
```

License
-------

BSD

Author Information
------------------

Paul Maunders
