# **InSAR geodesy**

InSAR (Interferometric Synthetic Aperture Radar) has revolutionized volcanology providing dense geodetic observations (up to ~0.5 m/pixel, most likely 10-30 m/pixel), albeit with a poor temporal sampling (1-42 days depending on the SAR platform). One of the major limitations of the method is the presence of atmospheric signals produced by water vapor and pressure changes that are correlated with the topography. In the case of stratovolcanoes, these signals mimic ground deformation produced by magma reservoir pressurization, and can be very challenging to mitigate for the time scales of volcanic eruptions (0.01 - 10 days). I'm interested in developing and comparing approaches that can reduce the effect of these artifacts.

On the other hand, volcano deformation is recorded over spatial scales that vary between a few tens of meters to hundreds of kilometers, produced by conduit pressurisation or very shallow sources to lower crustal intrusions. Ice covered volcanoes such as those in the Southern Andes are likely to pressurise only near the volcano summit, in areas where instrument deployments are very difficult due to harsh environmental conditions. These signals require specific acquisition plans to be potentially detectable by InSAR, hence I am also interested on using the complete civilian SAR constellation (TerraSAR-X/TanDEM-X, COSMO-SkyMED, RADARSAT-2, Sentinel-1A/B and ALOS-2) and the unique characteristics of each satellite to better understand volcanic processes over a wide range of spatio-temporal scales.  

<img style="float: center;" src="/images/villarrica_coherence.png">

Examples of 1-day CSK (COSMO-SkyMED) and 2-days UAVSAR interferograms at Villarrica volcano. The labels show the season, repeat period and acquisition dates. All the interferograms are wrapped and only a and b are filtered. Dashed black lines are the swaths of TerraSAR-X spotlight data. The figure shows that with the current SAR platforms it is not possile to sustain coherence in the summit of heavily glaciated but restless volcanoes. Only UAVSAR data is coherent but this platform is not used for permanent overflights. This currently hampers the use of InSAR to study of conduit pressurization produced by either stick-slip of solid plugs of andesitic magma or by gas slugs during strombolian eruptions because these signals are likely to be detected only with measurement acquired less than a few hundred meters from the eruptive vents.

<img style="float: center;" src="/images/villarrica_eraI.png">


Comparison of methods to correct atmospheric phase delays in ALOS-1 and CSK interferograms at Llaima (a-b only) and Villarrica volcanoes for ALOS-1 (a-b) and COSMO-SkyMED (c). The analysis shows that low-resolution global atmospheric models such as ERA-I do not significantly reduce the atmospheric noise variance compared with simple empirical techniques like a ramp with an elevation dependent term. This significantly hampers the detection of small-amplitude, transient signals in stratovolcanoes that are correlated with the spatial wavelengths of topography correlated atmospheric noise.

<img style="float: center;" src="/images/caulle_cor.jpg">


Coherence comparison for interferograms with 24 and 48 day repeat periods at Cordon Caulle volcano. The data sets are a low resolution wide swath mode (Sentinel-1 Terrain Observation by Progressive Scans, 20 m/pixel) with VV polarization and a high resolution strip map beam (RADARSAT-2 Wide Ultra Fine 12, 2 m/pixel) with HH polarization. The RADARSAT-2 coherence ​is much higher than the Sentinel-1 coherence due to a combination of the higher resolution and the HH polarization. 

<img style="float: center;" src="/images/ambrym.png">

Comparison of X, C and L band data of the 2018 Ambrym dike intrusion and submarine eruption. The coherence of Sentinel-1 data during the eruption is almost zero due to the 2 m of line-of-sight displacement exceeding the deformation gradient of 2pi radians per pixel required to sustain coherence. Therefore L-band data provides the best deformation measurements from InSAR due to its longer wavelength and smaller pixel size. However, the L-band azimuth offsets are corrupted by dispersive ionospheric streaks while azimuth offsets calculated from high resolution stripmap X-band data (2 m/pixel) are not affected by these effects due to their smaller wavelength and nicely show the along-track displacement resulting from the dike opening. The conclusion is that complex eruptions under difficult environmental conditions like tropical rainforest require to use multiplatform SAR data. Data from [Tara Shreve's excellent paper](https://www.nature.com/articles/s41598-019-55141-7) on this outstanding event.



<img style="float: center;" src="/images/pichilemu_wr.jpg" width="500">

Comparison of ALOS-1 L-band and ENVISAT C-band data of the Mw 7.0 2011 Pichilemu earthquake in Central Chile. The difference in the number of fringes is given by the longer wavelength of L-band data compared with C-band data. The patchy pattern at the bottom of the ENVISAT interferogram is produced by DEM errors by forest clearcuts in this long baseline interferogram (Bp ~ 390 m). In contrast, these DEM errors are absent in the ALOS-1 interferogram which a strict small baseline  pair. Also, C-band data tends to saturate near the fault trace due to high deformation gradients which are better captured by data with lower sensitivity like L-band data. C and L-band data can be considered analogous to a seismometer and a strong motion in earthquake seismology! And of course, in vegetated areas the coherence of C-band data is much lower compared to that of L-band data. But L-band data show dispersive signals like ionospheric streaks which are almost completely absent in C-band data. So each InSAR data has its unique capabilities and disadvantages and its crucial to understand them for a better use of the radar technology. 


### **Relevant publications**

[A global assessment of SAOCOM-1 L-band stripmap data for InSAR characterization of volcanic, tectonic, cryospheric, and anthropogenic deformation.](https://ieeexplore.ieee.org/document/10586971)<br>
**Delgado, F.**, Shreve, T., Borgstrom, S., León-Ibañez, P., Castillo, J., Poland, M.,**2024** IEEE Transactions on Geoscience and Remote Sensing, doi:10.1109/TGRS.2024.3423792.

[The utility of TerraSAR-X, TanDEM-X, and PAZ for studying global volcanic activity: Successes, challenges, and future prospects.](https://www.jvolcanica.org/ojs/index.php/volcanica/article/view/245/)<br>
Galetto, F., Dualeh, E., **Delgado, F.**, Pritchard, M., Poland, M., Ebmeier, S., Shreve, T., Biggs, J., Hamling, I., Wauthier, C., Gonzalez Santana, J., Froger, J.-L., Bemelmans, M. Volcanica, **2024**, 7(1), 273–301. doi: 10.30909/vol.07.01.273301.

[Rhyolitic volcano dynamics in the Southern Andes: contributions from 17 years of InSAR observations at Cordon Caulle since 2003 to 2020.](https://www.sciencedirect.com/science/article/abs/pii/S0895981120303849)<br>
**Delgado, F.**.  <i>Journal of South American Earth Sciences </i>, special issue on <i>New advances on SAR Interferometry in South America</i>. **2020**, doi:10.1016/j.jsames.2020.102841

[Recent unrest (2003-2015) imaged by space geodesy at the highest risk Chilean volcanoes:  Llaima, Villarrica and Calbuco (Southern Andes)](https://www.sciencedirect.com/science/article/pii/S0377027317303086)<br>
**Delgado, F.**, Pritchard, M.,  Ebmeier, S., Gonzalez, P., Lara, L. <i>Journal of Volcanology and Geothermal Research</i>. **2017**, doi:10.1016/j.jvolgeores.2017.05.020. Special issue of <i>"Volcano Geodesy: Recent developments and future challenges"</i>.
