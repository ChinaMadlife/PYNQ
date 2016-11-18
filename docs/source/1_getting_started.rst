
This guide will show you how to setup your compter and PYNQ-Z1 board to get started using PYNQ. 
Any issues can be posted to `the PYNQ support forum <https://groups.google.com/forum/#!forum/pynq_project>`_. 

***************
Getting Started
***************

.. contents:: Table of Contents
   :depth: 2

      .. image:: ./images/pynqz1_quick_start.jpg
      :align: center
	  
	  
Setup
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

If you already have a Micro SD card preloaded with the PYNQ-Z1 image, you can skip this step. Preloaded Micro SD cards area available from Digilent when you purchase the board. 

* `Download the PYNQ-Z1 image <https://files.digilent.com/Products/PYNQ/pynq_z1_image_2016_09_14.zip>`_, unzip/extract, and write the image to an SD card. Windows: `win32DiskImager <https://sourceforge.net/projects/win32diskimager/>`_, Linux/MacOS: *dd*.
   
For detailed instructions for writing the SD card using different operating systems, see the `Appendix: Writing the SD card image <17_appendix.rst#writing-the-sd-card-image.html>`_. 
   
PYNQ-Z1 setup
---------------


   .. image:: ./images/pynqz1_setup.jpg
      :align: center

To set up the board:

   1. Set the *boot* jumper (labelled JP4 on the board) is set to **SD** (This sets the board to boot from the Micro-SD card)  
   
   2. Set the *power* jumper (JP5) **USB** if you are powering from a USB cable. (Set to **REG** if using an external power regulator)
   
   3. Insert the **Micro SD** card loaded with the PYNQ-Z1 image into the board. (The Micro SD slot is underneath the board)
   
   4. Connect the USB cable to your PC/Laptop, and to the **PROG/UART** (J14) on the board
   
   5. Connect the Ethernet cable into your board
   
You will use a computer with a web browser to connect to and program the board. You can connect your PYNQ-Z1 board to an Ethernet port on your home router, an Ethenet port or cable on your work network, or you can connnect your board directly to your computer. You need to make sure you have permission to connect devices to your work network, and that there is a DHCP server running on your network that will assign an IP address to an unknown device. Your IT department can usually advise on connecting the board to the network. Home network is usually the easiest way to start using PYNQ. 

===============	 ========================================================	 ========================================================	 ========================================================
	             Home router (DHCP)	                                         Work Network (DHCP)                                         Direct Connection (Static IP)
---------------  --------------------------------------------------------    --------------------------------------------------------    --------------------------------------------------------
                 Connect board to Ethernet port on your router               Connect board to Ethernet port or cable on your network     Connect directly to ethernet port on your computer
Preparation			                                                                                                                     Configure your computer ethernet adapter with Static IP
			
Address          http://pynq:9090                                            http://pynq:9090                                            http://192.168.2.99:9090
Notes            May take some time to resolve the first time you connect    May take some time to resolve the first time you connect    No name resolution. You must use the IP address
			
Optional steps   Change hostname if multiple boards are on network           Change hostname if multiple boards are on network           Bridge Network connectionn
See  below       Enable WAN link to LAN on your router                       Configure proxy                   
===============	 ========================================================	 ========================================================	 ========================================================
	     
   7. **Turn on** the power switch on the board

When you power on the board, you should see a *Red LED*. After a few seconds, you should see a *Yellow/Green LED* (LD12/DONE). This is also a good indication that the boot process has started correctly. 
   
After about 30 seconds the board should finish booting. You should see the two color LEDs flash blue, and the four yellow/green user LEDs flash and remain on once the system is ready. 

Optional steps
---------------

To connect to the board using a terminal, you will use the Micro USB cable which should already be connected. You will need to install/use a terminal emulator to connect to the board. (puTTY <http://www.putty.org/>`_ is free for Windows) 

   Terminal Settings:

   * 115200 baud
   * 8 data bits
   * 1 stop bit
   * No Parity
   * No Flow Control

You can also ssh to the board ("ssh xilinx@pynq", password is xilinx)

If you can access PYNQ using a browser, you can also open a terminal from the browser in the Jupyter portal. To do this, select New > Notebook. Select New terminal, which will open a terminal inside the browser as root. 

You can run the following script to change the hostname:

   .. code-block:: console
   
      sudo /home/xilinx/scripts/hostname.sh NEW_HOST_NAME

(replace NEW_HOST_NAME with the hostname you want for your board)

Change static IP `Appendix: Assign your PC/Laptop a static ip address <17_appendix.html#assign-your-laptop-pc-a-static-ip-address>`_
  
   
Connect to the board
==================================   

If you connect your board to your home router, or network, it should get an IP address from a DHCP server. The network will also resolve the board hostname ("pynq") to the IP address. You can use either the hostname, or IP to connect to the board. 
 
If you connect directly to the Ethernet port of your PC, the board will automatically assign itself a static IP address (``192.168.2.99`` by default). You will need to configure your computer's Ethernet adapter to have an IP address in the same range (e.g. 192.168.2.1). 
   
Terminal `Frequently asked questions <14_faqs.html>`_  
   
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
   
   
<Trouble shooting>
   

You should now be ready to start using Pynq. You can continue reading this documentation, or try using Pynq on the board. 


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
