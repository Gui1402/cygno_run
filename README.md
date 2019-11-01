# How to configure and run the CYGNO Reconstruction Algorithm

This repository is for configuring the libraries used to get cygno images.


**Installing root**

    -Download root on: https://root.cern.ch/content/release-61404

You can extract the tar file by typing the following command in terminal:
      
     $tar -xvzf root_v6.14.04.source.tar.gz root-6.14.04/
     
There are many softwares and libraries that should be installed on your system for installation of ROOT. The list of prerequisites can be found at https://root.cern.ch/build-prerequisites. Install prerequisites by typying the following line into the terminal:

     $sudo apt-get install git dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev gfortran libssl-dev libpcre3-dev xlibmesa-glu-dev libglew1.5-dev libftgl-dev libmysqlclient-dev libfftw3-dev libcfitsio-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl0-dev libqt4-dev

It is recommended to build the ROOT in a separate folder other than the source folder so we should create a folder called "root" in the same directory where *root-6.14.04* is present. It's just type it into the terminal:

    $mkdir root
    $cd root

To install root and enable all libraries we need to type the follow command into the terminal:

    $cmake ../root-6.10.04/ -Dall=ON
    $cmake --build . -- -j3        ## if your processor has less than 3 cores you need to change j3 by j1 or j2
    $. bin/thisroot.sh
    
After the installation it's advisable to add root PATH to your *.bashrc* file.

    $pwd     ## to get root path
    $nano ~/.bashrc ## open bashrc file
    
Paste the following command lines at end of the your *.bashrc* file:
  
    export ROOTSYS=/home/myuser/Downloads/root     ## folder from pwd command
    export PATH=$ROOTSYS/bin:$PATH
    export LD_LIBRARY_PATH=$ROOTSYS/lib/:$LD_LIBRARY_PATH
  
Restart the terminal and try to run root in order to check if it is working properly.
	
	$ ROOT


**Config the virtual enviroment**

To do that you need to install pip(python's manager packages) or Anaconda(miniconda also works).

Install and create your virtualenv:

    $pip install virtualenv
    $virtualenv virutal_env_name
    
Active virtualenv:
    
    $git source bin/activate

Link your folder and this project:
    
    	$git init
	$git remote add origin 
	$git pull
    
Install project requirements:
    
    $pip install -r requirements.txt
    
**Cloning and running the repository**

After virtual environment configuration the next step is to clone cygnus analysis repository:

	$git clone https://github.com/CYGNUS-RD/analysis.git

And by now the up-to-date branch is *fng_18*.

Into the repository, you can run the file reconstruction.py. And it is recommended to make a directory to salve the outputs using:
	
	$mkdir plots_example
	
Before run the algorithm you will need to download the images that should be analysed. It is possible to find a tutorial on how to download the data using the [this]() tutorial. And it is also important to note that the input should be a *.root* file and some of the data are in *.h5* files.

**Convert the H5 files in ROOT files with TH2D**

First clone the repository: https://github.com/CYGNUS-RD/hdf2root
Then run this code on the terminal:

	$python2 hdf2root.py <folder-where-the-h5-was-placed>/<beginning-of-the-files-name>*.h5 -o <output-file>.root
	**Example**
	$python2 hdf2root.py ../ConvertingData/Run818/run818*.h5 -o histogram_Run00818.root

The usual name of the runs after the conversion is *histogram_Run00494.root*
or *histograms_Run01515.root* if it was already a root file.

Then, it's just run this code on the terminal:	
	
	$python3 reconstruction.py configFile.txt --pdir plots_example plots --max-entries 50 -j2

- *configFile.txt* is the configuration file with all the settings.
- *pdir* is the directory where the plots will be saved.
- *max-entries* is the number of images you want to analyse.
- *j* is the number of cores you want to use.

If the funciont import ROOT does not work, you will need to add a codeline into bash.rc file.

	$nano ~/.bashrc ##open bashrc in the terminal
	$source /full/path/to/your/ROOT/bin/thisroot.sh ## add source root.sh in that file
	
