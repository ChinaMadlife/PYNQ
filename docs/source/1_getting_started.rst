This guide will show you how to setup your computer and PYNQ-Z1 board to get started using PYNQ. 
Any issues can be posted to `the PYNQ support forum <https://groups.google.com/forum/#!forum/pynq_project>`_. 

***************
Getting Started
***************

.. contents:: Table of Contents
   :depth: 2
	  
	  
Video Guide
=================

You can watch the getting started video guide, or follow the instructions below.


.. raw:: html

    <embed>
        <iframe width="300" height="200" src="https://www.youtube.com/embed/-VE97r5XpEU" frameborder="0" allowfullscreen></iframe>
        </br>
        </br>
    </embed>


Prerequisites
=============

* PYNQ-Z1 board
* Computer with compatible browser (`Supported Browsers <http://jupyter-notebook.readthedocs.org/en/latest/notebook.html#browser-compatibility>`_)
* Ethernet cable
* Micro USB cable 
* Micro-SD card with preloaded image, or blank card (Minimum 8GB recommended)


Get the image and prepare the Micro-SD Card
----------------------------------------------------

Preloaded Micro SD cards are available from Digilent. If you already have one of these Micro SD card preloaded with the PYNQ-Z1 image, you can skip this step. 

To make your own PYNQ Micro-SD card:

   * `Download and the PYNQ-Z1 image <https://files.digilent.com/Products/PYNQ/pynq_z1_image_2016_09_14.zip>`_ and unzip
   * Write the image to a blank Micro SD card (minimum 8GB recommended)
      * Windows: Use `win32DiskImager <https://sourceforge.net/projects/win32diskimager/>`_
      * Linux/MacOS: Use the built in *dd* command
   
For detailed instructions for writing the SD card using different operating systems, see the `Appendix: Writing the SD card image <17_appendix.rst#writing-the-sd-card-image>`_. 
   
Setup the PYNQ-Z1 
===================


   .. image:: ./images/pynqz1_setup.jpg
      :align: center


1. Set the *boot* jumper (labelled JP4 on the board) is set to **SD** (This sets the board to boot from the Micro-SD card)  
   
2. Set the *power* jumper (JP5) **USB** if you are powering from a USB cable. (Set to **REG** if using an external power regulator)
   
3. Insert the **Micro SD** card loaded with the PYNQ-Z1 image into the board. (The Micro SD slot is underneath the board)
  
4. Connect the USB cable to your PC/Laptop, and to the **PROG/UART** (J14) on the board
   
5. Connect the Ethernet cable into your board
   

Connect to the board
------------------------

You can connect your PYNQ-Z1 board in three ways:

1. To a port on your home router

2. To a work network 

3. Directly to an Ethernet port on your computer

For a work network, make sure you have permission to connect devices. 


Connect to a network
--------------------------

Connecting to a network with internet access allows you to update your board and install new packages. If you are connecting to a work network, you may need to configure proxy settings. If you have more than one board on a network, you will need to change the hostname so that each board has a unique name. 

+----------------------------------------+
| Home router/Work Network               |
| (DHCP)                                 |
+========================================+
| 1. Connect to Ethernet port on         |
| router/switch                          |
+----------------------------------------+
| 2. Browse to http://pynq:9090          |
+----------------------------------------+
| 3. Optional: Change hostname (if more  |
| than one board on network)\*           |
+----------------------------------------+
| 4. Optional: Configure proxy\*         |
+----------------------------------------+

\* This can be done after the board is powered on. See below for instructions

Connect directly to your computer
---------------------------------------

You will need to have an Ethernet port available on your computer. This is a simple way to connect to your board. You will be able to use PYNQ, but unless you can bridge the board connection to an internet connection, your board will not have internet access, and you will be unable to update or load new packages.  

+-----------------------------------------+
| Direct Connection to your computer      |
| (Static IP)                             |
+=========================================+
| 1. Configure your computer              |
| with a Static IP\*                      |
+-----------------------------------------+
| 2. Connect directly to your             |
| computer's Ethernet port                |
+-----------------------------------------+
| 3. Browse to                            |
| http://192.168.2.99:9090                |
+-----------------------------------------+

\* See `Appendix: Assign your PC/Laptop a static IP address <17_appendix.html#assign-your-laptop-pc-a-static-ip-address>`_


Powering on
--------------

*Turn On* the power switch on the board to power on the board. You should see a *Red LED*. After a few seconds, you should see a *Yellow/Green LED* (LD12/DONE). 
   
After about 30 seconds you should see the two color LEDs flash blue, and the four yellow/green user LEDs flash and remain on once the system is ready. 
  

Connect to Jupyter  
===============================

* Open a web browser and go to `http://pynq:9090 <http://pynq:9090>`_ (network) `http://192.168.2.99:9090 <http://192.168.2.99:9090>`_ (direct connection)
* The Jupyter username/password is xilinx/xilinx
   
   .. image:: ./images/portal_homepage.jpg
      :height: 600px
      :scale: 75%
      :align: center


The default hostname is **pynq** and the default static IP address is ``192.168.2.99``. If you changed the hostname or static IP of the board, you will need to change the address you browse to. 
   
The first time you connect, it may take a few seconds for your computer to resolve the hostname/IP address. 
   
Change hostname
----------------------

If you are on a network where there may be other *pynq* boards, you should change your hostname immediately. E.g. work or university network. 

Open a terminal from the browser in the Jupyter portal by selecting **New > Notebook**. 

Select **New terminal**, which will open a terminal inside the browser as root. 

   .. image:: ./images/dashboard_files_tab_new.JPG
      :height: 300px
      :align: center


   .. code-block:: console
   
      sudo /home/xilinx/scripts/hostname.sh NEW_HOST_NAME

(replace NEW_HOST_NAME with the hostname you want for your board)

   .. image:: ./images/change_hostname.jpg
      :height: 300px
      :align: center
	  
Follow the instructions to reboot the board. 

   .. code-block:: console
   
      sudo shutdown -r now
	  
When the board reboots, reconnect using the new hostname. e.g. http://pynq_cmc:9090

If you can't connect to your board because there is already a board on the network with the hostname 'pynq', see the step below to open a terminal using the micro USB cable. 

Configure proxy
--------------------

If your board is connected to a network that uses a proxy, you need to set the proxy variables on the board. Open a terminal as above and enter the following where you should replace "my_http_proxy:8080" and "my_https_proxy:8080" with your settings.  

   .. code-block:: console
   
      set http_proxy=my_http_proxy:8080
      set https_proxy=my_https_proxy:8080


Connect to terminal using USB
---------------------------------

If you need to change settings on the board but you can't access the terminal from Jupyter, you can use connect a terminal using the micro USB cable already connected to the board. 

You will need to use a terminal emulator to connect to the board. (puTTY <http://www.putty.org/>`_ is available for free for Windows) 

   Terminal Settings:

   * 115200 baud
   * 8 data bits
   * 1 stop bit
   * No Parity
   * No Flow Control

You can then run the same commands listed above to change the hostname, or configure a proxy. 

You can also check the hostname of the board by running the *hostname* command:

   .. code-block:: console
   
      hostname
	  
You can also check the IP address of the board using *ifconfig*:

   .. code-block:: console
   
      ifconfig
	  
Using PYNQ
==========================

   
Getting started notebooks
----------------------------

A Jupyter notebook can be saved as html webpages. Some of this documentation has been generated directly from Jupyter notebooks. 

You can view the documentation as a webpage, or if you have a board running PYNQ, you can view and run the notebook documentation interactively. The documentation available as notebooks can be found in the *Getting_Started* folder in the Jupyter home area. 
 
.. image:: ./images/getting_started_notebooks.jpg
   :height: 600px
   :scale: 75%
   :align: center
   

There are also a number of example notebooks available showing how to use various peripherals with the board. 

.. image:: ./images/example_notebooks.jpg
   :height: 600px
   :scale: 75%
   :align: center

When you open a notebook and make any changes, or execute cells, the notebook document will be modified. It is recommended that you "Save a copy" when you open a new notebook. If you want to restore the original versions, you can download all the example notebooks from the `PYNQ GitHub page <www.github.com/xilinx/pynq>`_ .    
   
Accessing files on the board
----------------------------
`Samba <https://www.samba.org/>`_, a file sharing service, is running on the board. The home area on the board can be accessed as a network drive, and you can transfer files to and from the board. 

In Windows, to access the PYNQ home area you can go to:

``\\pynq\xilinx`` 

or 

``\\192.168.2.99\xilinx``  

Or in Linux: 

``smb://pynq/xilinx`` 

or 

``smb://192.168.2.99/xilinx``

Remember to change the hostname/IP address if necessary.

The Samba username:password is ``xilinx:xilinx``

.. image:: ./images/samba_share.JPG
   :height: 600px
   :scale: 75%
   :align: center


Troubleshooting
==========================

If you are having problems, please see the `Frequently asked questions <14_faqs.html>`_ or go the `PYNQ support forum <http://www.pynq.io>`_
