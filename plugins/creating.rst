Creating a Plugin
===================

A plugin has two main components:

* An ``info.json`` file that tells the server about the plugin,
* A main class inside a main file.

To start, create an ``info.json`` file. It should look something like this:

.. code:: js

    {
        "name": "Plugin Name", // The name of your plugin.
        "api_version": "0.0.1", // The API version of your plugin.
        "main": "main.Main", // Your plugin's main class.
        "version": "0.0.1", // Your plugin's version.
        "description": "Plugin Description", // Your plugin's description.
        "author": "Plugin Author" // The plugin's author.
    }

Now, it's time to start coding.

Create a new Python file. For the purpose of this tutorial,
we're going to name it ``main.py``.

Inside that file, create a new class, let's call it ``Main``.

This class should have an ``__init__`` method that takes no arguments (other than ``self``),
and gives the class a ``server`` attribute.

When your plugin is loaded, the ``server`` attribute will be the server the plugin is loaded into.

Your plugin's ``Main`` class can have 2 methods that are used by the server,
``on_load`` and ``on_unload``.

Each method is called when the plugin is loaded/unloaded respectively.


