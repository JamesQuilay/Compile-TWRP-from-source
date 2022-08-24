# How to compile twrp from source 
# For Android 8.1 (Oreo) tested in kali linux 2022.3
# Last updated on August 23,2022 (Tuesday)


# Update system repositories
sudo apt update

# Login via bash
bash

# Install repo
sudo apt install repo

# Install dependencies
sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig m4

# Manually install openjdk8
# If error occurs while installing check output to fix
goto https://www.openlogic.com/openjdk-downloads
download .deb files
dpkg -i <packagename>.deb

# Manually set java version to 1.8.x
sudo update-alternatives --config java
sudo update-alternatives --config javac

# Make desired directory
mkdir <directoryname>
cd <directoryname>

# Configure repo
git config --global user.name Your Name
git config --global user.email you@example.com (Tip: your google email)

# Get Twrp Manifest Files
# It will take a several hours, depends on your internet connection and pc performance 
repo init -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-8.1
repo sync

# Find device tree and make directory like this (device/manufacturer/codename)
# Note: replace manufacturer and codename based on your device 
# Or Make yourself, just enter this (python3 -m pip install twrpdtgen) and 
# And enter this in terminal: python3 -m twrpdtgen <path/to/recovery>
# Makesure your python is 3.7 above or else it will fails to find
# build.prop

# Set your python to 2.7
sudo ln -s /usr/bin/python2 /usr/bin/python

# To check python version
python -V

# Start Building 
. build/envsetup.sh 
export LC_ALL=C 
lunch 
make recoveryimage
