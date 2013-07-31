********************************
Saltstack configuration settings
********************************

============
Install salt
============

.. code-block:: bash

	apt-get install git
	wget -O - http://bootstrap.saltstack.org | sudo sh

Directions are at http://docs.saltstack.com/topics/installation/index.html.



===============
Set up hostname
===============

in `/etc/hosts` set the `salt` hostname to the master salt minion.

If it's just `salt-minion` and working locally, this is not nescessary. If master is on the same server, just add a `127.0.0.1  salt`.


======================
Download this git repo
======================

.. code-block:: bash

	git clone http://docs.saltstack.com/topics/installation/index.html

Be sure you have your ssh key from `~/.ssh/id_rsa.pub` in github settings for property permisions. Also `ssh-keygen -v` if you need to create a new one.

=========================================
Configure `file_roots` and `pillar_roots` 
=========================================

Set `file_roots` and `pillar_roots` for  `/etc/salt/minion` (and `/etc/salt/master` if this is a master instance):

.. code-block:: yaml

	file_roots:
	  base:
	    - /root/salt-cfg

	pillar_roots:
	  base:
	    - /root/salt-cfg/pillar


========
Commands
========

the `top.sls` file inside the salt config can run (if local, no master)

.. code-block:: bash

	salt-call --local state.highstate -ldebug

which will read through the `top.sls` (`top file <http://docs.saltstack.com/ref/states/top.html>`_) and install any packages accordingly. See http://docs.saltstack.com/ref/states/top.html for more de

and also to call packages individually, `state.sls`:

.. code-block:: bash

	salt-call --local state.sls db.mongodb -ldebug
