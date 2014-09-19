# Database Benchmarking

This application is intended to help you benchmark a database of your choice very simply and easily.  Simply follow the specified steps to build a module of your own and then you can see how it stacks up to other similar databases!

The following modules are currently operational:
* Riak DB
* Riak 2.0 DB
* MongoDB


## Using the Application

1. Install dependencies from `requirements.txt`.  It's recommended to use a virtual environment.
    ``` bash
    $ cd <path_to_project>/DB-Benchmarking
    $ pip install -r requirements.txt
    ```

2. Deploy vagrant machine(s)
   This procedure is slightly different for every module, so be sure to read the `README` for each one.
3. Run the application!

    ```
    $ python main.py <database_module_name> [options]
    ```

    * General usage information and options:
    ```
    DB Benchmarking Application
    ===========================

    Main.py

    This file houses the core of the application, and is where all of the read/write
    commands are issued from, timed, and all data is analyzed.  Results from the
    trials are printed to the console by default, but can optionally be printed to a
    file to keep a record of.  This is particularly helpful when benchmarking
    multiple DB's in a row to see which one is best for deployment purposes.

        Usage:
            main.py <database> [options]

        Options:
            -h --help           Show this help screen
            -v --verbose        Show verbose output from the application

            -V --really_verbose
                                Show REALLY verbose output, including the individual
                                    time information from each run

            -l --list_mods      Outputs a list of available DB modules before running
            -r --report         Option to generate a report file, which will
                                    OVERWRITE any existing reports from the specified
                                    DB in the `generated_reports` directory

            --entry_length=<n>  Specify an entry length [default: 10]
            --trial_number=<n>  Specify the number of reads and writes to make to the
                                    DB to collect data on [default: 100]
    ```

## Building a module

If you want to benchmark a DB that isn't already included, build a new module!  Fork the project from dev before making your changes, and then follow the instructions in `CONTRIBUTING.md` to create a new module to use with this application!

Building a new module is extremely easy, so please do so and then submit a PR to share that module with everyone else!