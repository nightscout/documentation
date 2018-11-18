Pushover
========

In addition to the normal web based alarms, there is also support for `Pushover <https://pushover.net/>`__ based alarms and notifications.

To get started install the Pushover application on your iOS or Android device and create an account.

Using that account login to `Pushover <https://pushover.net/>`__, in the top left you’ll see your User Key, you’ll need this plus an application API Token/Key to complete this setup.

You’ll need to `Create a Pushover Application <https://pushover.net/apps/build>`__. You only need to set the Application name, you can ignore all the other settings, but setting an Icon is a nice touch. Maybe you'd like to use `this one <https://raw.githubusercontent.com/nightscout/cgm-remote-monitor/master/static/images/large.png>`__?

Pushover is configured using the following Environment Variables:

    - ``ENABLE`` - ``pushover`` should be added to the list of plugin, for example: `ENABLE="pushover"`.
    - ``PUSHOVER_API_TOKEN`` - Used to enable pushover notifications, this token is specific to the application you create from in `Pushover <https://pushover.net/>`__.
    - ``PUSHOVER_USER_KEY`` - Your Pushover user key, can be found in the top left of the `Pushover <https://pushover.net/>`__ site, this can also be a pushover delivery group key to send to a group rather than just a single user.  This also supports a space delimited list of keys.  To disable `INFO` level pushes set this to `off`.
    - ``PUSHOVER_ALARM_KEY`` - An optional Pushover user/group key, will be used for system wide alarms (level > ``WARN``).  If not defined this will fallback to ``PUSHOVER_USER_KEY``.  A possible use for this is sending important messages and alarms to a CWD that you don't want to send all notification too.  This also support a space delimited list of keys.  To disable Alarm pushes set this to `off`.
    - ``PUSHOVER_ANNOUNCEMENT_KEY`` - An optional Pushover user/group key, will be used for system wide user generated announcements.  If not defined this will fallback to ``PUSHOVER_USER_KEY`` or ``PUSHOVER_ALARM_KEY``.  This also support a space delimited list of keys. To disable Announcement pushes set this to ``off``.
    - ``BASE_URL`` - Used for pushover callbacks, usually the URL of your Nightscout site, use https when possible.
    - ``API_SECRET`` - Used for signing the pushover callback request for acknowledgments.

    If you never want to get info level notifications (treatments) use ``PUSHOVER_USER_KEY="off"``
    If you never want to get an alarm via pushover use ``PUSHOVER_ALARM_KEY="off"``
    If you never want to get an announcement via pushover use ``PUSHOVER_ANNOUNCEMENT_KEY="off"``

    If only ``PUSHOVER_USER_KEY`` is set it will be used for all info notifications, alarms, and announcements.

For testing/development try `localtunnel <http://localtunnel.me/>`__.
	
----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.
