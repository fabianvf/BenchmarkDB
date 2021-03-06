# Contributing

Contributing a module to this application is very simple!  The format has already been established, so all you have to do is follow the given format and then you're good to go!  Up to this point, all modules have been for sharded databases, however you can write them for standalone instances as well.

After you build a module, test it rigorously and then please submit a pull request!  Take a close look at the documentation to make sure each function in your module does the exact prescribed functionality.  The basic structure can be seen in `benchmark_template.py`, however we'll briefly look at it here too:


1. Fork the project from `dev` and create the module directory
    * Create the directory inside the parent project directory: `.../DB-Benchmarking/<my_new_module>`
    * Name said directory logically: `<my_new_module>db`, or for examples: `mongodb` and `riakdb`.  The `db` at the end is **very important though!!!**

        ``` bash
        $ cd <path_to_project>/DB-Benchmarking
        $ mkdir <my_new_module>db
        ```

2. Move into the directory and create a few important things:

    ``` bash
    $ cd <my_new_module>db

    # Create the `__init__` file to make this directory a python package
    $ touch __init__.py

    # create the primary file that will house all of the read/write commands for your db
    $ touch main.py

    # Create the directory for all of your ansible/ vagrant files, so that someone else can easily bring your DB up and benchmark it themselves
    $ touch ansible/
    ```

3. Create your ansible roles and playbooks
    * Many of these are freely available on Github and what not, but you may need to create them yourself if it's a less-popular DB.
    * Be sure to include everything needed to deploy these vagrant boxes so that the only major thing a user needs to do it `vagrant up`
    * For an example, take a look at the `riakdb` module's ansible roles, as they are quite nice!  (They're from ansible_galaxy)

4. Create your primary DB file in `main.py`
    * Due to the nature of the application, you don't need to do any timing, recording, data_compliation, etc.  The wonderful thing is that all you need to do is create this module with a `main.py` that follows the given structure and the rest is done for you.  
    * Therefore, something to keep in mind is that the `main.py` you're creating will **only setup a DB connection, write to the DB, and then read from the DB**.  This makes things really simple to write, and enables us to create a relatively unbiased benchmarking report on various DB's since we're testing them all in the exact same way.
    * More detailed documentation on the specific functionality of each function lives in `benchmark_template.py`, but here is an outline:

        ```python
        from benchmark_template import BenchmarkDatabase

        class Benchmark(BenchmarkDatabase):

            def __init__(self, setup=False, verbose=False):

                if setup:
                    self.setup('test')

            def setup(self, collection):
                """ All setup actions are performed here and used in the `read` and
                `write` functions of this class.
                """

                # Do some setup stuff to get the DB client ready to use
                self.client = #something

            def write(self, data):
                """ The only thing this function should do is take the paramater `data`
                and write it to the DB
                """

                self.client.write(data)

            def read(self, index):
                """ The only thing this function does is to retrieve a single record
                from the DB given it's index (which is part of the original record).
                """

                self.client.read(index)
        ```

5. Document your module!
    * create a `README.md` with any special information for your module, and also be sure to include plenty of docstrings to let others know what you're doing

6. Submit a Pull Request with your finished module!  Before doing so, be sure to pull from `dev`, and that's where your PR will go as well.
