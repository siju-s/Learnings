### BUILD AOSP ON UBUNTU (VIRTUAL BOX)

#### Ubuntu Setup

1. Download`VirtualBox` from <https://www.virtualbox.org/wiki/Downloads> . Make sure to also download the extension pack.
2. Install Ubuntu from <https://ubuntu.com/download/desktop>
3. Create new VM in `VirtualBox` as `Linux`. Choose Storage as `Fixed` and give at least 300 GB or more.
4. Install Ubuntu by mounting the downloaded ISO in `VM Settings -> Storage->SATA`



#### Android Setup

1. Install all the required packages

   `sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig`

2.  Setup `Git` config

   ```
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

3.  Install `repo` 

   ```
   mkdir ~/bin
   curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
   chmod a+x ~/bin/repo
   ```

4. Open `bashrc` file using `nano ~/.bashrc`

5. Add the below at the bottom of the file

   ```
   export PATH=~/bin:$PATH
   ```

6. Reload bash using `source ~/.bashrc`

   ##### Downloading source

```
mkdir ~/aosp12
cd ~/aosp12
repo init -u https://android.googlesource.com/platform/manifest -b android-12.0.0_r2
```

Branch info can be found on <https://source.android.com/setup/start/build-numbers#source-code-tags-and-builds>

After `repo` is initialized, download source using

```
repo sync -c -j8
```

This will take 1-4 hours depending on internet connection speed.

##### Building source

To build, run the following command from the `aosp12` folder

```
source build/envsetup.sh
lunch
```

Select the number for which device you need to build like 35 for `sunfish userdebug (Pixel 4a)`

To start build, run

```
make -j8
```

This might take hours depending on RAM and cores on CPU.





##### Recommended Machine config

32 or 64 GB RAM

6 cores or above













### TROUBLESHOOTING

1. `Virtual box` full screen can be achieved through `Devices -> Insert Guest Additions` when Ubuntu is running. If you get error `System cannot build kernel modules`, make sure to install 

   `sudo apt install build-essential linux-kernel-headers`

2.  During repo init, if you face any python related issues like `/usr/bin/env: ‘python’: No such file or directory` , then run the below command

   ```
   sudo ln -s /usr/bin/python3 /usr/bin/python
   ```

   





#### REFERENCES

1. Convert fixed -> Dynamic and vice versa in Virtual box  <https://www.howtogeek.com/312456/how-to-convert-between-fixed-and-dynamic-disks-in-virtualbox/>
2. Build AOSP for Sony devices <https://developer.sony.com/develop/open-devices/guides/aosp-build-instructions/build-aosp-android-12-0>
3. Android official guide <https://source.android.com/setup/build/initializing>
4. Fix `Python 3` symlink issue <https://liongueststudios.com/download-and-build-aosp-android11-custom-rom/>