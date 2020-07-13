.. BarryCase documentation master file, created by
   sphinx-quickstart on Mon Jul  6 13:31:15 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.



2020 Janurary Cold Bias
=====================================
  
..............................
Model Configuration and Datasets
..............................

The case runs are initialized at 12z Jan 17, 2020 with 168 hours forecasting. The corresponding namelist options that need to be changed are listed below. The app uses ``./xmlchange`` to change the runtime settings. The settings needs to be modified to set up the start date, start time, and run time are listed below.

.. code-block:: bash
 
   ./xmlchange RUN_STARTDATE=2020-01-17,START_TOD=43200,STOP_OPTION=nhours,STOP_N=168


Initial condition (IC)  files are created from GFS reanalysis dataset in nemsio format. These files should be 
put in the /run/INPUT directory.

:download:`Initial condition files <https://domain.invalid/>`

The `GFS reanalysis dataset <https://www.ncdc.noaa.gov/data-access/model-data/model-datasets/global-forcast-system-gfs>`_ are used as 'truth' to compare with simulation results.

..............
Case Results
..............

======================================================
2-m Temperature
======================================================
:download:`Source script <../script/hurrican_track_intensity.py>`

.. |logo1| image:: images/FV3_T2_20200121_1200_GFSv16beta.png   
   :width: 600
   :align: middle


.. |logo2| image:: images/FV3_T2_20200121_1200.png
   :width: 600
   :align: top

.. |logo3| image:: images/GFSANL_T2_20200121_1200.png
   :width: 600
   :align: top

.. |logo4| image:: images/Diff_FV3_T2_20200121_1200_GFSv16beta.png
   :width: 600
   :align: top

+---------+---------+
| |logo1| | |logo2| |
+---------+---------+
| |logo3| | |logo4| |
+---------+---------+