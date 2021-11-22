
User Interface
==============
Rockstor supports three main user interface methods.

1. A browser based interface (Web-UI) for most users
2. A RESTful API for developers.
3. root access via terminal and SSH for advanced users.

The :ref:`webui` is the main way to interact with Rockstor, and each one of its
parts will be described in the pages below:

.. toctree::
    :maxdepth: 2

    dashboard
    storage
    system
    overview


.. _webui:

Web-UI
------

To access Rockstor browser based interface or Web-UI, we recommend using
Firefox or Chrome web browser.

The initial setup of the appliance should be done through the Web-UI; other
methods can be used afterwards.

.. _setup:

Setup
^^^^^

Once Rockstor installation is finished, as described in the
:ref:`installation` section, the new appliance can be setup by visiting
:code:`https://<appliance_ip>` in your browser.

The setup process consists of two screens. In the first screen, an admin user
must be created by entering desired credentials. In the second screen, all
disks detected in the system are displayed. Click next to finish the setup
process.

Once the setup process is complete, the newly created admin user is logged in
and the Rockstor :ref:`dashboard` is displayed.
