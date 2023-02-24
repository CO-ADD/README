Installation
========================================

Prerequisite
--------------

1. Prerequisite installation **COADD** is:

- Install conda in Linux by following the steps in [Installing on Linux] (https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html).
- Install rdkit pypi overall

2. Database environment

  1. create conda environment with:

     .. code-block:: python
      
        conda create --name <env_name>

  2. activate and install the following:

     * conda install -c anaconda postgresql
     * conda install -c rdkit rdkit-postgresql
     * pg_ctl initdb -D <path>/<your cluster name> eg. pg_ctl initdb -D ~/chem_data (meaning create cluster chem_data under user root)
     * pg_ctl -D <path>/<your cluster name> start
     * CREATE DATABASE databasename with:
   
       .. code-block::
      
        psql databasename
        create extension if not exists rdkit;
        create schema <name>

.. _setup:

Set up application environment
-------------------------------

Create another conda environment

Install all the following packages in the conda environment.

1. conda install -c conda-forge django
2. prerequistion for python-ldap
3. pip install python-ldap
4. pip install django-auth-ldap
5. pip install rdkit-pypi
6. pip install git+https://github.com/rdkit/django-rdkit.git
7. sudo apt-get install postgresql postgresql-contrib
   sudo apt-get install libpq-dev python3-dev
8. pip install psycopg2
9. for chemical drawing install the following:
   pip install ipython  
   pip install CairoSVG
10. django-sequences
11. pip install django-model-utils
12. pip install django-filter
13. pip install pdfplumber
    ...

