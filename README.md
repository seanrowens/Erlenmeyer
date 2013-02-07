Erlenmeyer
===========

*It's Flask, SQLAlchemy, and Core Data. Get it? It's a chemistry pun. Get it?*

Erlenmeyer allows you to create fully-functional Flask servers, complete with SQLAlchemy models, from a Core Data file.

    $ erlenmeyer -p MegaBits -c MBModels.xcodedatamodeld

This command will generate a new Flask project, called MegaBits, with the following directory structure::

    MegaBits.py
    /handlers
        __init__.py
        ...
    /models
        __init__.py
        Model.py
        ...
    /settings
        settings.json

Where the ellipses (`...`) are lists of models built from your Core Data file.


`MegaBits.py`
---------

`MegaBits.py` is the primary Flask service. It creates the Flask app and SQLAlchemy instances, and forwards requests to the handler objects found in the `handlers` module.


`handlers`
---------

The `handlers` module contains a separate handler object for each model object built from your Core Data file. Every handler has 5+ methods, depending on the relational complexity of the underlying model.

Each handler method retrieves or applies the appropriate information to its underlying model, and returns a cooresponding `flask.Response` object, depending on success. In addition, all handler methods are also documented inline.


`models`
---------

The `models` module contains two distict types of objects.

* `Model.py`, which inherits directly from `flask.ext.sqlalchemy.Model`. It provides a shared underlying primary key to ever other model, as well as some convenience methods.

* The remaining models, which are created from your Core Data file, and inherit from either `Model.py` or their Core Data-stated parent class.


`settings.json`
---------

`settings.json` contains information for the runtime of the service. The "server" dictionary provides information for the Flask app, such as the IP address and port on which to broadcast. And the "sql" dictionary provides SQLAlchemy login and database information with which it should store the models.


Other bits...
---------

For feature requests and bug reports, please use [https://github.com/MegaBits/Erlenmeyer/issues](https://github.com/MegaBits/Erlenmeyer/issues).