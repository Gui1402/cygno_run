# cygno_run

This repository is for configuring the libraries used to get cygno images.


**Installing root**

    -Download root on: https://root.cern.ch/content/release-61404

You can extract the tar file by typing following command in terminal:
      
     $tar -xvzf root_v6.14.04.source.tar.gz root-6.14.04/
     
There are many softwares and libraries that should be installed on your system for installation of ROOT. The list of prequisites can be found at https://root.cern.ch/build-prerequisites. Install prequisites by typying following into the terminal:

     $sudo apt-get install git dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev gfortran libssl-dev libpcre3-dev xlibmesa-glu-dev libglew1.5-dev libftgl-dev libmysqlclient-dev libfftw3-dev libcfitsio-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl0-dev libqt4-dev

It is recommended to build the ROOT in a separate folder other than the source folder so we should create a folder called "root" in the same directory where root root-6.14.04 is present. It's just type it into the terminal:

    $mkdir root
    $cd root

To install root and ebable all libraries we need to type the follow command into the terminal:

    $cmake ../root-6.10.04/ -Dall=ON
    $cmake --build . -- -j3        ## if your processor has less than 3 cores you need to change j3 by j1 or j2
    $. bin/thisroot.sh
    
After installation it's just need to add root PATH to .bashrc file.   
    
    $pwd     ## to get root path
    $nano ~/.bashrc ## open bashrc file
    
Paste the following at end of the .bashrc file:
  
    export ROOTSYS=/home/myuser/Downloads/root     ## folder from pwd command
    export PATH=$ROOTSYS/bin:$PATH
    export LD_LIBRARY_PATH=$ROOTSYS/lib/:$LD_LIBRARY_PATH
  
Restart the terminal and root should be works normally.  
    
