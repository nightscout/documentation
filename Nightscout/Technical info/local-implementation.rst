Local implementation of Nightscout
==================================

In addition to the recommended Heroku installation, it is technically possible to install Nightscout locally:

- Linux based install (Debian, Ubuntu, Raspbian) install with own Node.JS and MongoDB install (see software requirements below)
- Windows based install with own Node.JS and MongoDB install (see software requirements below)
- Vagrant install

Software requirements
---------------------

-  `Node.js <http://nodejs.org/>`__ Latest Node 8 LTS (Node 8.11.3 or later). Use `Install instructions for Node <https://nodejs.org/en/download/package-manager/>`__ or use ``setup.sh``
-  `MongoDB <https://www.mongodb.com/download-center?jmp=nav#community>`__ 3.x or later. MongoDB 2.4 is only supported for Raspberry Pi.


Installation on Linux
---------------------

As a non-root user clone `this repo <https://github.com/nightscout/cgm-remote-monitor>`__ then install dependencies into the root of the project:

.. code:: bash

    $ npm install
	

Installation notes for Windows and Node 10
------------------------------------------

-  See `install MongoDB, Node.js, and Nightscout on a single Windows system <https://github.com/jaylagorio/Nightscout-on-Windows-Server>`__, if you want to host your Nightscout outside of the cloud. Although the instructions are intended for Windows Server the procedure is compatible with client versions of Windows such as Windows 7 and Windows 10.
-  If you deploy to Windows and want to develop or test you need to install `Cygwin <https://www.cygwin.com/>`__ (use `setup-x86\_64.exe <https://www.cygwin.com/setup-x86\_64.exe>`__ and make sure to install ``build-essential`` package. Test your configuration by executing ``make`` and check if all tests are ok.
-  There may be some issues with Node 10.6.0 or later with Nightscout. Node 10 support will be in the 0.11 release. Please don't use Nightscout with (Node 9 or) Node 10 at this moment.


Vagrant install
---------------

Optionally, use `Vagrant <https://www.vagrantup.com/>`__ with the included ``Vagrantfile`` and ``setup.sh`` to install OS and node packages to a virtual machine.

.. code:: bash

    host$ vagrant up
    host$ vagrant ssh
    vm$ setup.sh

The setup script will install OS packages then run ``npm install``.

The Vagrant VM serves to your host machine only on 192.168.33.10, you can access the web interface on http://192.168.33.10:1337


Setting environment variables
-----------------------------

Easy to emulate on the commandline:

.. code:: bash

        echo 'MONGO_CONNECTION=mongodb://sally:sallypass@ds099999.mongolab.com:99999/nightscout' >> my.env
        echo 'MONGO_COLLECTION=entries' >> my.env

From now on you can run using

.. code:: bash

        $ (eval $(cat my.env | sed 's/^/export /') && PORT=1337 node server.js)

		
----------

All information, thought, and code described here is intended for informational and educational purposes only. Nightscout currently makes no attempt at HIPAA privacy compliance. Use of code from github.com is without warranty or support of any kind. Please review the LICENSE found within each repository for further details. Use Nightscout at your own risk, and do not use the information or code to make medical decisions.