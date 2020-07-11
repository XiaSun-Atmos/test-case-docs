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

The case runs are initialized at 00z Oct 16, 2017 with 168 hours forecasting. The corresponding namelist options that need to be changed are listed below.


.. table:: Table Namelist options
 :align: center

 +---------------+-------------+
 | Options       | Value       |
 +===============+=============+
 | RUN_STARTDATE | 2017-10-16  |
 +---------------+-------------+
 | START_TOD     | 0           |
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

An example Python script is provided below to do the Skew-T Log-P plots for the observed and simulated sounding profiles. Indices for sounding analysis (e.g. lapse rate) are also calculated and shown at the bottom of the plot. This script is adapted from `SHARPpy <http://sharp.weather.ou.edu/dev/>`_. Data format needs to comply with `SHARPpy requirements <https://sharppy.github.io/SHARPpy/datasource_guide.html>`_. 

* `Download the example script for Skew-T Log-P plot <https://domain.invalid/>`_ 

..............
Case Results
..............

======================================================
Skew-T Log-P Plot
======================================================

.. |logo1| image:: images/2017101700_84z_DNR_16betavsObs_indices-1.png   
   :width: 600
   :align: middle


.. |logo2| image:: images/2017101700_84z_DNR_15p2vsObs_indices-1.png
   :width: 600
   :align: top

+---------+---------+
| |logo1| | |logo2| |
+---------+---------+
