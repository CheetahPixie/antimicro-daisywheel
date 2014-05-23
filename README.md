# antimicro

## Description

AntiMicro is a graphical program used to map keyboard keys and mouse controls
to a gamepad. This program is useful for playing PC games using a gamepad that
do not have any form of built-in gamepad support. However, you can use this 
program to control any desktop application with a gamepad; on Linux, this
means that your system has to be running an X environment in order to run
this program.

This program is currently supported under various Linux
distributions and Windows Vista and later. At the time of writing this,
AntiMicro works in Windows XP but, since Windows XP is no longer supported,
running the program in Windows XP will not be officially supported.
However, efforts will be made to not intentionally break compatibility
with Windows XP.

## License

This program is licensed under the GPL v.3. Please read the gpl.txt text document
included with the source code if you would like to read the terms of the license.
The license can also be found online at
[http://www.gnu.org/licenses/gpl.txt](http://www.gnu.org/licenses/gpl.txt).

## Build Dependencies

This program is written in C++ using the [Qt](http://qt-project.org/)
framework. A C++ compiler and a proper C++ build environment will need to be
installed on your system prior to building this program. Under Debian and
Debian-based distributions like Ubuntu, the
easiest way to get a base build environment set up is to install the
meta-package **build-essential**. The following packages are required to be
installed on your system in order to build this program:

* g++
* cmake
* libqt4-dev
* libsdl1.2-dev (or libsdl2-dev)
* libxtst-dev
* libX11-dev

## Building under Linux

In order to build this program, open a terminal and cd into the antimicro
directory. Enter the following commands in order to build the program:

    cd antimicro
    mkdir build && cd build
    cmake ..
    make
    sudo make install

The installation path of antimicro can be customized by specifying the
CMAKE_INSTALL_PREFIX variable while running cmake.

    cmake -DCMAKE_INSTALL_PREFIX=/usr ..

This will install the antimicro executable to /usr/bin/antimicro.
By default, the executable will be installed to /usr/local/bin/antimicro.

The cmake step will use pkg-config to attempt to find any SDL
libraries that you have installed. The project is set up to
look for a copy of SDL 2 followed by SDL 1.2. This behavior should work
fine for most people. You can override this behavior by using the -DUSE_SDL_2
option when you run cmake. Using -DUSE_SDL_2=ON when you run cmake will mean
that you want AntiMicro compiled with SDL 2 support. Using -DUSE_SDL_2=0FF when
you run cmake will mean that you want AntiMicro compiled with SDL 1.2 support.

Here is an example of how to specify that you want AntiMicro to be compiled
with SDL 2 support when you run qmake.

    cmake -DUSE_SDL_2=ON ..

## Building under Windows

**Instructions provided by aybe @ https://github.com/aybe.
Modified by Travis Nickles.**

* Download and install CMake: http://www.cmake.org/cmake/resources/software.html

* You will need Qt with MinGW support: http://qt-project.org/downloads

* download SDL development package : http://www.libsdl.org/release/SDL2-devel-2.0.3-mingw.tar.gz

* open the archive and drop the 'SDL2-2.0.3' folder in the 'antimicro' folder

* open the project (CMakeLists.txt) in Qt Creator The CMake Wizard will appear
the first time you open the project in Qt Creator.

* Choose a Build Location. The recommendation is to create a "build" folder
under the root antimicro folder and choose that for the build location.

* In the Run CMake section, in the Arguments field, please input
-DCMAKE_PREFIX_PATH=<Path to mingw48_32 Qt install>
-DCMAKE_BUILD_TYPE=Release. Replace "<Path to mingw48_32 Qt install>"
with the actual path to your Qt installation. The default path for version
Qt 5.1.1 is C:\Qt\5.1.1\mingw48_32\.

* Choose "MinGW Generator" for the Generator option in the Run CMake section

* Click the Run CMake button and then click Finish

* In the main IDE window, open the Build menu and select "Build All" (Ctrl+Shift+B)

* The application will need SDL2.DLL. A build step has been added to
CMakeLists.txt in order to automate the process. Click the "Projects" icon
in the sidebar to bring up the "Build Settings" section. Within
"Build Steps", click the "Details" button on the Make entry. In the expanded
menu, uncheck the "all" checkbox and then check the "copy_sdl_dll" checkbox
and run "Build All".

* At this point, AntiMicro has been built for Windows and is runnable
from Qt Creator. A couple more steps are required in order to make a
distributable package.

* Under "Build Settings", expand the Make menu and check the "install" and
"install_dlls" checkboxes.

* Under the "Build" menu in the main window, select "Run CMake" and
add -DCMAKE_INSTALL_PREFIX=<DIR> option and replace <DIR> with the directory
that you want to install the application. The default for me is
C:\Program Files (x86)\AntiMicro although I use a different directory
when bundling the Window version for other users.

* Run "Build All" to have the application and required DLLs installed
into the final location that will be ready for distribution.

##Building the Windows Installer Package (MSI)

(these instructions have been tested with WiX 3.8)

* you need to have WiX installed, grab it at http://wixtoolset.org/

* the building process relies on the WIX environment, it is recommended that you download the installer instead of the binaries as it it will set it up for you

* if Qt Creator is running while you install or upgrade to a newer version then make sure to restart it as it will either not find that environment variable or fetch the old (incorrect) value from the previous version

* to build the MSI package, click on the "Projects" icon in the sidebar,
click the "Details" button on the make entry, uncheck all other options
and check the "buildmsi" box.

* currently it relies on INSTALL to copy files at the location they are harvested, this might change in the future

Notes about the WXS file and the building process :

* the WXS file has been generated with WixEdit and manually modified to contain relative paths, it will only work from the 'windows' sub-folder (or any other)

* WixCop can be run against the WXS file and it should not point out any errors as the WXS has been corrected previously with the -F switch

* CNDL1113 warning : shortucts are advertised, left as-is as a nice feature about them is that if the program gets corrupted it will be repaired by Windows Installer, by design the shortcuts will not point to antimicro.exe as a regular LNK file

* LGHT1073 warning : SDL2.DLL does not specify its language in the language column, not a big deal; it could be recompiled but it's pretty much a time waste as it would only prevent this warning

* all of these warnings have been made silent through the use of command-line switches.

* built MSI package will be placed in /windows

## Ideas For Future Features

This section is where some of the ideas for future features
for this program will be written.

* Copy set assignments to a new set. This will make creating
slightly altered sets easier.
* Write documentation for portions of the program.
* ~~Convert code base to use CMake as opposed to qmake.~~

Along with this, I will put the simple mind map that I am using to
write ideas for future development into the repository for this
program. The mind map will include extra notes that are not available in
this README. Opening the mind map will require the use of the program
FreeMind which can be downloaded from
[http://freemind.sourceforge.net/wiki/index.php/Main_Page](http://freemind.sourceforge.net/wiki/index.php/Main_Page).

## Shoutout

A big inspiration for this program was the program QJoyPad
([http://qjoypad.sourceforge.net/](http://qjoypad.sourceforge.net/)).
I was a user of the program for years and it is unfortunate that the
program is no longer being maintained. The source code for QJoyPad was an
invaluable resource when I made the first version of this program and the UI
for this program mostly resembles QJoyPad.

## Credits

### Main Developer
Travis Nickles <nickles.travis@gmail.com>

### Contributors
aybe  
Zerro Alvein  
Jeff Backus <jeff.backus@gmail.com>

### Translators

Belleguic Terence <hizo@free.fr> - French  
Jay Alexander Fleming <tito.nehru.naser@gmail.com> - Serbian  
VaGNaroK <vagnarokalkimist@gmail.com> - Brazilian Portuguese
