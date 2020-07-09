.. BarryCase documentation master file, created by
   sphinx-quickstart on Mon Jul  6 13:31:15 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.



2017 Denver Inversion
=====================================
  

..............................
Namelist,Datasets and Scripts
..............................
===================
Namelist
===================

The case runs are initialized at 12z Oct 19, 2017 with 168 hours forecasting. The corresponding namelist options that need to be changed are listed below.


.. table:: Table Namelist options
 :align: center

 +---------------+-------------+
 | Options       | Value       |
 +===============+=============+
 | RUN_STARTDATE | 2017-10-19  |
 +---------------+-------------+
 | START_TOD     | 43200       |
 +---------------+-------------+
 | STOP_OPTION   | 168         |
 +---------------+-------------+
 | STOP_N.       | nhours      |
 +---------------+-------------+

====================================
Datasets
====================================

Initial condition (IC)  files are created from GFS reanalysis dataset in nemsio format. These files should be 
put in the /run/INPUT directory.

* `Download the 2019 Denver Inversion case initial condition files <https://domain.invalid/>`_

Sounding profiles can be downloaded from the `University of Wyoming <http://weather.uwyo.edu/upperair/sounding.html>`_.

====================================
Scripts
====================================

An example Python script is provided below to do the Skew-T Log-P plot based on the observed and simulated sounding profiles. Indices for sounding analysis (e.g. cap strength) are also calculated at the bottom of the plot. This script is adapted from `SHARPpy <http://sharp.weather.ou.edu/dev/>`_. 

* `Download the example script for Skew-T Log-P plot <https://domain.invalid/>`_ 

..............
Case Results
..............

======================================================
Skew-T Log-P Plot
======================================================

.. |logo1| image:: images/Skew-T1.png   
   :width: 600
   :align: middle


.. |logo2| image:: images/Skew-T2.png
   :width: 600
   :align: top

+---------+---------+
| |logo1| | |logo2| |
+---------+---------+
