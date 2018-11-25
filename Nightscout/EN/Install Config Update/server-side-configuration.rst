Server-side configuration
=========================

WORK IN PROGRESS

   - `Where to go to set these variables <#where-to-go-to-set-these-variables>`__
   - `Required <#required>`__
   - `Features/Labs <#featureslabs>`__
   - `Alarms <#alarms>`__
   - `Core <#core>`__
   - `Predefined values for your browser settings (optional) <#predefined-values-for-your-browser-settings-optional>`__
   - `Views <#views>`__
   - `Plugins <#plugins>`__
   - `Default Plugins <#default-plugins>`__

      - ``delta`` `(BG Delta) <#delta-bg-delta>`__
      - ``direction`` `(BG Direction) <#direction-bg-direction>`__
      - ``upbat`` `(Uploader Battery) <#upbat-uploader-battery>`__
      - ``timeago`` `(Time Ago) <#timeago-time-ago>`__
      - ``devicestatus`` `(Device Status) <#devicestatus-device-status>`__
      - ``errorcodes`` `(CGM Error Codes) <#errorcodes-cgm-error-codes>`__
      - ``ar2`` `(AR2 Forecasting) <#ar2-ar2-forecasting>`__
      - ``simplealarms`` `(Simple BG Alarms) <#simplealarms-simple-bg-alarms>`__
      - ``profile`` `(Treatment Profile) <#profile-treatment-profile>`__

   - `Advanced Plugins <#advanced-plugins>`__

      - ``careportal`` `(Careportal) <#careportal-careportal>`__
      - ``boluscalc`` `(Bolus Wizard) <#boluscalc-bolus-wizard>`__
      - ``food`` `(Custom Foods) <#food-custom-foods>`__
      - ``rawbg`` `(Raw BG) <#rawbg-raw-bg>`__
      - ``iob`` `(Insulin-on-Board) <#iob-insulin-on-board>`__
      - ``cob`` `(Carbs-on-Board) <#cob-carbs-on-board>`__
      - ``bwp`` `(Bolus Wizard Preview) <#bwp-bolus-wizard-preview>`__
      - ``cage`` `(Cannula Age) <#cage-cannula-age>`__
      - ``sage`` `(Sensor Age) <#sage-sensor-age>`__
      - ``iage`` `(Insulin Age) <#iage-insulin-age>`__
      - ``treatmentnotify`` `(Treatment Notifications) <#treatmentnotify-treatment-notifications>`__
      - ``basal`` `(Basal Profile) <#basal-basal-profile>`__
      - ``bridge`` `(Share2Nightscout bridge) <#bridge-share2nightscout-bridge>`__
      - ``mmconnect`` `(MiniMed Connect bridge) <#mmconnect-minimed-connect-bridge>`__
      - ``pump`` `(Pump Monitoring) <#pump-pump-monitoring>`__
      - ``openaps`` `(OpenAPS) <#openaps-openaps>`__
      - ``loop`` `(Loop) <#loop-loop>`__
      - ``xdrip-js`` `(xDrip-js) <#xdrip-js-xdrip-js>`__
      - ``alexa`` `(Amazon Alexa) <#alexa-amazon-alexa>`__
      - ``cors`` `(CORS) <#cors-cors>`__

   - `Extended Settings <#extended-settings>`__
   - `Treatment Profile <#treatment-profile>`__

	  
Where to go to set these variables
----------------------------------




	  
Environment
-----------

``VARIABLE`` (default) - description

Required
~~~~~~~~

- ``MONGO_CONNECTION`` - Your mongo uri, for example: ``mongodb://sally:sallypass@ds099999.mongolab.com:99999/nightscout``. (The data being uploaded from the server to the client is from a MongoDB server such as `mongolab <https://mongolab.com>`__. Try the `what is my mongo string tool <https://nightscout.github.io/pages/mongostring/>`__ to get a good idea of your mongo string. You can copy and paste the text in the gray
box into your ``MONGO_CONNECTION`` environment variable.)
- ``DISPLAY_UNITS`` (``mg/dl``) - Choices: ``mg/dl`` and ``mmol``. Setting to ``mmol`` puts the entire server into ``mmol`` mode by default, no further settings needed.
- ``BASE_URL`` - Used for building links to your sites api, ie pushover callbacks, usually the URL of your Nightscout site you may want https instead of http.

Features/Labs
~~~~~~~~~~~~~

- ``ENABLE`` - Used to enable optional features, expects a space delimited list, such as: ``careportal rawbg iob``, see `plugins <#plugins>`__ below
- ``DISABLE`` - Used to disable default features, expects a space delimited list, such as: ``direction upbat``, see `plugins <#plugins>`__ below
- ``API_SECRET`` - A secret passphrase that must be at least 12 characters long, required to enable ``POST`` and ``PUT``; also required for the Care Portal
- ``AUTH_DEFAULT_ROLES`` (``readable``) - possible values ``readable``, ``denied``, or any valid role name. When ``readable``, anyone can view Nightscout without a token. Setting it to ``denied`` will require a token from every visit, using ``status-only`` will enable api-secret based login.
- ``IMPORT_CONFIG`` - Used to import settings and extended settings from a url such as a gist. Structure of file should be something like:    ``{"settings": {"theme": "colors"}, "extendedSettings": {"upbat": {"enableAlerts": true}}}``
- ``TREATMENTS_AUTH`` (``on``) - possible values ``on`` or ``off``. Deprecated, if set to ``off`` the ``careportal`` role will be added to ``AUTH_DEFAULT_ROLES``

Alarms
~~~~~~

These alarm setting effect all delivery methods (browser, pushover,
maker, etc), some settings can be overridden per client (web browser)

- ``ALARM_TYPES`` (``simple`` if any ``BG_``\* ENV's are set, otherwise ``predict``) - currently 2 alarm types are supported, and can be used independently or combined. The ``simple`` alarm type only compares the current BG to ``BG_``\* thresholds above, the ``predict``    alarm type uses highly tuned formula that forecasts where the BG is going based on it's trend. ``predict`` **DOES NOT** currently use any of the ``BG_``\* ENV's
- ``BG_HIGH`` (``260``) - must be set using mg/dl units; the high BG outside the target range that is considered urgent
- ``BG_TARGET_TOP`` (``180``) - must be set using mg/dl units; the top of the target range, also used to draw the line on the chart
- ``BG_TARGET_BOTTOM`` (``80``) - must be set using mg/dl units; the bottom of the target range, also used to draw the line on the chart
- ``BG_LOW`` (``55``) - must be set using mg/dl units; the low BG outside the target range that is considered urgent
- ``ALARM_URGENT_HIGH`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_URGENT_HIGH_MINS`` (``30 60 90 120``) - Number of minutes to snooze urgent high alarms, space separated for options in browser, first used for pushover
- ``ALARM_HIGH`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_HIGH_MINS`` (``30 60 90 120``) - Number of minutes to snooze high alarms, space separated for options in browser, first used for    pushover
- ``ALARM_LOW`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_LOW_MINS`` (``15 30 45 60``) - Number of minutes to snooze low alarms, space separated for options in browser, first used for pushover
- ``ALARM_URGENT_LOW`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_URGENT_LOW_MINS`` (``15 30 45``) - Number of minutes to snooze urgent low alarms, space separated for options in browser, first used for pushover
- ``ALARM_URGENT_MINS`` (``30 60 90 120``) - Number of minutes to snooze urgent alarms (that aren't tagged as high or low), space separated for options in browser, first used for pushover
- ``ALARM_WARN_MINS`` (``30 60 90 120``) - Number of minutes to snooze warning alarms (that aren't tagged as high or low), space separated for options in browser, first used for pushover

Core
~~~~

- ``MONGO_COLLECTION`` (``entries``) - The collection used to store SGV, MBG, and CAL records from your CGM device
- ``MONGO_TREATMENTS_COLLECTION`` (``treatments``) -The collection used to store treatments entered in the Care Portal, see the ``ENABLE`` env var above
- ``MONGO_DEVICESTATUS_COLLECTION``\ (``devicestatus``) - The collection used to store device status information such as uploader battery
- ``MONGO_PROFILE_COLLECTION``\ (``profile``) - The collection used to store your profiles
- ``MONGO_FOOD_COLLECTION``\ (``food``) - The collection used to store your food database
- ``MONGO_ACTIVITY_COLLECTION``\ (``activity``) - The collection used to store activity data
- ``PORT`` (``1337``) - The port that the node.js application will listen on.
- ``HOSTNAME`` - The hostname that the node.js application will listen on, null by default for any hostname for IPv6 you may need to use ``::``.
- ``SSL_KEY`` - Path to your ssl key file, so that ssl(https) can be enabled directly in node.js
- ``SSL_CERT`` - Path to your ssl cert file, so that ssl(https) can be enabled directly in node.js
- ``SSL_CA`` - Path to your ssl ca file, so that ssl(https) can be enabled directly in node.js
- ``HEARTBEAT`` (``60``) - Number of seconds to wait in between database checks
- ``DEBUG_MINIFY`` (``true``) - Debug option, setting to ``false`` will disable bundle minification to help tracking down error and speed up    development

Predefined values for your browser settings (optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- ``TIME_FORMAT`` (``12``)- possible values ``12`` or ``24``
- ``NIGHT_MODE`` (``off``) - possible values ``on`` or ``off``
- ``SHOW_RAWBG`` (``never``) - possible values ``always``, ``never`` or ``noise``
- ``CUSTOM_TITLE`` (``Nightscout``) - Usually name of T1
- ``THEME`` (``default``) - possible values ``default``, ``colors``, or ``colorblindfriendly``
- ``ALARM_TIMEAGO_WARN`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_TIMEAGO_WARN_MINS`` (``15``) - minutes since the last reading to trigger a warning
- ``ALARM_TIMEAGO_URGENT`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_TIMEAGO_URGENT_MINS`` (``30``) - minutes since the last reading to trigger a urgent alarm
- ``SHOW_PLUGINS`` - enabled plugins that should have their visualizations shown, defaults to all enabled
- ``SHOW_FORECAST`` (``ar2``) - plugin forecasts that should be shown by default, supports space delimited values such as ``"ar2 openaps"``
- ``LANGUAGE`` (``en``) - language of Nightscout. If not available english is used

   -  Currently supported language codes are: bg (Български), cs
      (Čeština), de (Deutsch), dk (Dansk), el (Ελληνικά), en (English),
      es (Español), fi (Suomi), fr (Français), he (עברית), hr
      (Hrvatski), it (Italiano), ko (한국어), nb (Norsk (Bokmål)), nl
      (Nederlands), pl (Polski), pt (Português (Brasil)), ro (Română),
      ru (Русский), sk (Slovenčina), sv (Svenska), zh\_cn (中文（简体)),
      zh\_tw (中文（繁體))

- ``SCALE_Y`` (``log``) - The type of scaling used for the Y axis of the charts system wide.

   -  The default ``log`` (logarithmic) option will let you see more detail towards the lower range, while still showing the full CGM range.
   -  The ``linear`` option has equidistant tick marks, the range used is dynamic so that space at the top of chart isn't wasted.
   -  The ``log-dynamic`` is similar to the default ``log`` options, but uses the same dynamic range and the ``linear`` scale.

- ``EDIT_MODE`` (``on``) - possible values ``on`` or ``off``. Enable or disable icon allowing enter treatments edit mode.

Views
~~~~~

There are a few alternate web views available that display a simplified BG stream. Append any of these to your Nightscout URL: 

- ``/clock.html`` - Shows current BG. Grey text on a black background.
- ``/bgclock.html`` - Shows current BG, trend arrow, and time of day. Grey text on a black background. 
- ``/clock-color.html`` - Shows current BG and trend arrow. White text on a background that changes color to indicate current BG threshold (green = in range; blue = below range; yellow = above range; red = urgent below/above).

Plugins
-------

Plugins are used extend the way information is displayed, how notifications are sent, alarms are triggered, and more.

The built-in/example plugins that are available by default are listed below. The plugins may still need to be enabled by adding to the ``ENABLE`` environment variable.

Default Plugins
~~~~~~~~~~~~~~~

These can be disabled by setting the ``DISABLE`` env var, for example ``DISABLE="direction upbat"``

``delta`` (BG Delta)
^^^^^^^^^^^^^^^^^^^^

Calculates and displays the change between the last 2 BG values.

``direction`` (BG Direction)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Displays the trend direction.

``upbat`` (Uploader Battery)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Displays the most recent battery status from the uploader phone. . Use these `extended setting <#extended-settings>`__ to adjust behavior: 

- ``UPBAT_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable uploader battery alarms via Pushover and IFTTT. 
- ``UPBAT_WARN`` (``30``) - Minimum battery percent to trigger warning. 
- ``UPBAT_URGENT`` (``20``) - Minimum battery percent to trigger urgent alarm.

``timeago`` (Time Ago)
^^^^^^^^^^^^^^^^^^^^^^

Displays the time since last CGM entry. Use these `extended setting <#extended-settings>`__ to adjust behavior: 

- ``TIMEAGO_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable stale data alarms via Pushover and IFTTT. 
- ``ALARM_TIMEAGO_WARN`` (``on``) - possible values ``on`` or ``off``
- ``ALARM_TIMEAGO_WARN_MINS`` (``15``) - minutes since the last reading to trigger a warning
- ``ALARM_TIMEAGO_URGENT`` (``on``) - possible values ``on`` or ``off`` 
- ``ALARM_TIMEAGO_URGENT_MINS`` (``30``) - minutes since the last reading to trigger a urgent alarm

``devicestatus`` (Device Status)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Used by ``upbat`` and other plugins to display device status info. Supports the ``DEVICESTATUS_ADVANCED="true"`` `extended setting <#extended-settings>`__ to send all device statuses to the client for retrospective use and to support other plugins.

``errorcodes`` (CGM Error Codes)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Generates alarms for CGM codes ``9`` (hourglass) and ``10`` (???). 

- Use `extended settings <#extended-settings>`__ to adjust what errorcodes trigger notifications and alarms: 
- ``ERRORCODES_INFO`` (``1 2 3 4 5 6 7 8``) - By default the needs calibration (blood drop) and other codes below 9 generate an info level notification, set to a space separate list of number or ``off`` to disable 
- ``ERRORCODES_WARN`` (``off``) - By default there are no warning configured, set to a space separate list of numbers or ``off`` to disable
- ``ERRORCODES_URGENT`` (``9 10``) - By default the hourglass and ??? generate an urgent alarm, set to a space separate list of numbers or ``off`` to disable

``ar2`` (AR2 Forecasting)
^^^^^^^^^^^^^^^^^^^^^^^^^

Generates alarms based on forecasted values. See `Forecasting using AR2 algorithm <https://github.com/nightscout/nightscout.github.io/wiki/Forecasting>`__

- Enabled by default if no thresholds are set **OR** ``ALARM_TYPES`` includes ``predict``. 
- Use `extended settings <#extended-settings>`__ to adjust AR2 behavior: 
- ``AR2_CONE_FACTOR`` (``2``) - to adjust size of cone, use ``0`` for a single line.

``simplealarms`` (Simple BG Alarms)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Uses ``BG_HIGH``, ``BG_TARGET_TOP``, ``BG_TARGET_BOTTOM``, ``BG_LOW`` thresholds to generate alarms. Enabled by default if 1 of these thresholds is set **OR** ``ALARM_TYPES`` includes ``simple``.

``profile`` (Treatment Profile)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add link to Profile Editor and allow to enter treatment profile settings. Also uses the extended setting: 

- ``PROFILE_HISTORY`` (``off``) - possible values ``on`` or ``off``. Enable/disable NS ability to keep history of your profiles (still experimental)
- ``PROFILE_MULTIPLE`` (``off``) - possible values ``on`` or ``off``. Enable/disable NS ability to handle and switch between multiple treatment profiles

Advanced Plugins
~~~~~~~~~~~~~~~~

``careportal`` (Careportal)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

An optional form to enter treatments.

``boluscalc`` (Bolus Wizard)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``food`` (Custom Foods)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An option plugin to enable adding foods from database in Bolus Wizard.

``rawbg`` (Raw BG)
^^^^^^^^^^^^^^^^^^

Calculates BG using sensor and calibration records from and displays an alternate BG values and noise levels.

``iob`` (Insulin-on-Board)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Adds the IOB pill visualization in the client and calculates values that used by other plugins. Uses treatments with insulin doses and the ``dia`` and ``sens`` fields from the `treatment profile <#treatment-profile>`__.

``cob`` (Carbs-on-Board)
^^^^^^^^^^^^^^^^^^^^^^^^

Adds the COB pill visualization in the client and calculates values that used by other plugins. Uses treatments with carb doses and the ``carbs_hr``, ``carbratio``, and ``sens`` fields from the `treatment profile <#treatment-profile>`__.

``bwp`` (Bolus Wizard Preview)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This plugin in intended for the purpose of automatically snoozing alarms when the CGM indicates high blood sugar but there is also insulin on board (IOB) and secondly, alerting to user that it might be beneficial to measure the blood sugar using a glucometer and dosing insulin as calculated by the pump or instructed by trained medicare professionals. **The values provided by the plugin are provided as a reference based on CGM data and insulin sensitivity you have configured, and are not intended to be used as a reference for bolus calculation.** The plugin calculates the bolus amount when above your target, generates alarms when you should consider checking and bolusing, and snoozes alarms when there is enough IOB to cover a high BG. Uses the results of the ``iob`` plugin and ``sens``, ``target_high``, and ``target_low`` fields from the `treatment profile <#treatment-profile>`__. Defaults that can be adjusted with `extended setting <#extended-settings>`__.

- ``BWP_WARN`` (``0.50``) - If ``BWP`` is > ``BWP_WARN`` a warning alarm will be triggered. 
- ``BWP_URGENT`` (``1.00``) - If ``BWP`` is > ``BWP_URGENT`` an urgent alarm will be triggered. 
- ``BWP_SNOOZE_MINS`` (``10``) - minutes to snooze when there is enough IOB to cover a high BG. 
- ``BWP_SNOOZE`` - (``0.10``) If BG is higher then the ``target_high`` and ``BWP`` < ``BWP_SNOOZE`` alarms will be snoozed for ``BWP_SNOOZE_MINS``.

``cage`` (Cannula Age)
^^^^^^^^^^^^^^^^^^^^^^

Calculates the number of hours since the last ``Site Change`` treatment that was recorded. \* ``CAGE_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications to remind you of upcoming cannula change. 

- ``CAGE_INFO`` (``44``) - If time since last ``Site Change`` matches ``CAGE_INFO``, user will be warned of upcoming cannula change
- ``CAGE_WARN`` (``48``) - If time since last ``Site Change`` matches ``CAGE_WARN``, user will be alarmed to to change the cannula 
- ``CAGE_URGENT`` (``72``) - If time since last ``Site Change`` matches ``CAGE_URGENT``, user will be issued a persistent warning of overdue
change.
- ``CAGE_DISPLAY`` (``hours``) - Possible values are 'hours' or 'days'. If 'days' is selected and age of canula is greater than 24h
number is displayed in days and hours

``sage`` (Sensor Age)
^^^^^^^^^^^^^^^^^^^^^

Calculates the number of days and hours since the last ``Sensor Start`` and ``Sensor Change`` treatment that was recorded. 

- ``SAGE_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications to remind you of upcoming sensor change. 
- ``SAGE_INFO`` (``144``) - If time since last sensor event matches ``SAGE_INFO``, user will be warned of upcoming sensor change 
- ``SAGE_WARN`` (``164``) - If time since last sensor event matches ``SAGE_WARN``, user will be alarmed to to change/restart the sensor
- ``SAGE_URGENT`` (``166``) - If time since last sensor event matches ``SAGE_URGENT``, user will be issued a persistent warning of overdue change.

``iage`` (Insulin Age)
^^^^^^^^^^^^^^^^^^^^^^

Calculates the number of days and hours since the last ``Insulin Change`` treatment that was recorded.

- ``IAGE_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications to remind you of upcoming insulin reservoir change. 
- ``IAGE_INFO`` (``44``) - If time since last ``Insulin Change`` matches ``IAGE_INFO``, user will be warned of upcoming insulin reservoir change
- ``IAGE_WARN`` (``48``) - If time since last ``Insulin Change`` matches ``IAGE_WARN``, user will be alarmed to to change the insulin reservoir
- ``IAGE_URGENT`` (``72``) - If time since last ``Insulin Change`` matches ``IAGE_URGENT``, user will be issued a persistent warning of overdue change.

``treatmentnotify`` (Treatment Notifications)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Generates notifications when a treatment has been entered and snoozes alarms minutes after a treatment. Default snooze is 10 minutes, and can be set using the ``TREATMENTNOTIFY_SNOOZE_MINS`` `extended setting <#extended-settings>`__.

``basal`` (Basal Profile)
^^^^^^^^^^^^^^^^^^^^^^^^^

Adds the Basal pill visualization to display the basal rate for the current time. Also enables the ``bwp`` plugin to calculate correction temp basal suggestions. Uses the ``basal`` field from the `treatment profile <#treatment-profile>`__. Also uses the extended setting:

- ``BASAL_RENDER`` (``none``) - Possible values are ``none``, ``default``, or ``icicle`` (inverted)

``bridge`` (Share2Nightscout bridge)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Glucose reading directly from the Share service, uses these extended settings: 

- ``BRIDGE_USER_NAME`` - Your user name for the Share service. 
- ``BRIDGE_PASSWORD`` - Your password for the Share service.
- ``BRIDGE_INTERVAL`` (``150000`` *2.5 minutes*) - The time to wait between each update. 
- ``BRIDGE_MAX_COUNT`` (``1``) - The maximum number of records to fetch per update.
- ``BRIDGE_FIRST_FETCH_COUNT`` (``3``) - Changes max count during the very first update only.
- ``BRIDGE_MAX_FAILURES`` (``3``) - How many failures before giving up.
- ``BRIDGE_MINUTES`` (``1400``) - The time window to search for new data per update (default is one day in minutes).

``mmconnect`` (MiniMed Connect bridge)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Transfer real-time MiniMed Connect data from the Medtronic CareLink server into Nightscout (`read more <https://github.com/mddub/minimed-connect-to-nightscout>`__).

- ``MMCONNECT_USER_NAME`` - Your user name for CareLink Connect.
- ``MMCONNECT_PASSWORD`` - Your password for CareLink Connect.
- ``MMCONNECT_INTERVAL`` (``60000`` *1 minute*) - Number of milliseconds to wait between requests to the CareLink server.
- ``MMCONNECT_MAX_RETRY_DURATION`` (``32``) - Maximum number of total seconds to spend retrying failed requests before giving up.
- ``MMCONNECT_SGV_LIMIT`` (``24``) - Maximum number of recent sensor glucose values to send to Nightscout on each request.
- ``MMCONNECT_VERBOSE`` - Set this to "true" to log CareLink request information to the console.
- ``MMCONNECT_STORE_RAW_DATA`` - Set this to "true" to store raw data returned from CareLink as ``type: "carelink_raw"`` database entries (useful for development).

``pump`` (Pump Monitoring)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Generic Pump Monitoring for OpenAPS, MiniMed Connect, RileyLink, t:slim, with more on the way. 

- Requires ``DEVICESTATUS_ADVANCED="true"`` to be set 
- ``PUMP_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications for Pump battery and reservoir.
- ``PUMP_WARN_ON_SUSPEND`` (``false``) - Set to ``true`` to get an alarm when the pump is suspended.
- ``PUMP_FIELDS`` (``reservoir battery``) - The fields to display by default. Any of the following fields: ``reservoir``, ``battery``, ``clock``, ``status``, and ``device`` 
- ``PUMP_RETRO_FIELDS`` (``reservoir battery clock``) - The fields to display in retro mode. Any of the above fields. 
- ``PUMP_WARN_CLOCK`` (``30``) - The number of minutes ago that needs to be exceed before an alert is triggered. 
- ``PUMP_URGENT_CLOCK`` (``60``) - The number of minutes ago that needs to be exceed before an urgent alarm is triggered.
- ``PUMP_WARN_RES`` (``10``) - The number of units remaining, a warning will be triggered when dropping below this threshold.
- ``PUMP_URGENT_RES`` (``5``) - The number of units remaining, an urgent alarm will be triggered when dropping below this threshold.
- ``PUMP_WARN_BATT_P`` (``30``) - The % of the pump battery remaining, a warning will be triggered when dropping below this threshold. 
- ``PUMP_URGENT_BATT_P`` (``20``) - The % of the pump battery remaining, an urgent alarm will be triggered when dropping below this threshold.
- ``PUMP_WARN_BATT_V`` (``1.35``) - The voltage (if percent isn't available) of the pump battery, a warning will be triggered when dropping below this threshold. 
- ``PUMP_URGENT_BATT_V`` (``1.30``) - The voltage (if percent isn't available) of the pump battery, an urgent alarm will be triggered when dropping below this threshold.

``openaps`` (OpenAPS)
^^^^^^^^^^^^^^^^^^^^^

Integrated OpenAPS loop monitoring, uses these extended settings: 

- Requires ``DEVICESTATUS_ADVANCED="true"`` to be set
- ``OPENAPS_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications when OpenAPS isn't looping. If OpenAPS is going to offline for a period of time, you can add an ``OpenAPS Offline`` event for the expected duration from Careportal to avoid getting alerts.
- ``OPENAPS_WARN`` (``30``) - The number of minutes since the last loop that needs to be exceed before an alert is triggered
- ``OPENAPS_URGENT`` (``60``) - The number of minutes since the last loop that needs to be exceed before an urgent alarm is triggered
- ``OPENAPS_FIELDS`` (``status-symbol status-label iob meal-assist rssi``) - The fields to display by default. Any of the following fields: ``status-symbol``, ``status-label``, ``iob``, ``meal-assist``, ``freq``, and ``rssi`` 
- ``OPENAPS_RETRO_FIELDS`` (``status-symbol status-label iob meal-assist rssi``) - The fields to display in retro mode. Any of the above fields.

Also see `Pushover <#pushover>`__ and `IFTTT Maker <#ifttt-maker>`__.

``loop`` (Loop)
^^^^^^^^^^^^^^^

iOS Loop app monitoring, uses these extended settings: 

- Requires ``DEVICESTATUS_ADVANCED="true"`` to be set \* ``LOOP_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications when Loop isn't looping. 
- ``LOOP_WARN`` (``30``) - The number of minutes since the last loop that needs to be exceeded before an alert is triggered
- ``LOOP_URGENT`` (``60``) - The number of minutes since the last loop that needs to be exceeded before an urgent alarm is triggered
- Add ``loop`` to ``SHOW_FORECAST`` to show forecasted BG.

``xdrip-js`` (xDrip-js)
^^^^^^^^^^^^^^^^^^^^^^^

Integrated xDrip-js monitoring, uses these extended settings:

- Requires ``DEVICESTATUS_ADVANCED="true"`` to be set
- ``XDRIP-JS_ENABLE_ALERTS`` (``false``) - Set to ``true`` to enable notifications when CGM state is not OK or battery voltages fall below threshold.
- ``XDRIP-JS_STATE_NOTIFY_INTRVL`` (``0.5``) - Set to number of hours between CGM state notifications
- ``XDRIP-JS_WARN_BAT_V`` (``300``) - The voltage of either transmitter battery, a warning will be triggered when dropping below this threshold.

``alexa`` (Amazon Alexa)
^^^^^^^^^^^^^^^^^^^^^^^^

Integration with Amazon Alexa. Detailed setup instructions are `here <https://github.com/nightscout/cgm-remote-monitor/blob/master/lib/plugins/alexa-plugin.md>`__

``speech`` (Speech)
^^^^^^^^^^^^^^^^^^^

Speech synthesis plugin. When enabled, speaks out the blood glucose values, IOB and alarms. Note you have to set the LANGUAGE setting on the server to get all translated alarms.

``cors`` (CORS)
^^^^^^^^^^^^^^^

Enables `CORS <https://en.wikipedia.org/wiki/Cross-origin_resource_sharing>`__ so other websites can make request to your Nightscout site. Uses these
extended settings: 

- ``CORS_ALLOW_ORIGIN`` (``*``) - The list of sites that are allow to make requests

Pushover
^^^^^^^^

See `Pushover`_ for environment variables you can configure for this service.

IFTTT-maker
^^^^^^^^^^^

See `IFTTT-maker`_ for environment variables you can configure for this service.

.. _Pushover: ../3rd%20party%20integration/pushover.html
.. _IFTTT-maker: ../3rd%20party%20integration/IFTTT.html


Extended Settings
-----------------

Some plugins support additional configuration using extra environment variables. These are prefixed with the name of the plugin and a ``_``. For example setting ``MYPLUGIN_EXAMPLE_VALUE=1234`` would make ``extendedSettings.exampleValue`` available to the ``MYPLUGIN`` plugin.

Plugins only have access to their own extended settings, all the extended settings of client plugins will be sent to the browser.

- ``DEVICESTATUS_ADVANCED`` (``true``) - Defaults to true. Users who only have a single device uploading data to Nightscout can set this to false to reduce the data use of the site.

Treatment Profile
-----------------

Some of the `plugins <#plugins>`__ make use of a treatment profile that can be edited using the `Profile Editor <../Understanding%20your%20site/profile-editor.html>`__.


----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.