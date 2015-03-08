Wooey
=====

Automated web UIs for Python scripts

## About

Wooey is a simple web interface (built on Flask) to run command line Python scripts. Think of it as an easy solution
to routine data analysis, file processing, or anything else. Get your scripts up on the web.

![Welcome](welcome_to_wooey.png)

![mock_argparse example script](mock_argparse_example.png)

![plot_some_numbers script with docs](plot_some_numbers_with_documentation.png)

![User job listing](user_job_list.png)

![Job with success 1](job_success_1.png)
![Job with success 2](job_success_2.png)

![Job with error console](job_with_error.png)



## Quickstart

First, set your app's secret key as an environment variable. For example, example add the following to ``.bashrc`` or ``.bash_profile``.


    export WOOEY_SECRET='something-really-secret'


Then run the following commands to bootstrap your environment.


    git clone https://github.com/mfitzp/wooey
    cd wooey
    pip install -r requirements/dev.txt
    python manage.py server

You will see a pretty welcome screen.

Once you have installed your DBMS, run the following to create your app's database tables and perform the initial migration:

    python manage.py db init
    python manage.py db migrate
    python manage.py db upgrade
    python manage.py server

The server will start up. But you will see it is empty! To add the example scripts to the database and allow you to test
also run:

    python manage.py build_scripts
    python manage.py find_scripts

This will build (create JSON for Python scripts using argparse) and then add them to the database.

In another shell, you can start the temporary dev 'daemon' (which is nothing of the sort, yet) using:

    python manage.py start_daemon


Deployment
----------

In your production environment, make sure the ``WOOEY_ENV`` environment variable is set to ``"prod"``.


Shell
-----

To open the interactive shell, run ::

    python manage.py shell

By default, you will have access to ``app``, ``db``, and the ``User`` model. This can be used to quickly recreate database tables
during development, i.e. delete `dev.db` (SQLite) and then from the shell enter:

    db.create_all()


Running Tests
-------------

To run all tests, run ::

    python manage.py test


Migrations
----------

Whenever a database migration needs to be made. Run the following commmands:
::

    python manage.py db migrate

This will generate a new migration script. Then run:
::

    python manage.py db upgrade

To apply the migration.

For a full migration command reference, run ``python manage.py db --help``.