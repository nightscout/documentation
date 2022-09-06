Nightscout API
==============

The Nightscout API enables direct access to your DData without the need for direct Mongo access. You can find CGM data in ``/api/v1/entries``, Care Portal Treatments in ``/api/v1/treatments``, and Treatment Profiles in ``/api/v1/profile``. The server status and settings are available from ``/api/v1/status.json``.

By default the ``/entries`` and ``/treatments`` APIs limit results to the the most recent 10 values from the last 2 days. You can get many more results, by using the ``count``, ``date``, ``dateString``, and ``created_at`` parameters, depending on the type of data you're looking for.

Example Queries
---------------

(replace ``http://localhost:1337`` with your base url, YOUR-SITE)

-  100's: ``http://localhost:1337/api/v1/entries.json?find[sgv]=100``
-  Count of 100's in a month: ``http://localhost:1337/api/v1/count/entries/where?find[dateString][$gte]=2016-09&find[dateString][$lte]=2016-10&find[sgv]=100``
-  BGs between 2 days: ``http://localhost:1337/api/v1/entries/sgv.json?find[dateString][$gte]=2015-08-28&find[dateString][$lte]=2015-08-30`` 
-  Juice Box corrections in a year: ``http://localhost:1337/api/v1/treatments.json?count=1000&find[carbs]=15&find[eventType]=Carb+Correction&find[created_at][$gte]=2015``
-  Boluses over 2U: ``http://localhost:1337/api/v1/treatments.json?find[insulin][$gte]=2``

The API is Swagger enabled, so you can generate client code to make working with the API easy. To learn more about the Nightscout API, visit
https://YOUR-SITE.com/api-docs.html or review `swagger.yaml <https://github.com/nightscout/cgm-remote-monitor/blob/master/lib/api3/swagger.yaml>`__.

----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.
