IFTTT maker
===========

In addition to the normal web based alarms, and pushover, there is also integration for `IFTTT Maker <https://ifttt.com/maker>`__.

With Maker you are able to integrate with all the other `IFTTT Channels <https://ifttt.com/channels>`__. For example you can send a tweet when there is an alarm, change the color of hue light, send an email, send and sms, and so much more.

1. Setup IFTTT account: `login <https://ifttt.com/login>`__ or `create an account <https://ifttt.com/join>`__
2. Find your secret key on the `maker page <https://ifttt.com/maker>`__
3. Configure Nightscout by setting these environment variables:

	-  ``ENABLE`` - ``maker`` should be added to the list of plugin, for example: ``ENABLE="maker"``.
	-  ``MAKER_KEY`` - Set this to your secret key that you located in step 2, for example:    ``MAKER_KEY="abcMyExampleabc123defjt1DeNSiftttmak-XQb69p"`` This also support a space delimited list of keys.
	-  ``MAKER_ANNOUNCEMENT_KEY`` - An optional Maker key, will be used for system wide user generated announcements. If not defined this will fallback to ``MAKER_KEY``. A possible use for this is sending important messages and alarms to a CWD that you don't want to send all notification too. This also support a space delimited list of keys.

4. `Create a recipe <https://ifttt.com/myrecipes/personal/new>`__ or see `more detailed instructions <https://github.com/nightscout/cgm-remote-monitor/blob/master/lib/plugins/maker-setup.md#create-a-recipe>`__

Plugins can create custom events, but all events sent to maker will be prefixed with ``ns-``. The core events are: 
- ``ns-event`` - This event is sent to the maker service for all alarms and notifications. This is good catch all event for general logging.
- ``ns-allclear`` - This event is sent to the maker service when an alarm has been ack'd or when the server starts up without triggering any alarms. For example, you could use this event to turn a light to green.
- ``ns-info`` - Plugins that generate notifications at the info level will cause this event to also be triggered. It will be sent in addition to ``ns-event``.
- ``ns-warning`` - Alarms at the warning level with cause this event to also be triggered. It will be sent in addition to ``ns-event``. 
- ``ns-urgent`` - Alarms at the urgent level with cause this event to also be triggered. It will be sent in addition to ``ns-event``.
- see the `full list of events <https://github.com/nightscout/cgm-remote-monitor/blob/master/lib/plugins/maker-setup.md#events>`__

----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.
