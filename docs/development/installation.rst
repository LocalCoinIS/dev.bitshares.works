
***********************
Getting Started 
***********************

.. _installation-guide:

Installation
========================

LocalCoin Core is the LocalCoin blockchain implementation and command-line interface. The web wallet is `LocalCoin UI <https://github.com/localcoinis/localcoin-ui>`_.

Visit `LocalCoin.is <https://LocalCoin.is/>`_ to learn about LocalCoin and join the community at `LocalCoinTalk.org <https://localcointalk.org/>`_.

**NOTE:** The official LocalCoin git repository location, default branch, and submodule remotes were recently changed. Existing repositories can be updated with the following steps::

	git remote set-url origin https://github.com/localcoinis/localcoin-core.git
	git checkout master
	git remote set-head origin --auto
	git pull
	git submodule sync --recursive
	git submodule update --init --recursive
	
	
.. Attention:: See LocalCoin :ref:`system requirements <system-requirements-node>`.


Download and Build
-----------------------

Select an operation system and install and build.

.. toctree:: 
    :maxdepth: 1

    installation/build_ubuntu
    installation/build_osx
    installation/build_windows
    installation/build_windows_devenv
    installation/windows_cli_tool
	

Build and Run LocalCoin-Core in WSL (Installation Option)
---------------------------------------------------------

.. toctree:: 
    :maxdepth: 1

    installation/wsl
	
Known issues
-------------

.. toctree:: 
    :maxdepth: 1

    installation/boost_versions


------------------------

	
|

