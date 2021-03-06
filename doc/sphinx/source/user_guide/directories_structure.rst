.. user_guide directories_structure

=====================
Directories Structure
=====================

This chapter explains how files and directory are structured in Paparazzi.


Here is an extract of the Paparazzi tree:

.. code-block:: text

    ├── conf
    │   ├── airframes
    │   │   └── airframe.dtd
    │   ├── autopilot
    │   │   └── autopilot.dtd
    │   ├── conf.xml
    │   ├── control_panel.xml
    │   ├── flight_plans
    │   │   ├── basic.xml
    │   │   └── flight_plan.dtd
    │   ├── modules
    │   │   └── baro_bmp3.xml
    │   ├── radios
    │   │   └── FrSkyX9D.xml
    │   ├── settings
    │   │   ├── fixedwing_basic.xml
    │   │   └── settings.dtd
    │   ├── telemetry
    │   │   ├── default_fixedwing.xml
    │   │   ├── default_rotorcraft.xml
    │   │   └── telemetry.dtd
    │   ├── tools
    │   │   ├── blacklisted
    │   │   ├── gcs.xml
    │   │   └── messages.xml
    ├── doc
    │   └── sphinx
    │       └── source
    ├── Makefile
    ├── paparazzi
    ├── start.py
    ├── sw
    │   ├── ext
    │   ├── airborne
    │   │   ├── autopilot.c
    │   │   ├── autopilot.h
    │   │   └── modules
    │   │       ├── decawave
    │   │       ├── demo_module
    │   │       └── gps
    │   ├── ground_segment
    │   │   ├── tmtc
    │   │   └── cockpit
    │   └── simulator
    └── var
        ├── aircrafts
        │   └── Microjet
        ├── logs
        │   ├── 20_06_25__11_39_10.data
        │   ├── 20_06_25__11_39_10.log
        └── messages.xml

From a user perspective, the ``conf`` directory is the most important.

Aircraft
--------

The ``conf/airframes``, ``conf/flight_plans``, ``conf/radios`` and ``conf/telemetry`` sub-directories must contain the corresponding files. You can add as many subdirectories as you want, but don't forget to maintain the relative path to the associated *dtd* file.

In this example tree for the *airframe* directory (located itself in the ``conf`` directory):

.. code-block:: text

    airframe
    ├── airframe.dtd
    ├── examples
    │   └── microjet.xml
    └── nimp.xml


.. code-block:: xml
    :caption: This is the first line of ``nimp.xml``:

    <!DOCTYPE airframe SYSTEM "airframe.dtd">


.. code-block:: xml
    :caption: This is the first line of ``examples/microjet.xml``:

    <!DOCTYPE airframe SYSTEM "../airframe.dtd">

Aircrafts configurations (stored in ``conf`` files), and control panel files should be located in the ``userconf`` directory.

Tools
-----

The *Tools* in the Paparazzi Center come from the ``conf/tools`` directory. Each xml file produce a new entry in the *Tools* menu. You can add you own tools by creating a new xml file in this directory, and restarting the Paparazzi Center.

There are many tools that you will probably never use. You can remove these from the menu by adding their name to the ``blacklisted`` file.

Modules
-------

Modules configuration files are located in the ``conf/modules`` directory. The actual code of the modules is located in ``sw/airborne/modules``.


Software
--------

Paparazzi softwares are located in ``sw``. Airborne code, that will run on the drone itself, is located in ``sw/airborne``.

- ``sw/ext`` contains external software dependencies.
- ``sw/simulator`` contains the simulators
- ``sw/ground_segment/tmtc``, for "telemetry and telecommand" contains tools related to modems (link), and the server.
- ``sw/ground_segment/cockpit`` contains the GCS code

Doc
---

This documentation is stored in the ``doc/sphinx`` directory. Feel free to improve it!

Generated files
---------------

Compiled and generated files are located in the ``var`` directory.

``var/aircrafts`` contains the files generated by building your aircrafts.

``var/logs`` contains the logs written by the *Server* from real flights as well as for simulations if you remove the ``-n`` option on the server during a simulation.

``var/messages.xml`` list all PprzLink messages.

Launcher
--------

You can launch Paparazzi  with the eponym executable file ``paparazzi``, or via the configuration utility ``start.py``. In the later case, you can choose what conf file and what control panel file you want to use.



