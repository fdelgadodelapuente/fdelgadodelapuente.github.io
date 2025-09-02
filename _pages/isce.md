---
layout: archive
title: "ISCE"
excerpt: "ISCE"
author_profile: true
permalink: /isce/

---
## **ISCE tutorial and add-ons**

[ISCE tutorial](https://www.overleaf.com/read/shtkqpdjpghj) that I wrote for teaching students. It's mostly my troubleshooting notes over the years, but adapted into a Latex document. [Compiled PDF](https://drive.google.com/file/d/1NP5WWYWWy6d_O2iIM6Ln1fZCcuVeNwig/view?usp=sharing).

[SAOCOM-1 parser for stripmap stack processor, ALOS-4 parser for stripmapApp and stripmap stack processor ](https://github.com/isce-framework/isce2/pull/982).

FilterAndCoherenceStackLayover.py for applying the layover mask to interferograms generated with the stripmap stack processor

TanDEM-X CoSSC processor: clunky code to generate bistatic interferograms. The following must be dumped in the stripmap stack processor folder: [tandemxApp.csh](https://github.com/fdelgadodelapuente/tandemx/blob/main/tandemxApp.csh), [unpackFrame_TDX.py](https://github.com/fdelgadodelapuente/tandemx/blob/main/unpackFrame_TDX.py), [rangePix.py](https://github.com/fdelgadodelapuente/tandemx/blob/main/rangePix.py), bigeo2rdr.py

