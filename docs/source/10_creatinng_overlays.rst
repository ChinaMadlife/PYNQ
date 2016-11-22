Creatinng Overlays
==============================================

Introduction
------------------

This section will describe how existing overlays can be created and integrated into PYNQ, but will not cover the hardware design process in detail. Overlays are created using standard Xilinx design methodologies (SDSoC, Vivado, or Vivado HLS), which is a specialised task for hardware designers. 

An overlay consists of a bitstream to configure the Zynq PL, and Python driver, or C library and Python wrapper.

FPGAs and the PL in Zynq can be customized to very specific and optimized implementations. One of the key concepts of an Overlay is that it should be designed to be flexible and reusable for a class of applications, rather than highly customized for a single task. 

For example, it is recommended that IOPs are used for Pmod interfaces to make the overlay as widely applicable as possible, even where the designer intends to use a specific peripheral for a particular application. This may result in a design that uses more FPGA resources than is necessary, but the flexibility and reuseability of the overlay is valued over the overhead of the additional resources used. 


Existing Overlays
-----------------

As seen in previous sections, the bitstream or binary for the base overlay is include in the PYNQ image and available to use. The full source code for the Vivado project which was used to build the bitstream is avialble in the Pynq repository:

   * ``<GitHub repository>/Pynq-Z1/vivado/base``

The source code include HDL code, custom IP, constraints, IOP projects and C code, and the Vivadoe TCL file to build the project. A Makefile is provided to build the Vivado project and generate the bitstream for the overlay. 

As the bitstream for the overlay is provided as part of the PYNQ image, it is not necessary to build the Vivado project. For an FPGA designer, building an existing overlay design allows the project to be opened in Vivado and examined, or used as a starting point to create a new overlay.  

A full Vivado installation is required to design and build overlays. 

.. image:: ./images/vivado_base_overlay.JPG
   :scale: 50%
   :align: center
   
New Overlays
--------------

Overlays are created using the Xilinx Vivado tools. For a standard Zynq design, a Vivado project is usually used to create a PL bitstream, and generate a Zynq boot image*. The boot image will include configuration settings for the Zynq PS derived from the Vivado project. PS settings include CPU clocks and PS to PL clocks; the clock(s) that will be used by an overlay. During the boot process the PS settings are configured and then the bitstream is downloaded to the PL. 

The hardware design process for a new PYNQ overlays is similar to creating a standard PL design for Zynq with one extra consideration. A Vivado project will be created which contains Zynq PS settings, and will be used to generate the bitstream for the PL. However, as the overlay will be loaded dynamically, when PYNQ is running, only the PL bitstream will be used. The Zynq PS settings will not be configured from the Vivado project for the new Overlay. 

An overlay designer should be aware of the base configuration settings for the Zynq before creating a new overlay. It is possible to change the configuration settings for some parts of the Zynq PS when the system is running, however, care must be taken by the designer to ensure the system is always configured correctly. It is recommended to use the Vivado *base* overlay project as a starting point for a new overlay. This will ensure the PYNQ settings for the Zynq PS, and the existing PS/PL interfaces are used in the new project. 

A full example showing how to create a new PYNQ overlay is covered in the next section.

* There are a number of ways to boot a Zynq device. Using a boot image to configure the PS and download a bitstream to the PL is one common method, and should be familiar to Zynq developers. 
   
