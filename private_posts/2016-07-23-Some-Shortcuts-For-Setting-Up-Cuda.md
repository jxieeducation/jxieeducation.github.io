---
layout: post
category : tutorial
tags: cuda
tagline: "Cuda Ubuntu Setup"
excerpt: Cuda Ubuntu Setup

---

### How to setup Cuda on Ubuntu 14.04

After spending thousands in the past 2 years using AWS EC2 GPUs, I decided that it's finally time for me to get my own deep learning setup. Unlike with ec2 virtualizations where I can just use an existing CUDA image, I had to setup Cuda and Nvidia drivers myself for the first time. 

There have been many tutorials dedicated to troubleshooting the process. However, I really struggled because of difference advices and unclear instructions on the Ubuntu forum. So I will just try to explain in my words how to setup Cuda.

### Nvidia

When you first install Ubuntu, the display graphics is likely messed up because the Nvidia display drivers are not installed yet. The first step is to install Nvidia. 

If you simply try to install via ``` sudo apt-get install nvidia-352 ```, you will encounter the infamous [login loop problem](http://askubuntu.com/questions/614128/15-04-and-nvidia-login-loop). 

If you encounter this issue, follow the following [steps](http://askubuntu.com/questions/451221/ubuntu-14-04-install-nvidia-driver#answer-700613). The ```ubuntu-drivers autoinstall``` commands saves the trouble of the complications in setting up nvidia.

### Cuda

After rebooting, Ubuntu display should now be fixed, because graphics drivers are not setup properly. The next step is to install Cuda.

The most painless way is to follow [this](http://askubuntu.com/questions/672047/anyone-has-successfully-installed-cuda-7-5-on-ubuntu-14-04-3-lts-x86-64#answer-736505), with 1 tiny change.

During step 6(b), instead of saying yes to installing Nvidia again, say no. **P.S. Letting Cuda reinstall your Nvidia will cause the login loop again.** Everything else stays the same.

### Conclusion

After everything is setup, enjoy going through the ```NVIDIA_CUDA-7.5_Samples```. Hopefully this guide have made your experience much better than mine! 

