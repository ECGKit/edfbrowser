# EDFBrowser
This is a fork of the original [EDFBrowser](https://gitlab.com/Teuniz/EDFbrowser) with modifications for the [OpenSCORE](https://github.com/DWonGH/OpenSCORE) and [TEETACSI](https://github.com/DWonGH/TEETACSI)
projects. EDFBrowser has been modified to run as a feature in OpenSCORE and to record the state of the UI to file for TEETACSI.

To build on Windows need to download Qt, Qt Creator, and install MinGW compiler tools like gcc and g++.

The source code specific to OpenSCORE and TEETACSI can be found on the ui_log_reduced development branches, and pre-built ```.exe```'s and binaries can be found in the 
releases section. Use the latest [release](https://github.com/d3-worgan/edfbrowser/releases) for the most up to date and reduced feature EDFBrowser for TEETACSI, 
and use the [OpenSCORE](https://github.com/d3-worgan/edfbrowser/releases/tag/v2.0) version for a full featured EDFBrowser when creating score reports.

To run without OpenSCORE from the command line:
1. The first argument is the absolute path to an EDF file. The second 
argument is an absolute path to the location where to save the log files. The third argument is a pre-defined montage (```.mtg```) file.
2. EDFBrowser will create a directory in the specified output location. It will write a ui_log file, png screenshot
images to the screenshots directory, and montage files to the montages directory.
3. Close edf browser
4. Use the 


Below is the original instructions for compiling on Linux systems

# Requirements
Qt  http://www.qt.io/

Qt4 minimum version 4.7.1 or later, preferable 4.8.7

or

Qt5 minimum version 5.9.1 or later, preferable 5.12.10

EDFbrowser is a GNU/Linux & GCC & GNU Make project. Other tools or compilers are not supported.


Introduction
============

EDFbrowser is a Qt application and uses qmake as part of the build process.
Qmake is part of your Qt installation.



Compiling and installing on Ubuntu Linux and derivatives
========================================================
```
sudo apt-get update
sudo apt-get install g++ make git qtbase5-dev-tools qtbase5-dev qt5-default
git clone https://gitlab.com/Teuniz/EDFbrowser.git
cd EDFbrowser
qmake
make -j24  (change option -j according to number of available cpu cores/threads e.g -j4 or -j8)
sudo make install
edfbrowser
```



Advanced users (keep in mind, EDFbrowser is NOT a community project, pull/merge requests will be ignored)
=========================================================================================================

In case you want to compile EDFbrowser "static" with Qt5, here is a howto:

First, fulfill the requirements for Qt:

https://doc.qt.io/qt-5/linux.html

Debian/Ubuntu: sudo apt-get install build-essential libgl1-mesa-dev libcups2-dev libx11-dev

Fedora: 
```
sudo dnf groupinstall "C Development Tools and Libraries"
sudo dnf install mesa-libGL-devel cups-devel libx11-dev
```
openSUSE: sudo zypper install -t pattern devel_basis
          sudo zypper install xorg-x11-devel cups-devel freetype-devel fontconfig-devel libxkbcommon-devel libxkbcommon-x11-devel

# Compile a static version of the Qt5 libraries excluding all modules that are not needed.
```
mkdir Qt5-source
cd Qt5-source
wget https://ftp1.nluug.nl/languages/qt/official_releases/qt/5.12/5.12.10/single/qt-everywhere-src-5.12.10.tar.xz
```
here is a list of download mirrors: https://download.qt.io/static/mirrorlist/
The Qt source package you are going to need is: qt-everywhere-src-5.12.10.tar.xz
```
tar -xvf qt-everywhere-src-5.12.10.tar.xz

cd qt-everywhere-src-5.12.10

./configure -v -prefix /usr/local/Qt-5.12.10-static -release -opensource -confirm-license -c++std c++11 -static -accessibility -fontconfig -no-libudev -no-vulkan -skip qtdeclarative -skip qtconnectivity -skip qtmultimedia -qt-zlib -no-mtdev -no-journald -qt-libpng -qt-libjpeg -system-freetype -qt-harfbuzz -no-openssl -no-libproxy -no-glib -nomake examples -nomake tests -no-compile-examples -cups -no-evdev -no-dbus -no-egl -no-eglfs -qreal double -no-opengl -skip qtlocation -skip qtsensors -skip qtwayland -skip qtgamepad -skip qtserialbus -skip qt3d -skip qtpurchasing -skip qtquickcontrols -skip qtquickcontrols2 -skip qtspeech -skip qtwebengine

make -j24  (change option -j according to number of available cpu cores e.g -j4 or -j8)
```
(takes about 2.5 minutes on an AMD Ryzen 9 3900X)
```
sudo make install
```
Now go to the directory that contains the EDFbrowser sourcecode and enter the following commands:
```
/usr/local/Qt-5.12.10-static/bin/qmake

make -j24  (change option -j according to number of available cpu cores e.g -j4 or -j8)

sudo make install
```

Now you can run the program by typing: ```edfbrowser```

Congratulations!
You have compiled a static version of EDFbrowser that can be deployed on other systems without the need
to install the Qt libraries.
In order to reduce the size of the executable, run the following commands:

strip -s edfbrowser

upx edfbrowser (if upx is not recognized as a command, install it using your package manager)



Requirements on macOS (warning, I don't have a Mac and I can not support it!)
=====================

Development tools from Apple: to get them, run
```
xcode-select --install

Qt >= 5.9.1: one method to get Qt on macOS is to install it via homebrew:

brew install qt
```
Note: after installing, qmake will likely not be in your $PATH, so you need to invoke it using its full path.


Build on macOS
==============

In the directory where you extracted sourcefile or cloned git repo, first run qmake, then make
(change option -j according to number of available cpu cores, get with 'sysctl -n hw.ncpu' command):
```
$(brew --prefix qt)/bin/qmake
make -j4
```
You can also build it in a dedicated subdirectory:
```
mkdir build
cd build
$(brew --prefix qt)/bin/qmake ..
make -j4
```
This will create the app bundle in the current directory, which you can then move to /Applications/ if desired.





