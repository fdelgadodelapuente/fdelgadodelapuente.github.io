Here I have compiled a set of Linux and OSX installations instructions for ISCE and some data sets of earthquakes and volcanoes from the Alaska Satellite Facility .
 
Ubuntu Installation

The notes in this website are from instructions by Piyush Agram (JPL), one of the developers of the ISCE software: Installation of ISCE and https://github.com/piyushrpt/oldLinuxSetup. The instructions presented below were tested for the isce_201609 version, but have been used with the most recent versions of the software in an Ubuntu machine. If you use other Linux distributions like RedHat or openSUSE, it's likely that you will have to modify these instructions. 

Additional instructions for Linux machines with little to none sudo permissions (Whyjay Zheng, Cornell University).

Other instructions (Scott Henderson, University of Washington)

STEP 1: update Python2.7 

ISCE is compiled with scons, a Python2.7 application. You have scons installed if you type
which scons
scons -h
and the outputs do not display errors
If you do not have scons, download miniconda2, update the libraries and install scons 
 
/home/francisco/miniconda2/bin/conda update --all
/home/francisco/miniconda2/bin/conda install scons
 
Now type again the scons commands. If it doesn't work, close the terminal, open another window and try again. As far as I understand, the last version of ISCE supports scons for python3.
 
STEP 2: update Python3

ISCE is written in Python3 and uses a lot of its libraries. To install them all you need to install anaconda3 and then type
 
/home/francisco/anaconda3/bin/conda config --add channels conda-forge
/home/francisco/anaconda3/bin/conda update --all
/home/francisco/anaconda3/bin/conda install gdal
/home/francisco/anaconda3/bin/conda install libgdal
/home/francisco/anaconda3/bin/conda install -c omnia fftw3f=3.3.4
 
Now open a python3 window and type
 
import scipy
import numpy
import matplotlib.pyplot as plt
import h5py
from osgeo import gdal
 
If they are correctly installed, you should see no errors.
 
The steps in https://github.com/piyushrpt/oldLinuxSetup/blob/master/anaconda.md for installing anaconda are slightly different because they state that you should update the libraries before installing gdal. I've noticed that sometimes the installation is just fine if you do it the way I posted above. If anaconda failed to install the libraries, delete the folder and reinstall from scratch

The range split spectrum method for ionospheric correction uses cython
conda install cython
ln -sf /home/fjd49/anaconda3/bin/cython /home/fjd49/anaconda3/bin/cython3

If you don't have the cython3 soft link, the split spectrum module will not be installed

STEP 3: create the SConfigISCE file
 
This is the tricky part, that ISCE can actually find all the installed libraries. You need to create a file called SConfigISCE in the folder above ISCE which specifies the libraries paths. 
 
If you are starting from a raw ubuntu installation, you will need to install a few extra libraries, including the OpenMotif library for the MDX interferogram viewer. To do so, just type in the terminal
sudo apt-get install libx11-dev libxm4 libmotif-dev libfftw3f-dev gfortran
If your system doesn't find the the fftw3 library, get it from this link
 
For the 2.2 version you also need openCV2 for stripmapApp.py
conda install opencv
However, this will downgrade gdal, which you must then update with
conda update gdal

STEP 4: Install ISCE

cd to the ISCE folder and then type in the terminal
SCONS_CONFIG_DIR=/home/francisco scons install
with /home/francisco the path of the SCONS_CONFIG file
The ISCE compilation will output thousands of warnings, they are ok, so don't be scared. Once you've succeed to compile the software, you need to add ISCE to your bash profile. If the installation fails due to missing libraries, type

rm -rf config.log .sconfig.dblite .sconf_temp

and then restart

STEP 5: source ISCE
 
Create and modify a bash file with the name isce1807.sh. Then type 
 
chmod 777 isce1708.sh
source isce1708.sh
 
This ends the ISCE installation
 
STEP 6: run ISCE
 
You should see a bunch of outputs with no error messages when you type 

insarApp.py --steps --help (stripmap processor with motion compensated geometry, works for all raw data, doesn't work well for zero Doppler data)
topsApp.py --steps --help (Sentinel-1 IW TOPS processor)
stripmapApp.py --steps --help (stripmap processor with geometry based coregistration, handles both raw and zero Doppler data)

STEP 7: get SRTM access
 
ISCE uses the SRTM DEM (the best free DEM available for InSAR processing, much better than the ASTER GDEM). You need to get a NASA account at urs.earthdata.nasa.gov (free).

First, cd $HOME
Then, create a file named .netrc with the following 3 lines 
 
machine urs.earthdata.nasa.gov
login your_earthdata_login_name
password your_earthdata_password 

Change .netrc permissions with chmod 600 ~/.netrc 

OSX Installation

For installing ISCE on OSX I suggest strongly suggest you to stick to a single package manager (either macports, brew or conda). Otherwise you might find conflicting issues due to the different versions of the installed libraries.

Instructions for MacPorts (Piyush Agram, JPL) 
Instructions for OSX 10.14 Mojave (adapted by me from those by Piyush Agram)
Instructions for Homebrew (Jose Uribe, CECS, Chile). 
Instructions for Homebrew and Docker (Scott Henderson, U of Washington)
SCONS_CONFIG file (tested with High Sierra and Mojave)
Troubleshooting (a common issue with OSX): isce 2.2 on OSX High Sierra

Issues with unbinded Python libraries: If the Python libraries are correctly installed with macports, but Python cannot import them because you mixed package managers, just run the following line

export PYTHONPATH=/opt/local/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages:$PYTHONPATH

This issue might happen if you installed libraries with both conda and macports, but then you removed conda like I did once, resulting in a complete mess.

STEP 8: process interferograms! 

Software manual by me and with of references to online resources

Sentinel-1 C band ascending interferogram of the VEI 4 2015 Calbuco volcano eruption (topsApp.py control file, orbits and Sentinel-1 calibration files)

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SDV_20150426T234151_20150426T234227_005661_007430_AFBE.zip

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20150414T234157_20150414T234224_005486_007013_5C44.zip

Interferograms of the June 2007 Kilauea volcano Father's Day dike intrusion
ENVISAT C band ascending

https://eo-virtual-archive4.esa.int/supersites/ASA_IM__0CNPDK20070621_082536_000000172059_00136_27745_3245.N1

https://eo-virtual-archive4.esa.int/supersites/ASA_IM__0CNPDK20070412_082532_000000162057_00136_26743_2801.N1

https://eo-virtual-archive4.esa.int/supersites/ASA_IM__0CNPDK20070618_081954_000000162059_00093_27702_3230.N1

https://eo-virtual-archive4.esa.int/supersites/ASA_IM__0CNPDK20070514_081953_000000172058_00093_27201_3022.N1

ALOS-1 L band ascending

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP068020370-L1.0.zip

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP074730370-L1.0.zip
ALOS-1 L band descending

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP058463230-L1.0.zip

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP078593230-L1.0.zip

ENVISAT C-band ascending interferogram of the 2008 Okmok eruption

https://eo-virtual-archive4.esa.int/supersites/ASA_IM__0CNPDK20080627_084349_000000172069_00451_33070_6667.N1

https://eo-virtual-archive4.esa.int/supersites/ASA_IM__0CNPDK20080801_084350_000000162070_00451_33571_6940.N1

ALOS-1 L band ascending interferogram (2 frames) of the March 2010 Mw 6.9 Pichilemu earthquake

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP219546490-L1.0.zip

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP219546480-L1.0.zip

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP226256490-L1.0.zip

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP226256480-L1.0.zip

ALOS-1 L band ascending interferogram of the inflating Laguna del Maule rhyolitic field

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP163386450-L1.0.zip

https://datapool.asf.alaska.edu/L1.0/A3/ALPSRP056026450-L1.0.zip

Sentinel-1C band interferogram (3 frames) of the December 2016 Mw 7.6 Chiloe earthquake
Ascending interferogram

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20170114T234913_20170114T234940_014834_0182E3_33D4.zip

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20170114T234938_20170114T235005_014834_0182E3_75E4.zip

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20170114T235003_20170114T235030_014834_0182E3_D27E.zip

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20161221T235005_20161221T235032_014484_017826_F82F.zip

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20161221T234940_20161221T235007_014484_017826_9FE1.zip

https://datapool.asf.alaska.edu/SLC/SA/S1A_IW_SLC__1SSV_20161221T234915_20161221T234942_014484_017826_BA92.zip
 
Descending interferogram 3 frames

https://datapool.asf.alaska.edu/SLC/SB/S1B_IW_SLC__1SDV_20161217T095718_20161217T095744_003434_005DE5_9E53.zip

https://datapool.asf.alaska.edu/SLC/SB/S1B_IW_SLC__1SDV_20161217T095742_20161217T095809_003434_005DE5_88FB.zip

https://datapool.asf.alaska.edu/SLC/SB/S1B_IW_SLC__1SDV_20161217T095807_20161217T095834_003434_005DE5_F6FB.zip

https://datapool.asf.alaska.edu/SLC/SB/S1B_IW_SLC__1SDV_20170110T095716_20170110T095743_003784_00681B_FBFF.zip

https://datapool.asf.alaska.edu/SLC/SB/S1B_IW_SLC__1SDV_20170110T095740_20170110T095807_003784_00681B_49B8.zip

https://datapool.asf.alaska.edu/SLC/SB/S1B_IW_SLC__1SDV_20170110T095805_20170110T095832_003784_00681B_59B8.zip

stripmapApp.py zero doppler SLC data control files for RADARSAT-2, TerraSAR-X (stripmap and spotlight), ALOS-2 stripmap and COSMO-SkyMED (stripmap and spotlight) 

insarApp.py: stripmap processor with motion compensated geometry for raw data (ENVISAT, ALOS-1, COSMO-SkyMED)
topsApp.py: TOPS processor with geometric coregistration for Sentinel-1 data
stripmapApp.py: processor with geometric coregistration for raw (ENVISAT, ALOS-1, COSMO-SkyMED) and zero doppler data (COSMO-SkyMED SLC stripmap and spotlight, RADARSAT-2, TerraSAR-X stripmap and spotlight, ALOS-2 stripmap)

Files for processing the Sentinel-1 Calbuco, ENVISAT KIlauea, ALOS-1 Kilauea, CSK Kilauea, ALOS-1 Pichilemu, Sentinel-1 Chiloe and ALOS-1 Laguna del Maule data sets. This files include orbits  (ENVISAT and Sentinel), instrument files (ENVISAT), calibration files (Sentinel) and ISCE control files

CSK Kilauea 2018

InSAR time series Matlab example


SNAP Instructions
 
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
