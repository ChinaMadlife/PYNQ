
This guide will show you how to setup your compter and PYNQ-Z1 board to get started using PYNQ. 
Any issues can be posted to `the PYNQ support forum <https://groups.google.com/forum/#!forum/pynq_project>`_. 

***************
Getting Started
***************

.. contents:: Table of Contents
   :depth: 2

      .. image:: ./images/pynqz1_quick_start.jpg
      :align: center
	  
	  
Setup the board
================

Prerequisites
-------------

* PYNQ-Z1 board
* Computer with compatible browser (`Supported Browsers <http://jupyter-notebook.readthedocs.org/en/latest/notebook.html#browser-compatibility>`_)
* Micro-SD card (Minimum 8GB recommended)
* Ethernet cable
* Micro USB cable 
* USB port

Get the image and prepare the micro-SD Card
----------------------------------------------------

Preloaded Micro SD cards are available from Digilent. If you already have one of these Micro SD card preloaded with the PYNQ-Z1 image, you can skip this step. To make your own:

* `Download the PYNQ-Z1 image <https://files.digilent.com/Products/PYNQ/pynq_z1_image_2016_09_14.zip>`_, unzip/extract, and write the image to an Micro SD card (minimum 8GB recommended). 

On Windows `win32DiskImager <https://sourceforge.net/projects/win32diskimager/>`_ can be used to write the image. On Linux/MacOS: *dd* can be used.   
For detailed instructions for writing the SD card using different operating systems, see the `Appendix: Writing the SD card image <17_appendix.rst#writing-the-sd-card-image>`_. 
   
Setup the PYNQ-Z1 
------------------


   .. image:: ./images/pynqz1_setup.jpg
      :align: center


   1. Set the *boot* jumper (labelled JP4 on the board) is set to **SD** (This sets the board to boot from the Micro-SD card)  
   
   2. Set the *power* jumper (JP5) **USB** if you are powering from a USB cable. (Set to **REG** if using an external power regulator)
   
   3. Insert the **Micro SD** card loaded with the PYNQ-Z1 image into the board. (The Micro SD slot is underneath the board)
   
   4. Connect the USB cable to your PC/Laptop, and to the **PROG/UART** (J14) on the board
   
   5. Connect the Ethernet cable into your board
   
You will use a computer with a web browser to connect to and program the board. You can connect your PYNQ-Z1 board to an Ethernet port on your home router, an Ethenet port or cable on your work network, or directly to your computer. You need to make sure you have permission to connect devices to your work network, and that there is a DHCP server running that will assign an IP address to an unknown device. A home router is usually the easiest way to start using PYNQ. 



+---------------+--------------------------------------------------------+--------------------------------------------------------+---------------------------------------------------------+
|               |Home router (DHCP)	                                     |Work Network (DHCP)                                     |Direct Connection (Static IP)                            |
+===============+========================================================+========================================================+=========================================================+
|               |Connect board to Ethernet port on your router           |Connect board to Ethernet port or cable on your network |Connect directly to ethernet port on your computer       |
+---------------+--------------------------------------------------------+--------------------------------------------------------+---------------------------------------------------------+
|               |                                                        |                                                        |Configure your computer ethernet adapter with Static IP  |
+---------------+--------------------------------------------------------+--------------------------------------------------------+---------------------------------------------------------+
|Address        |http://pynq:9090                                        |http://pynq:9090                                        |http://192.168.2.99:9090                                 |
+---------------+--------------------------------------------------------+--------------------------------------------------------+---------------------------------------------------------+
|Optional steps |Change hostname if multiple pynq boards are on network  |Change hostname if multiple pynq boards are on network  |                                                         |
+See below      +--------------------------------------------------------+--------------------------------------------------------+---------------------------------------------------------+
|               |                                                        |Configure proxy                                         |                                                         |
+---------------+--------------------------------------------------------+--------------------------------------------------------+---------------------------------------------------------+



=============  ========================================================  ======================================================  ========================================================
               Home router (DHCP)	                                     Work Network (DHCP)                                     Direct Connection (Static IP)                            
=============  ========================================================  ======================================================  ========================================================
               Connect board to Ethernet port on your router             Connect board to Ethernet port or cable on your network Connect directly to ethernet port on your computer       
                                                                                                                                 Configure your computer ethernet adapter with Static IP  
Address        http://pynq:9090                                          http://pynq:9090                                        http://192.168.2.99:9090                                 
Optional steps Change hostname if multiple pynq boards are on network    Change hostname if multiple pynq boards are on network                                                           
See below      
                                                                         Configure proxy                                                                                                  
=============  ========================================================  ======================================================  ========================================================






**Turn on** the power switch on the board

When you power on the board, you should see a *Red LED*. After a few seconds, you should see a *Yellow/Green LED* (LD12/DONE). This is also a good indication that the boot process has started correctly. 
   
After about 30 seconds the board should finish booting. You should see the two color LEDs flash blue, and the four yellow/green user LEDs flash and remain on once the system is ready. 
  
   
Connect to the board
==================================   

If you connected your board to your home router, or network, it should get an IP address from a DHCP server. The network will also resolve the board hostname ("pynq") to the IP address. You can use the hostname to connect to the board. 
 
If you connect directly to the Ethernet port of your PC, the board will automatically assign itself a static IP address (``192.168.2.99`` by default). You will need to `Configure your computer ethernet adapter with Static IP addess<17_appendix.html#assign-your-laptop-pc-a-static-ip-address>`_ in the same range (e.g. 192.168.2.1). 
   
   
Open a web browser and connect to Pynq Jupyter Notebooks web portal
---------------------------------------------------------------------------

If the board is connected to your network:

   * Open a web browser and go to `http://pynq:9090 <http://pynq:9090>`_ (network) `http://192.168.2.99:9090 <http://192.168.2.99:9090>`_ (direct connection)
   * The Jupyter username/password is xilinx/xilinx
   
   .. image:: ./images/portal_homepage.jpg
      :height: 600px
      :scale: 75%
      :align: center


	  
The default hostname of the board is **pynq** and the default static IP address is ``192.168.2.99``. If you changed the hostname or static IP of the board, you will need to change the address above to match your hostname. 
   
It may take a few seconds for your computer to resolve the hostname/IP address. 
   
Change hostname
=========================
If you are on a network where there may be other *pynq* boards, you should change your hostname immediately. Open a terminal from the browser in the Jupyter portal. To do this, select New > Notebook. Select New terminal, which will open a terminal inside the browser as root. 

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
	  
When the board reboots, reconnect using the new hostname. e.g. http://pynq_cmc

Configure proxy
========================

If your board is connected to a network that uses a proxy, you need to set the proxy variables on the board. Open a terminal as above and enter the following where you should replace "my_http_proxy:8080" and "my_https_proxy:8080" with your settings.  

   .. code-block:: console
   
      set http_proxy=my_http_proxy:8080
      set https_proxy=my_https_proxy:8080

Troubleshooting
=========================

Connect to terminal
---------------
If you need to change settings on the board but you can't access the terminal from Jupyter, you can use connect a terminal using the micro USB cable already connected to the board. 

To connect to the board using a terminal, you will use the Micro USB cable which should already be connected. You will need to install/use a terminal emulator to connect to the board. (puTTY <http://www.putty.org/>`_ is free for Windows) 

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
	  
Using Pynq
==========================

   
Getting started notebooks
----------------------------

Jupyter notebooks can be saved as html webpages. Some of this Pynq documentation has been generated directly from Jupyter notebooks. 

You can view the documentation as a webpage, or if you have a board running Pynq, you can view and run the notebook documentation interactively. The documentation available as notebooks can be found in the *Getting_Started* folder in the Jupyter home area. 
 
.. image:: ./images/getting_started_notebooks.jpg
   :height: 600px
   :scale: 75%
   :align: center
   

There are also a number of example notebooks available showing how to use various peripherals with the board. 

.. image:: ./images/example_notebooks.jpg
   :height: 600px
   :scale: 75%
   :align: center

When you open a notebook and make any changes, or execute cells, the notebook document will be modified. It is recommended that you "Save a copy" when you open a new notebook. Original copies of all the notebooks can be found on the `PYNQ GitHub page <www.github.com/xilinx/pynq>`_ .    
   
Accessing files on the board
----------------------------
`Samba <https://www.samba.org/>`_, a file sharing service, is running on the board. The home area on the board can be accessed as a network drive, and you can transfer files to and from the board. 

In Windows, to access the pynq home area you can go to:

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
--------------------
If you are having problems getting the board set up, please see the `Frequently asked questions <14_faqs.html>`_ or go the `PYNQ support forum <http://www.pynq.io>`_


Change static IP `Appendix: Assign your PC/Laptop a static ip address <17_appendix.html#assign-your-laptop-pc-a-static-ip-address>`_

Terminal `Frequently asked questions <14_faqs.html>`_  
