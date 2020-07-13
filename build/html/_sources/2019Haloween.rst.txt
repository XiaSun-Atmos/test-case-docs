.. BarryCase documentation master file, created by
   sphinx-quickstart on Mon Jul  6 13:31:15 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.



2019 Halloween Storm
=====================================

The 2019 Halloween storm stroke the eastern U.S. cities with wind gusts, thunderstorms, and flash flooding. 

..............................
Model Configuration and Datasets
..............................

The case runs are initialized at 12z Oct 25, 2019 with 168 hours forecasting. The corresponding namelist options that need to be changed are listed below. The app uses ``./xmlchange`` to change the runtime settings. The settings that need to be modified to set up the start date, start time, and run time are listed below.

.. code-block:: bash
 
   ./xmlchange RUN_STARTDATE=20191025,START_TOD=43200,STOP_OPTION=nhours,STOP_N=168

.. warning:: The model run time step is reduced from the default 225s to 150s (dt_atmos=150) in this case due to the model instability in GFSv16beta. To set the time step, add ``dt_atmos=150`` to ``user_nl_ufsatm``

Initial condition (IC)  files are created from GFS reanalysis dataset in nemsio format. The `GFS reanalysis dataset <https://www.ncdc.noaa.gov/data-access/model-data/model-datasets/global-forcast-system-gfs>`_ are used as 'truth' to compare with simulation results.

:download:`Initial condition files <https://domain.invalid/>`

..............
Case Results
..............

======================================================
500mb Geopotentail Height and Aboslute Vorticity Map
======================================================
:download:`Source script <../script/hurrican_track_intensity.py>`

.. |logo1| image:: images/500mb_2019110100_16beta_150s.png   
   :width: 600
   :align: middle


.. |logo2| image:: images/500mb_2019110100_15p2_150s.png
   :width: 600
   :align: top

.. |logo3| image:: images/500mb_2019110100_NAM.png
   :width: 600
   :align: top

+---------+---------+
| |logo1| | |logo2| |
+---------+---------+
| |logo3| |         |
+---------+---------+

====================================
Composite Reflectivity
====================================
:download:`Source script <../script/hurrican_track_intensity.py>`

.. |logo4| image:: images/GFS16beta_f156_REFC_entireatmosphere.png  
   :width: 600
   :align: middle

.. |logo5| image:: images/GFS15p2_f156_REFC_entireatmosphere.png
   :width: 600
   :align: top

.. |logo6| image:: images/GFSANL_00z1Nov_REFC_entireatmosphere.png
   :width: 600
   :align: top

+---------+---------+
| |logo4| | |logo5| |
+---------+---------+
| |logo6| |         |
+---------+---------+

====================================
Surface Gust
====================================
:download:`Source script <../script/hurrican_track_intensity.py>`

.. |logo7| image:: images/GFS16beta_f156_GUST_surface.png  
   :width: 600
   :align: middle


.. |logo8| image:: images/GFS15p2_f156_GUST_surface.png
   :width: 600
   :align: top

.. |logo9| image:: images/GFSANL_00z1Nov_GUST_surface.png
   :width: 600
   :align: top

+---------+---------+
| |logo7| | |logo8| |
+---------+---------+
| |logo9| |         |
+---------+---------+

====================================
2-m Temperature
====================================
:download:`Source script <../script/hurrican_track_intensity.py>`

.. |logo10| image:: images/GFS16beta_f156_TMP_2maboveground.png  
   :width: 600
   :align: middle


.. |logo11| image:: images/GFS15p2_f156_TMP_2maboveground.png 
   :width: 600
   :align: middle

.. |logo12| image:: images/GFSANL_00z1Nov_TMP_2maboveground.png 
   :width: 600
   :align: top

+----------+----------+
| |logo10| | |logo11| |
+----------+----------+
| |logo12| |          |
+----------+----------+
