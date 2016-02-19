restore-sqldump-from-s3
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
* s3_backup_url or s3_backup_url_parent - The path to your S3 backups bucket. You should only set one of these. If you set the s3_backup_parent_url it will expect this to contain a collection of sub folders, e.g. daily backups, and will choose the latest (last in the list). If you set s3_backup_url this should be a specific backup folder. It assumes the backup folder contains one file per database, with the filename as the database name, compressed with GZ and encrypted with GPG. Each filename should be of the format databasename.sql.gz.gpg 
* s3_databases - An optional list of databases you wish to restore, specified without the sql.gz.gpg suffix. If this is not set the role will attempt to download every database in the S3 folder.
* gpg_secret_key  - The GPG secret key that the backups are encrypted for.
* innodb_row_format - If this variable is set to a ROW_FORMAT value, we will attempt to add the ROW_FORMAT to any CREATE TABLE statement which doens't already have one present. So if you wish to enable compression across all tables, you could set this to innodb_row_format=compressed - please note, this will require you to have innodb_file_format=Barracuda in your my.cnf

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
