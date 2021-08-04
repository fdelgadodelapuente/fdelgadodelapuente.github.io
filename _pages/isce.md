---
layout: archive
title: "ISCE"
excerpt: "ISCE"
author_profile: true
permalink: /isce/

---
## **ISCE tutorial**


## **SNAP Instructions**
 
SNAP is the Sentinel Toolbox software from ESA. SNAP biggest advantage with respect to the Linux based software like ISCE is that it has a GUI, so it is very easy to get acquainted with the InSAR processing, particularly for InSAR newbies. The Sentinel-1 TOPS processing is very straightforward with SNAP. However, it doesn't replace a terminal-based software like ISCE for serious scientific applications.

Tutorial from ASF for the Calbuco Sentine-1 ascending interferogram 

1. Radar -> Coregistration -> S-1 TOPS Coregistration 

2. TOPSAR-Split -> select the IW1 subswath for each of the products
Select bursts 1-3 for 150414 SLC and bursts 4-6 for 150426 SLC
Apply-Orbit-File -> Sentinel Precise Orbit State Vectors

3. Radar > Interferometric > Products ->  Interferogram Formation 
Use _orb_stack product 
 
4. Radar > Sentinel-1 TOPS -> S-1 TOPS Deburst
Use _orb_stack_ifg product 

5. Radar > Interferometric > Products -> Topographic Phase Removal
Use _orb_stack_ifg_deb product 

6. Radar -> Multilooking
Processing  parameters, Number of Range Looks, 10 looks o 20 
Always use GR Square Pixel
Interferograms with short temporal baselines can be processed with 10 looks, and those that are noisier should have a larger number of looks
Use _orb_stack_ifg_deb_dinsar product 

7. Radar > Interferometric > Filtering ->Goldstein Phase Filtering
Porcessing Paramenters, Adaptative Filter Exponent, 0.5
Use _orb_stack_ifg_deb_dinsar_ML product 
 
8. Radar > Geometric > Terrain Correction -> Range-Doppler Terrain Correction (Intensity and Phase)
Use _orb_stack_ifg_deb_dinsar_ML_flt product 
