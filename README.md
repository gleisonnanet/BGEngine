![](doc/readme/GitHub_Readme1.png)

UPBGE (**Uchronia Project Blender Game Engine**) is a fork of Blender created by Porteries Tristan (a Blender Game Engine developer) and some of his friends in September 2015.

It's an independent branch, and its aim is to clean up and improve current Blender Game Engine (BGE) code, experiment with new features, and implement forgotten features that currently exist but have not been merged with the official Blender trunk.

Currently, after the Blender Foundation's decision to delete BGE from next 2.8 release UPBGE becomes, de facto, the only one to follow the development of the Game Engine. This gives us even more freedom, if possible, to make certain decisions, since we will never, in any way, come into conflict with the official version.

Its development cycle spans the course of 4 months: 3 months to add new features and refactors and 1 months to fix bugs. Then a new release is made available for download (around 3 or 4 per year).

Regularly, the UPBGE merges the official Blender new patches, to stay up-to-date with the last Blender evolutions.

The UPBGE team is composed of volunteers; BGE users who are interested in the game engine development, a web developer, and a communication manager.

## What's new?
You can take a look at the release notes to see all the new features:
[UPBGE **Release Notes**](https://github.com/UPBGE/blender/wiki/Release-notes)

## From The Team
We hope that new users will join the project, to help us test new features, report bugs, provide feedback and ideas to improve UPBGE (https://github.com/UPBGE/blender/issues), and that new developers will join the team to help us develop shiny new features for the game engine.

Building Blender on Ubuntu
Quick Setup
The following instructions will create a Blender build in a blender-git folder in your home directory.

Install Packages
Install essential packages with the package manager.

sudo apt update
sudo apt install build-essential git subversion cmake libx11-dev libxxf86vm-dev libxcursor-dev libxi-dev libxrandr-dev libxinerama-dev libglew-dev
For Wayland support (BUILD_CMAKE_ARGS="-DWITH_GHOST_WAYLAND=ON")

sudo apt install libwayland-dev wayland-protocols libegl-dev libxkbcommon-dev libdbus-1-dev linux-libc-dev
Download Sources
Download the latest source code from the git.blender.org.

mkdir ~/blender-git
cd ~/blender-git
git clone https://git.blender.org/blender.git
For additional information on using Git with Blender's sources, see Git Usage.

Download Libraries
For Intel and AMD Linux systems, we recommend using precompiled libraries. These are the quickest way to get a feature complete Blender build and can be downloaded as follows.

These libraries are built on CentOS 7 for VFX reference platform compatibility, but they work fine on other Linux distributions.

mkdir ~/blender-git/lib
cd ~/blender-git/lib
svn checkout https://svn.blender.org/svnroot/bf-blender/trunk/lib/linux_centos7_x86_64
For other systems or to use system packages, see Advanced Setup.

Update and Build
Get latest source code and add-ons, and build. These commands can be used for the first build, and repeated whenever you want to update to the latest version.

cd ~/blender-git/blender
make update
make
After the build finished, you will find blender ready to run in ~/blender-git/build_linux/bin.

If building fails after an update, it sometimes helps to remove the ~/blender-git/build_linux folder to get a completely clean build.

Advanced Setup
Automatic Dependency Installation
When not using precompiled libraries, the preferred way to install dependencies under Linux is to use the install_deps.sh script in the Blender sources. It will install system packages where possible, and if needed can build some libraries from source.

It currently supports Debian (and derivatives), Ubuntu, Fedora, Suse and Arch distributions. It is executed as follows.

cd ~/blender-git
./blender/build_files/build_environment/install_deps.sh
Some commands in this script requires sudo, so you'll be likely be asked for your password. When the script finishes installing/building all the packages, it prints the instructions to configure the build with the required CMake parameters.

For other distributions, it can:

Print the list of all main dependencies needed to build Blender (--show-deps option).
Attempt to build main 'big' libraries you cannot easily install from packages (--build-foo options, see --help of the script for details).
Important It might be required to re-run install-depsh.sh once in a while, as Blender updates its dependencies. You will typically want to try this when you have build errors after updating the sources.

Portable Builds
The above instructions install packages through the system package manager. This makes it possible to share packages between Blender and other software, however the resulting builds will generally not work on other computers.

When using the precompiled libraries, builds are portable and can be shared with others. These libraries are built from source, and this system can also be used to create your own portable libraries.

Running make deps will build libraries in ../lib/linux_x86_64, which will be automatically picked up when building Blender itself.

Besides the libraries, the glibc version of the system affects portability. Builds will only run on Linuxes with the same or higher glibc version. Official builds are made with RHEL 7 and glibc 2.17.

Manual CMake Setup
Build Options
By default Blender builds will be similar to official releases. Many Build Options are available for debugging, faster builds, and to enable or disable various features.

System Installation
Portable installation is the default where scripts and data files will be copied into the build '~/blender-git/build/bin' directory and can be moved to other systems easily.

To install Blender into the system directories, a system installation can be used instead. Disable WITH_INSTALL_PORTABLE to install into CMAKE_INSTALL_PREFIX which uses a typical Unix FHS layout: bin/, share/blender/, man/ etc.

Optimize Rebuilds
