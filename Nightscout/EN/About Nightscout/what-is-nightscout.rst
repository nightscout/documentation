What is Nightscout?
===================

.. image:: https://cloud.githubusercontent.com/assets/751143/8425633/93c94dc0-1ebc-11e5-99e7-71a8f464caac.png

Nightscout is an open source, Do-It-Yourself (DIY) project that allows real time access to a continuous glucose monitor (CGM) data via a personal website, a smartwatch, or apps and widgets available for smartphones.

Nightscout was developed by parents of children with type 1 diabetes and has continued to be developed, maintained, and supported by volunteers. When first implemented, Nightscout was a solution specifically for remote monitoring of Dexcom G4 CGM data. Today, Nightscout is compatible with an increasing number of glucose monitor models including Dexcom's G4/G5/G6, Freestyle Libre, and Medtronic. Nightscout also provides browser-based visualization for #OpenAPS users, #AndroidAPS users, and Loop users.

`#WeAreNotWaiting <https://twitter.com/hashtag/wearenotwaiting?src=hash&vertical=default&f=images>`_ and `this <https://vimeo.com/109767890>`_ is why.

How does it work?
-----------------

The technology is simple: Your glucose monitor continues to work as it always has by reading the glucose level of the T1D who is wearing a compatible sensor/transmitter. An uploader device reads the data from the glucose monitor and transmits the readings to the Internet, where any web-connected device can view the numbers.

This image from the Wall Street Journal article, `"Citizen Hackers Tinker with Medical Devices" <http://online.wsj.com/articles/citizen-hackers-concoct-upgrades-for-medical-devices-1411762843>`_, illustrates the entire system.

.. image:: http://www.nightscout.info/wp-content/uploads/2014/07/WSJ-Infographic.jpg

Image Courtesy of Wall Street Journal. Published on line, Friday, Sept. 26, 2014

What does it cost?
------------------

The Nightscout software itself is open source and therefore free. There are however incidental costs which will vary based on your needs and setup. The four main cost categories are:

- Internet data upload, i.e. the cost of a smart phone, as well as data package charges if not using wifi
- Web hosting / services, i.e. to run your website and store your data
- In some cases, additional hardware is needed to collect data from the glucose monitor, e.g. a NFC reader for Freestyle Libre 
- Optional accessories such as a smartwatch

At the time of this writing, web hosting / services can for the most part be obtained for free. Setting up accounts with web service providers is covered in the `Deployment to Heroku <../Install%20Config%20Update/deployment-to-heroku.html>`_ section.

Is it safe? Is it approved?
---------------------------

Nightscout is purely DIY software, built by patient volunteers or their caregivers, each to meet their own needs. All code is available online, and each user of Nightscout must decide for themselves whether they consider it safe. While all development takes place with safety as a first priority, the information shown on Nightscout cannot replace your primary, approved information source, i.e. the software or device provided with your glucose monitor.

In short:

- Do not use any of the Nightscout information or code to make medical decisions.
- There is no support or any warranty of any kind.
- The quality and performance of the project is with you if you choose to use it.

Regulatory authorities require each submitted product to have a legal manufacturer. Given there is no central organization responsible for Nightscout, it cannot be formally approved.

Where do I find more information?
---------------------------------

The menu to the left provides links to further information, including how to install Nightscout and how to understand its interface. If you have a question not covered in the documentation, head over to `Where to get help <./where-to-get-help.html>`_.

----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.