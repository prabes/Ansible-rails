Postgresql
==========

Install Postgresql and create a postgres user. 

Requirements
------------

* Requires superuser privileges for installation of Postgresql.
* Requires `python3-psycopg2 | libpq-dev | postgresql` packages before using the `postgresql_user` module

Role Variables
--------------

> Variables can be accessed from app-vars. Defaults are set in `/postgresql/defaults/main.yml` 


* `db_user` -> DB user for postgresql
* `db_user_password` -> Password for the DB user for postgresql


