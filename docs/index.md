<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#org6f86cea">1. Overview</a>
<ul>
<li><a href="#orgc823fce">What is FlowAnalyzer?</a></li>
<li><a href="#orge78f9b2">Why to use Optical Flow Analysis?</a></li>
<li><a href="#org91b0e32">How does Optical Flow Analysis work?</a></li>
<li><a href="#org737bc00">Regions of interest and disinterest</a></li>
<li><a href="#org7454bd0">Computing Motion Signals</a></li>
</ul>
</li>
<li><a href="#orgc1fbbb6">2. Installation</a>
<ul>
<li><a href="#org0d9c2e3">Standalone application (Mac OS only)</a></li>
<li><a href="#org1eda3db">General method (Linux, Mac, Windows)</a>
<ul>
<li><a href="#orga7035dc">Download FlowAnalyzer</a></li>
<li><a href="#orgf2eae96">Install Python</a></li>
<li><a href="#org3db9129">Install the required Python libraries</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#orgebaa8c2">3. Quick Start Guide</a>
<ul>
<li><a href="#org50ab5b9">Running FlowAnalyzer</a></li>
</ul>
</li>
<li><a href="#orge21def6">4. Auxiliary tools</a></li>
</ul>
</div>
</div>


<a id="org6f86cea"></a>

# Overview


<a id="orgc823fce"></a>

## What is FlowAnalyzer?

-   FlowAnalyzer is a piece of software, based on Optical Flow Analysis (OFA), for extracting motion from 2D video sequences

-   Optical Flow Analysis (OFA) is a quantitative method for measuring motion from video. It is based on a computer vision algorithm known as Optical Flow

-   As an example, consider [this video](./media/metronome/metronome_320x240_30fps_h264.mov) of a metronome. When submitted to Optical Flow Analysis, it produces the following motion signal:

![img](./media/metronome/metronome_320x240_30fps_h264_frames_8050_16100_zoom.png)


<a id="orge78f9b2"></a>

## Why to use Optical Flow Analysis?

-   Non-invasive (measurement does not interfere with the speech production process)
-   Portable (data acquisition can take place out of the lab)
-   Automated
-   Fast
-   Objective


<a id="org91b0e32"></a>

## How does Optical Flow Analysis work?

-   Optical flow computes pixel displacements between consecutive frames in the video

-   All pixel displacements are represented and stored as velocity vectors
    -   x and y components (cartesian coordinates)
    -   magnitude and direction (polar coordinates)

-   The array of velocity vectors comprises the optical flow field

-   Flow fields can be visualized in at least two different ways:
    -   we can overlay the velocity vectors directly on the input video, as shown in this [example](./media/videos/benoit-7_h264.mov)
    
    -   alternatively, we can discard the vectors' directions and visualize their amplitudes as brightness. We call this a flow video, as shown [here](./media/videos/KatieTest_whole_flow-11_small.mov)


<a id="org737bc00"></a>

## Regions of interest and disinterest

-   Rectangular regions of interest (ROIs) and disinterest (RODs) can be defined

-   All velocity vectors within each region of interest are combined into a single measure

-   Motion within regions of disinterest is ignored

-   By combining regions of interest and disinterest, it’s possible to create non-rectangular regions of interest, as shown below

![img](./media/pictures/baby_regions.png)


<a id="org7454bd0"></a>

## Computing Motion Signals

-   All velocity vectors inside each region of interest are summed for each frame in the video

-   This creates horizontal, vertical and magnitude motion signals as a function of time

![img](./media/pictures/100002010000041800000122C009BAB3A4FAD015.png)


<a id="orgc1fbbb6"></a>

# Installation


<a id="org0d9c2e3"></a>

## Standalone application (Mac OS only)

There is a DMG installation file for Mac OSX available [here](./builds/MacOS/FlowAnalyzer.dmg). Note, however, that this only installs the FlowAnalyzer GUI. Auxiliary scripts (such as for batch processing, creating flow movies, etc) won't be installed in this case.


<a id="org1eda3db"></a>

## General method (Linux, Mac, Windows)


<a id="orga7035dc"></a>

### Download FlowAnalyzer

First, download the FlowAnalyzer software from [here](./optical_flow.zip).


<a id="orgf2eae96"></a>

### Install Python

FlowAnalyzer is written in Python. In order to run it, you need to have Python 2.7 and all the required libraries installed on your computer. The easiest way to achieve this (at least on Windows and Mac OSX) is by using [miniconda](http://conda.pydata.org/miniconda.html). Installation files and instructions can be found [here](http://conda.pydata.org/miniconda.html) and [here](http://conda.pydata.org/docs/install/quick.html), respectively. **Important:** make sure you install miniconda for Python 2.7, not Python 3.x.


<a id="org3db9129"></a>

### Install the required Python libraries

Now, you need to install the required Python libraries. In order to do that, issue the commands below in a terminal window.

Mac OSX:

    conda upgrade --all
    conda install matplotlib=1.3.1 pytables=3.0.0 pillow=2.7.0 pyqt=5.6.0 opencv=2.4.8 xlrd=1.0.0 xlwt=1.1.2

Windows:

    conda upgrade --all
    conda install matplotlib=1.5.3 pytables=3.3.0 pillow=3.4.2 pyqt=5.6.0 xlrd=1.0.0 xlwt=1.1.2

On Windows, the OpenCV packages available from miniconda can't handle videos, what makes them useless for our purposes. However, the OpenCV packages available from [Christoph Gohlke's page](http://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv) work fine. Go to his page and download version 2.4.x (not 3.x) of the OpenCV package for your architecture (32 or 64 bits). As a convenience, these packages are also available from [here](./opencv/opencv_python-2.4.13.2-cp27-cp27m-win32.whl) (32 bits) and [here](./opencv/opencv_python-2.4.13.2-cp27-cp27m-win_amd64.whl) (64 bits). After downloading the appropriate file, install it using the pip command:

    pip install file_name

where file\_name is the name of the downloaded file (with a .whl extension). 

If you use Linux, you probably don't need miniconda, as the required libraries are likely available through your distribution's package manager (although you can still use miniconda if you want). For example, in Debian/Ubuntu the required libraries can be installed with the following command:

    sudo apt-get install python-matplotlib python-tables python-imaging python-xlrd python-xlwt python-pyqt5 python-opencv

Finally, you need the py-notify module, which only seems to be available through [pip](http://pypi.python.org). In order to install py-notify through pip, issue the following command in a terminal window:

    pip install py-notify

If the command above fails (for example, because you don't have a C compiler installed &#x2013; something quite common on Windows and Mac OSX), you can use the pre-compiled binaries below:

-   Linux ([32 bits](./py-notify/py-notify-linux-32bit-py2.7.zip), [64 bits](./py-notify/py-notify-linux-64bit-py2.7.zip))
-   Windows ([32 bits](./py-notify/py-notify-win-32bit-py2.7.zip), [64 bits](./py-notify/py-notify-win-64bit-py2.7.zip))
-   Mac OSX ([64 bits](./py-notify/py-notify-macosx-64bit-py2.7.zip))

Download the appropriate file for your architecture and uncompress it in the same folder where the FlowAnalyzer.py script is located, or put it somewhere in your Python path.


<a id="orgebaa8c2"></a>

# Quick Start Guide


<a id="org50ab5b9"></a>

## Running FlowAnalyzer

Unzip the optical\_flow.zip archive downloaded in the previous section, enter the created folder (optical\_flow/python) and, from there, open a terminal window and do:

    python FlowAnalyzer.py

This will bring up the interface shown in Figure 1.

![img](./figures/figure_1.png "Initial window of the Optical Flow GUI.")

Click on the button “Open File” to choose the video file to be analyzed. The first frame of the video will be shown in the interface (Figure 2). You can use the slider at the bottom of the window to browse the video.

If you don't want to analyze the whole video file, you can use the “Initial Frame” and “Final Frame” spinboxes to define the segment of interest to be analyzed.

![img](./figures/figure_2.png "Optical Flow GUI after a video file has been loaded.")

Click somewhere on the image frame and use the mouse to define a rectangle. When you release the mouse button, you will be presented with a dialog box where you can choose the region's name and type (interest or disinterest) (Figure 3). You can define as many regions as you want. The algorithm will compute one motion signal for each region of interest defined.

Motion within regions of disinterest is completely ignored. This is useful when there are regions in the image frame whose motion we need to ignore (e.g., a running time stamp somewhere in the frame). It's interesting to note that by defining overlapping regions of interest and disinterest we can create what's effectively non-rectangular regions of interest (Figure 4).

After defining all regions, click the button “Go” to run the analysis. Depending on the video's resolution and frame rate and on the number of frames to be processed, this may take a long time.

Once the analysis is finished, a figure is plotted showing all the computed motion signals (Figure 5). There is one such signal per region of interest. This figure is exported to disk as a pdf file.

The computed motion signals are saved to disk as an Excel spreadsheet and also as an HDF file (<http://www.hdfgroup.org>). The contents of both files are exactly the same.

The HDF motion file can be loaded into Matlab by using the scripts available in the folder matlab. For instructions on how to load and plot the motion signals in Matlab, have a look at the script sample.m in that folder.

![img](./figures/figure_3.png "Defining a region of interest in the Optical Flow GUI.")

![img](./figures/figure_4.png "Regions of interest and disinterest.")

![img](./figures/figure_5.png "Motion signals computed from optical flow.")


<a id="orge21def6"></a>

# Auxiliary tools

The FlowAnalyzer software defines an API and provides a set of tools for performing optical flow analysis on videos. The FlowAnalyzer GUI is the most commonly used of these tools and for many users it may be all they need. Nevertheless, there are some additional tools to help users with some specific tasks, as listed below:

-   `flow_analyzer.py` - this is a command line version of FlowAnalyzer.py. It allows you to perform optical flow analysis of a movie file without interacting with the GUI. This is useful when you need to process a movie non-interactively.

-   `batch_processing.py` - this script batch processes all the movie files in a given directory.

-   `create_flow_movie.py` - this script creates a flow movie from a flow field (hdf) file. In the future, this functionality will be incorporated into the FlowAnalyzer application so that extracting the motion signals and creating the flow movie can be done in parallel, in a single pass. This will make it unnecessary to create the intermediate flow field file (which can be quite big depending on the duration and resolution of the movie under analysis).

-   `read_flow_signals.py` - this script imports a motion signals file into Python

-   `read_flow_signals.m` - this script imports a motion signals file into Matlab

