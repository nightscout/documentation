Uploader software
=================

Below are different applications which can upload CGM and other data to Nightscout. Visit their respective pages to learn more about how to install and configure them.

What you'll need
----------------

In order to configure uploader software you will need your Nightscout URL and API_SECRET. 

There is an `autoconfigure tool <https://nightscout.github.io/pages/configure/>`_ which will be helpful in configuring your software if your device supports reading of QR codes.

.. image:: ../Images/configureuploader.jpg
	:width: 400 px
	:alt: autoconfigure tool
	:align: center

Open source uploaders
---------------------

The following open source uploaders connect to a wide range of CGM hardware, and have additional features as well, i.e. to track and upload treatments.

- `Xdrip+ (Android) <https://jamorham.github.io/#xdrip-plus>`_
- `Spike (iOS) <https://spike-app.com/>`_
- `Medtronic 600 series Android uploader <https://github.com/pazaan/600SeriesAndroidUploader/>`_ (see complete setup cookbook `here <https://docs.google.com/document/d/1sfpi5iUZ8aozl-udEkuKc6dTypFVr444tB7tUs4o4jE/edit>`_

Open source artificial pancreas systems
---------------------------------------

The artificial pancreas systems below are able to upload a wide range of data including CGM, pump, and treatment information.

- `AndroidAPS (Android) <https://androidaps.readthedocs.io/en/latest/EN/>`_
- `Loop (iOS) <https://loopkit.github.io/loopdocs/>`_
- `OpenAPS (Linux) <https://openaps.readthedocs.io/en/latest/>`_

Commercial systems supported by open source software
----------------------------------------------------

- `Dexcom Share <https://github.com/nightscout/share2nightscout-bridge>`_

----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.