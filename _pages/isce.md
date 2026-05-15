---
layout: archive
title: "ISCE"
excerpt: "ISCE"
author_profile: true
permalink: /isce/

---
## **ISCE tutorials**

[ISCE tutorial](https://www.overleaf.com/read/shtkqpdjpghj) that I wrote for teaching students. It's mostly my troubleshooting notes over the years, but adapted into a Latex document. [Compiled PDF May 2026](https://drive.google.com/file/d/1FA_27gILYAF5t1hpepLDLlz37MBaL2bs/view?usp=share_link).

[TOPS Stack Processor and MintPy tutorial](https://www.overleaf.com/project/69fc94aeb1a36bc853a58932). Example for the Salar de Atacama Basin.


### Software

[SAOCOM-1 parser for stripmap stack processor, ALOS-4 parser for stripmapApp and stripmap stack processor ](https://github.com/isce-framework/isce2/pull/982).

[FilterAndCoherence.py](https://github.com/fdelgadodelapuente/isce_utils/blob/main/FilterAndCoherence.py) for applying the layover mask to interferograms generated with the stripmap stack processor.

[MATLAB/Python/C shell](https://github.com/fdelgadodelapuente/isce_utils) scripts for loading data, masking, removing ramps and exporting the data to GMT grids.

[TanDEM-X CoSSC processor](https://github.com/fdelgadodelapuente/tandemx). Clunky code to generate bistatic interferograms. Install the following files in the stripmap stack processor folder: tandemxApp.csh, unpackFrame_TDX.py, rangePix.py, bigeo2rdr.py

