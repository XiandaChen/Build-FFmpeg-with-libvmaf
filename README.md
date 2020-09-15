# Build & Install FFmpeg with libvmaf on Ubuntu 18.04
[FFmpeg](https://ffmpeg.org/ffmpeg.html) is the leading multimedia framework, able to decode, encode, transcode, mux, demux, stream, filter and play pretty much anything that humans and machines have created. [VMAF](https://github.com/Netflix/vmaf) is a perceptual video quality assessment algorithm developed by Netflix. VMAF Development Kit (VDK) is a software package that contains the VMAF algorithm implementation, as well as a set of tools that allows a user to train and test a custom VMAF model.

VMAF in FFmpeg: https://ffmpeg.org/ffmpeg-filters.html#libvmaf \
https://websites.fraunhofer.de/video-dev/calculating-vmaf-and-psnr-with-ffmpeg/

## Installation
1. Install [Meson](https://mesonbuild.com/index.html) and [Ninja](https://github.com/ninja-build/ninja) using following commands:
    
    `sudo apt-get install ninja-build`
    
    `pip install meson`
2. Get latest VMAF SDK release from [here](https://github.com/Netflix/vmaf/releases).
3. Unzip VMAF SDK zip and install `libvmaf` with following commands:
    
    `cd vmaf-1.3.15`
    
    `sudo make`
    
    `sudo make install`
4. Get latest FFmpeg soruce from [here](https://ffmpeg.org/download.html).
5. Build and install ffmpeg with libvamf using following commands:
    
    `./configure --enable-gpl --enable-libx264 --enable-libx265 --enable-nonfree --enable-libvmaf --enable-version3`
    
    `sudo make`
    
    `sudo make install`
    
    `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib`
    
## bugs and solutions
1. Unable to import a module that is definitely installed (Python.h) \
    #!/usr/bin/env python3 in vmaf-1.5.3/python/setup.py \
    
    2-1. /usr/bin/python3 may refer to undesired python3.x site-packages/, set \
    > sudo ln -s /usr/bin/python3.x /usr/bin/python3 
    
    2-2. https://blog.ducthinh.net/gcc-no-such-file-python-h/
2. error while loading shared libraries: libvmaf.so \
    https://github.com/Netflix/vmaf/issues/528 \
    /usr/local/lib/libvmaf.so

3. 
