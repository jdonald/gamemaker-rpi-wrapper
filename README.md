GameMaker (YoYo Games) Pi Runner wrapper
=============================

This is a wrapper for Pi games built on GameMaker that originally target
the dispmanx-based graphics libraries. This allows for running these
these legacy binaries with the Mesa driver on Raspbian Stretch or newer,
but might also serve to run the programs on non-Broadcom chips.

This was forked from xobs/mcrpi-wrapper with the following modifications:

* Removed unnecessary counters that were delaying necessary egl*() API calls
* Added shims for GLES1 functions to their GLES2 counterparts lacking the OES suffix
* Reduced requested resolution, otherwise window fails to initialize properly

Usage
-----

Download any or all three games from [https://www.yoyogames.com/pi]

    tar xvf SuperCrateBox.tar.gz
    tar xvf MalditaCastilla.tar.gz
    tar xvf TheyNeedToBeFed.tar.gz

Clone this repo.

    cd gamemaker-rpi-wrapper
    make

    sudo raspi-config # Enable full OpenGL with KMS

    sudo apt install libegl1-mesa libgles2-mesa

    cd path/to/SuperCrateBox # or one of the other games from Yoyo Games
    LD_PRELOAD=path/to/gamemaker-rpi-wrapper/libbcm_host.so.1.0 ./SuperCrateBox

Super Crate Box works well. Maldita Castilla is quite playable although the world
jitters when scrolling forward. They Need To Be Fed seems to have trouble properly
handling mouse movement and clicks.
