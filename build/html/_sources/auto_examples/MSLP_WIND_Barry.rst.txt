.. only:: html

    .. note::
        :class: sphx-glr-download-link-note

        Click :ref:`here <sphx_glr_download_auto_examples_MSLP_WIND_Barry.py>`     to download the full example code
    .. rst-class:: sphx-glr-example-title

    .. _sphx_glr_auto_examples_MSLP_WIND_Barry.py:


Plotting Time Series of Hurricane Max. WS and Min. MSLP
==========================================

This example uses plots the hurricane tracks and intensity estimated from tc-tracker as well as the BestTrack data.


.. code-block:: default

    from __future__ import print_function
    import Ngl, Nio
    import pandas as pd
    import numpy as np
    import xarray as xr
    import netCDF4 as nc
    from netCDF4 import Dataset
    import matplotlib.pyplot as plt
    import math
    #wgrib2 GFSPRS.GrbF72 -match '^(656|685|686|):' -grib GFSPRS.GrbF72_subset
    #comp="15p2"
    comp="v16beta"
    npfull =51
    postfile=nc.MFDataset("/home/Xia.Sun/CIME_OUT/ufs-mrweather-app-workflow_"+comp+".c768/2019071100/GFSPRS.GrbF72_subset.nc")
    #sfcuv=nc.MFDataset('/home/Xia.Sun/CIME_OUT/ufs-mrweather-app-workflow_15p2.c768//2019071100/GFSPRS.GrbF72_subset.nc')
    mslp=postfile["MSLET_meansealevel"][0,:,:]*0.01
    sfugrd=postfile["UGRD_10maboveground"][0,:,:]*1.9438445
    sfvgrd=postfile["VGRD_10maboveground"][0,:,:]*1.9438445
    sfcws=((sfugrd**2+sfvgrd**2)**(1/2.0)) # in knots
    #sfu10m=sfugrd*1.9438445
    #reposat=nc.MFDataset('/glade/u/home/xiasun/scratch/FV3_RT/repo_sat/fv3_gfdlmp_repro/dynf015.nc')
    #gfsana=Nio.open_file('/glade/u/home/xiasun/scratch/FV3_RT/repo_sat/fv3_gfdlmp_repro/dynf015.nc',"r")

    #tmp2m=fv3["t2m_analysis"][:,:]
    #tmp2m=fv3["TMP_2maboveground"][0,:,:]
    #tmp2mF=(tmp2m-273.15)*9/5+32
    gridlat=postfile["latitude"][:]
    gridlon=postfile["longitude"][:]
    #hgt=fv3["HGT_500mb"][0,:,:]*0.1
    #ugrd=fv3["UGRD_500mb"][0,:,:]
    #vgrd=fv3["VGRD_500mb"][0,:,:]
    #absv=fv3["ABSV_500mb"][0,:,:]*1e5
    #print(ugrd)
    lat=gridlat
    lon=gridlon
    maxlat=lat.max()
    minlat=lat.min()
    maxlon=lon.max()
    minlon=lon.min()
    #print(gridlat)
    #print(absv.shape)

    wks_type = "png"
    wks = Ngl.open_wks(wks_type,"MSLP_2019101400_Barry_"+comp)

    mpres = Ngl.Resources()
    #mpres.mpShapeMode = "FreeAspect"
    #mpres.mpProjection="LambertConformal"#"CylindricalEquidistant"
    #mpres.mpLambertParallel1F = 33.0 #        ; two parallels
    #mpres.mpLambertParallel2F = 45.0
    #mpres.mpLambertMeridianF  = -95.0 #       ; central meridian
    #mpres.vpXF        = 0.00
    #mpres.vpYF        = 0.94
    #mpres.vpWidthF    = 0.42
    #mpres.vpHeightF   = 0.42
    mpres.nglMaximize = False
    mpres.nglFrame     = False
    #gray_index = Ngl.new_color(wks,0.7,0.7,0.7)
    #cyan_index = Ngl.new_color(wks,0.5,0.9,0.9)
    #mpres.mpFillAreaSpecifiers  = ["Water","Land"]
    #mpres.mpSpecifiedFillColors = [cyan_index,gray_index]

    mpres.mpFillOn               = True
    #mpres.mpFillDrawOrder        = "PostDraw"
    mpres.mpGridAndLimbOn = True
    mpres.mpOceanFillColor       = "Transparent"
    mpres.mpLandFillColor        = "Gray90"#"Gray90"
    mpres.mpInlandWaterFillColor = "Transparent"
    #mpres.mpInlandWaterFillColor = "Transparent"
    #mpres.mpLimitMode        = "Corners"
    mpres.mpLimitMode        = "LatLon"
    mpres.mpMaxLonF = -75#maxlon	
    mpres.mpMaxLatF =40#maxlat
    mpres.mpMinLonF = -100#minlon
    mpres.mpMinLatF = 20#minlat
    #mpres.mpLeftCornerlatF =10
    #mpres.mpLeftCornerlonF = -140
    #mpres.mpRightCornerlatF =60
    #mpres.mpRightCornerlonF = -60
    mpres.mpDataBaseVersion     = "MediumRes"
    mpres.mpOutlineBoundarySets = "USStates"
    mpres.mpUSStateLineThicknessF=2 
    mpres.mpGeophysicalLineThicknessF= 2
    mpres.mpCountyLineThicknessF=2
    mpres.mpNationalLineThicknessF=2
    mpres.mpGeophysicalLineColor="black"
    mpres.mpNationalLineColor="black"
    mpres.mpUSStateLineColor="gray60"
    mpres.mpGridLineDashPattern=11
    mpres.mpGridLineColor="grey60"
    #wks1 = Ngl.open_wks(wks_type,"Fast_Sat_F")
    cnres                 = Ngl.Resources()
    #cnres.cnLevelSelectionMode="ExplicitLevels"# Contour resources
    #cnres.cnFillColors=["Transparent","(/1.,.9607843,.8/)","(/1,0.9019608,0.4392157/)","(/1,.8,.2/)","(/1.,0.6862745,0.2/)","(/1.,0.6,0.2/)","(/1.,0.43529412,0.2, /)","(/1.,0.33333334,0./)","(/0.9019608,0.15686275,0.11764706/)","(/0.78431374,0.11764706,0.07843138/)"]
    #cnres.cnLevels    = [9,12,15,18,21,24,27,30]
    cnres.wkColorMap="WhiteBlueGreenYellowRed" #"cmap"
    #Ngl.set_values(wks,cnres)
    #cmap = Ngl.retrieve_colormap(wks)
    #print(cmap)
    cnres.cnFillOn        = True
    #cnres.cnFillPalette   = cmap#"sunshine_9lev"#"temp"#"NCV_bright_white"#"matlab_jet"#"BlueYellowRed" #"sunshine_9lev"#""#BlueYellowRed"      # New in PyNGL 1.5.0

    cnres.cnLinesOn       = False
    cnres.cnLineLabelsOn  = False
    #cnres.cnLevelSelectionMode = "ManualLevels"

    #cnres.cnMinLevelValF = 6#-45
    #cnres.cnMaxLevelValF = 28#55
    #cnres.cnLevelSpacingF = 2
    #cnres.cnFillColors=["Transparent"]
    #cnres.cnLevelSpacingF=(cbarmax-0)/10
    #cnres.nglMaximize = True
    #cnres.nglDraw     = False
    cnres.nglFrame    = False
    # Labelbar resource
    #cnres.trYMaxF = 25
    cnres.tiXAxisString = "Lon"
    cnres.tiYAxisString = "Lat"

    cnres.lbOrientation   = "horizontal"
    cnres.lbTitleString = "kts"
    cnres.lbTitlePosition="Bottom"
    cnres.lbTitleFontHeightF="0.015"
    # Scalar field resources
    cnres.sfXArray        = lon[:]
    cnres.sfYArray        = lat[:]
    # Map resources
    #cnres.mpProjection   =  "LambertConformal"
    #cnres.mpFillOn               = False
    #cnres.mpFillDrawOrder        = "PostDraw"
    #cnres.mpGridAndLimbOn = False
    #cnres.mpLandFillColor        = "Transparent"
    #cnres.mpOceanFillColor       = "Transparent"
    #cnres.mpInlandWaterFillColor = "Transparent"
    #cnres.mpLimitMode        = "LatLon"
    #cnres.mpMaxLonF = -66.9513812#maxlon	
    #cnres.mpMaxLatF = 49.3457868#maxlat
    #cnres.mpMinLonF = -124.7844079#minlon
    #cnres.mpMinLatF = 24.7433915#minlat
    #cnres.mpLeftCornerlatF =30
    #cnres.mpLeftCornerlonF = -120
    #cnres.mpRightCornerlatF =50
    #cnres.mpRightCornerlonF = -110
    #cnres.mpDataBaseVersion     = "MediumRes"
    #cnres.mpOutlineBoundarySets = "USStates"#AllBoundaries"#USStates"#"AllBoundaries"
    cnres0=cnres
    cnres0.lbLabelFontHeightF = 0.012
    cnres0.pmLabelBarHeightF =0.1
    cnres0.pmLabelBarWidthF=0.6
    cnres0.cnFillPalette="WhiteBlueGreenYellowRed"
    cnres0.cnLevelSelectionMode = "ManualLevels"
    cnres0.cnMinLevelValF = 20#30
    cnres0.cnMaxLevelValF = 45
    #mapres=cnres
    mpres.tiMainString = "ufsv1.0.0_ccpp("+comp+"): MSLP (hPa) and 10-m wind (knots)  ~C~Initialized: 0000Z 11 Jul 2019 | Valid: 0000Z 14 Jul 2019"#"{} ({}) at {:.2f} hPa with fast_sat".format(clwmr.long_name,clwmr.units,vpfull)
    mpres.tiMainFontHeightF=0.012
    mpres.tiMainPosition = "Center"
    #mpres.tiMainJust="topleft"
    #contour = Ngl.contour_map(wks,absv[:,:],cnres0)

    cnres1= Ngl.Resources()
    cnres1.nglDraw=False
    cnres1.nglFrame    = False
    cnres1.cnFillOn    = True
    cnres1.cnLinesOn = True
    cnres1.sfXArray        = lon[:]
    cnres1.sfYArray        = lat[:]
    cnres1.cnLineThicknessF = 3.0
    cnres1.cnFillPalette="WhiteBlueGreenYellowRed"
    cnres1.cnLevelSelectionMode = "ManualLevels"
    cnres1.cnMinLevelValF = 996#-45
    cnres1.cnMaxLevelValF = 1024
    cnres1.cnLevelSpacingF=2
    cnres1.cnInfoLabelOn   = False

    cnres1.cnLineLabelBackgroundColor= "white"#"Transparent" 
    cnres1.cnLineLabelDensityF=1.5
    #cnres1.cnLineLabelPlacementMode = "computed"
    cnres1.cnLineLabelFontHeightF=0.008
    #cnres1.cnConstFLabelFontHeightF
    #cnLineLabe
    #cnres1.cnMinLevelValF = 6#-45
    #cnres1.cnMaxLevelValF = 28#55
    #cnres1=cnres
    #cnres1.tiMainString = "{} ({}) at {:.2f} hPa with no fast_sat".format(clwmr.long_name,clwmr.units,vpfull)

    #cnres1.tiMainString = "Temperature at"+npfull+" Layer with no fast_sat"
    #contour1 = Ngl.contour_map(wks1,noclwmr[:,:],cnres1)
    #mpres = Ngl.Resources()
    #mpres.mpShapeMode = "FreeAspect"
    #mpres.vpXF        = 0.06
    #mpres.vpYF        = 0.94
    #mpres.vpWidthF    = 0.42
    #mpres.vpHeightF   = 0.42

    #mpres.nglFrame     = False
    #gray_index = Ngl.new_color(wks,0.7,0.7,0.7)
    #cyan_index = Ngl.new_color(wks,0.5,0.9,0.9)
    #mpres.mpFillAreaSpecifiers  = ["Water","Land"]
    #mpres.mpSpecifiedFillColors = [cyan_index,gray_index]

    #mpres.mpFillOn               = False
    #cnres.mpFillDrawOrder        = "PostDraw"
    #mpres.mpGridAndLimbOn = False
    #mpres.mpOceanFillColor       = "Transparent"
    #mpres.mpLandFillColor        = "Transparent"
    #mpres.mpInlandWaterFillColor = "Transparent"
    #mpres.mpLimitMode        = "LatLon"
    #mpres.mpMaxLonF = -66.9513812#maxlon	
    #mpres.mpMaxLatF = 49.3457868#maxlat
    #mpres.mpMinLonF = -124.7844079#minlon
    #mpres.mpMinLatF = 24.7433915#minlat
    #cnres.mpLeftCornerlatF =30
    #cnres.mpLeftCornerlonF = -120
    #cnres.mpRightCornerlatF =50
    #cnres.mpRightCornerlonF = -110
    #mpres.mpDataBaseVersion     = "MediumRes"
    #mpres.mpOutlineBoundarySets = "USStates"


    #map=Ngl.map(wks,res=mpres)
    resources= cnres
    resources.nglDraw     = False
    resources.nglFrame    = False
    resources.vcMinFracLengthF = 1
    resources.vcRefMagnitudeF  =10
    resources.vcRefLengthF     = 0.025
    resources.vcMinDistanceF = 0.025
    resources.vcMonoLineArrowColor  = True   # Draw vectors in color.
    resources.vfXArray=lon[:]
    resources.vfYArray=lat[:]
    resources.vcGlyphStyle = "WindBarb"
    #vc = Ngl.vector_map(wks,ugrd,vgrd,resources)
    map=Ngl.map(wks,mpres)
    #pabsv=Ngl.contour(wks,sfcws[:,:],cnres0)
    pwb=Ngl.vector(wks,sfugrd,sfvgrd,resources)
    phgt=Ngl.contour(wks,mslp[:,:],cnres1)
    #Ngl.overlay(map,pabsv)
    Ngl.overlay(map,phgt)
    Ngl.overlay(map,pwb)
    Ngl.draw(map)
    #Ngl.wmsetp("col",2)
    #Ngl.wmsetp("wbs",.2)
    #Ngl.wmbarbmap(wks,lat[:],lon[:],ugrd[:,:],vgrd[:,:])
    Ngl.frame(wks)
    #cmap = Ngl.retrieve_colormap(wks)

    #del resources
    Ngl.end()

.. rst-class:: sphx-glr-timing

   **Total running time of the script:** ( 0 minutes  0.000 seconds)


.. _sphx_glr_download_auto_examples_MSLP_WIND_Barry.py:


.. only :: html

 .. container:: sphx-glr-footer
    :class: sphx-glr-footer-example



  .. container:: sphx-glr-download sphx-glr-download-python

     :download:`Download Python source code: MSLP_WIND_Barry.py <MSLP_WIND_Barry.py>`



  .. container:: sphx-glr-download sphx-glr-download-jupyter

     :download:`Download Jupyter notebook: MSLP_WIND_Barry.ipynb <MSLP_WIND_Barry.ipynb>`


.. only:: html

 .. rst-class:: sphx-glr-signature

    `Gallery generated by Sphinx-Gallery <https://sphinx-gallery.github.io>`_
