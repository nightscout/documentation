Deployment to Azure
===================

WORK IN PROGRESS



-  If deploying the software to Microsoft Azure, you must set \*\* in the app settings for *WEBSITE\_NODE\_DEFAULT\_VERSION* and    *SCM\_COMMAND\_IDLE\_TIMEOUT* **before** you deploy the latest Nightscout or the site deployment will likely fail. Other hosting environments do not require this setting. Please use:

   ::

       WEBSITE_NODE_DEFAULT_VERSION=8.11.1
       SCM_COMMAND_IDLE_TIMEOUT=300


	   

.. Hint:: If your site appears empty, as in there are no glucose or other data visible, then you will need to `configure an uploader <../Before%20you%20start/uploader-software.html>`_. If your site does not resemble this at all (white or black screen, dashes, error message), have a look at the `troubleshooting guide <Troubleshooting%20and%20questions/troubleshooting-guide.html>`_.

	.. image:: New_site_no_data.jpg
		:width: 400 px
		:alt: new site with no data
		:align: center


----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.