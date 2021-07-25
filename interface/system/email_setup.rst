.. _email_notifications:

Email alerts
============

Rockstor integrates an easy to use email/postfix configuration section that
enables email notifications.  By default all local root (system) email will
be forwarded to a specified email address.  This is accomplished by using a
dedicated (configurable) email account that Rockstor can login too and send
email from.

.. _email_setup:

Initial Email Setup
-------------------

Navigate to the **Email Alerts** section of the **System** page:-

..  image:: /images/interface/system/email_setup/email_init.png
    :width: 100%
    :align: center

Press the **Add an Email account** button to begin.

Complete the following required fields

* **Name** - associated with this email ie firstname lastname
* **Email** - of the dedicated Rockstor sending account
* **Password** - for the above account
* **SMTP Server** - sending email server name for the above account
* **TLS** - use Transport Layer Security, most email servers support this
* **Recipient email** who is to receive the notification emails from Rockstor

..  image:: /images/interface/system/email_setup/email_config.png
    :width: 100%
    :align: center

**Submit** button when done

..  _email_current:

Current Email Configuration
---------------------------

Upon submitting the desired configuration the following is displayed
summarizing the previously entered and now current information and advising on
how this configuration might be :ref:`tested <email_test>`.

**Email Alerts** section of the **System** page with existing configuration.

..  image:: /images/interface/system/email_setup/email_done.png
    :width: 100%
    :align: center

Note **the Bin icon** to remove the configuration and start
over, and the **small arrow icon** to **test** the configuration.

.. _email_test:

Testing Email
-------------

A test email containing the appliance id, a UUID generated during install, can
be sent using the **small arrow icon** next to the **Bin icon** on the
:ref:`email_current` page. Upon a test email having been sent the following
screen should be visible:

..  image:: /images/interface/system/email_setup/email_test.png
    :width: 100%
    :align: center

**Please note that the appliance id sent in this email is used to identify
this particular install and it's update channel registration**
