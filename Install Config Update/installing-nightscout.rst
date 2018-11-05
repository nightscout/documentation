Installing Nightscout
=====================

WORK IN PROGRESS

.. image:: https://www.herokucdn.com/deploy/button.png
   :target: https://dashboard.heroku.com/new?button-url=https%3A%2F%2Fgithub.com%2Fnightscout%2Fcgm-remote-monitor&template=https%3A%2F%2Fgithub.com%2Fnightscout%2Fcgm-remote-monitor

If you plan to use Nightscout, we recommend using `Heroku <http://openaps.readthedocs.io/en/latest/docs/While%20You%20Wait%20For%20Gear/nightscout-setup.html#nightscout-setup-with-heroku>`__, as Nightscout can reach the usage limits of the free Azure plan and cause it to shut down for hours or days. If you end up needing a paid tier, the $7/mo Heroku plan is also much cheaper than the first paid tier of Azure. Currently, the only added benefit to choosing the $7/mo Heroku plan vs the free Heroku plan is a section showing site use metrics for performance (such as response time). This has limited benefit to the average Nightscout user. In short, Heroku is the free and best option for Nightscout hosting.

- `Nightscout Setup with Heroku <http://openaps.readthedocs.io/en/latest/docs/While%20You%20Wait%20For%20Gear/nightscout-setup.html#nightscout-setup-with-heroku>`__ (recommended)

- `Nightscout Setup with Microsoft Azure <http://www.nightscout.info/wiki/faqs-2/azure-2>`__ (not recommended)

Please `switch from Azure to Heroku <http://openaps.readthedocs.io/en/latest/docs/While%20You%20Wait%20For%20Gear/nightscout-setup.html#switching-from-azure-to-heroku>`__.

----

.. Hint:: If following your installation your site appears empty, as in there are no glucose or other data visible, then you will need to `configure an uploader <../Before%20you%20start/uploader-software.html>`_. If your site does not resemble this at all (white or black screen, dashes, error message), have a look at the `troubleshooting guide <../Troubleshooting%20and%20questions/troubleshooting-guide.html>`_.

	.. image:: New_site_no_data.jpg
		:width: 400 px
		:alt: new site with no data
		:align: center

----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.