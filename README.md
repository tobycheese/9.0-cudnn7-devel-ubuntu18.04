# 9.0-cudnn7-devel-ubuntu18.04
Docker image for Ubuntu 18.04 with cuda 9.0

As Nvidia does not provide Docker images for the combination of older cuda versions with never versions of Ubuntu, I made this image. I copied together as much as possible from the original Nvidia Dockerfiles, making changes only where necessary.

Main benefits (as of 2019-01-19):

* tensorflow officially requires cuda 9.0 (though now packages for never versions exist, but have not for a long time)
* Ubuntu 18.04 has Python 3.6
