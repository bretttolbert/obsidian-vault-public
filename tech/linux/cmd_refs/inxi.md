# inxi

###### Get information about graphics card(s)
```bash
$ inxi -Gx
Graphics:
  Device-1: NVIDIA GP106 [GeForce GTX 1060 6GB]
    vendor: ASUSTeK DUAL-GTX1060-O6G driver: nvidia v: 390.151 bus-ID: 01:00.0
  Display: x11 server: X.Org v: 1.21.1.3 driver: X: loaded: nvidia
    unloaded: fbdev,modesetting,nouveau,vesa gpu: nvidia resolution:
    1: 3840x2160~60Hz 2: 3840x2160~60Hz
  OpenGL: renderer: GeForce GTX 1060 6GB/PCIe/SSE2 v: 4.6.0 NVIDIA 390.151
    direct render: Yes
```

###### torch error `UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 9010)`
```
>>> import torch
/home/brett/PyVEnvs/sileroenv/lib/python3.10/site-packages/torch/cuda/__init__.py:83: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 9010). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at  ../c10/cuda/CUDAFunctions.cpp:109.)
  return torch._C._cuda_getDeviceCount() > 0
```

###### CUDA setup

```bash
sudo apt install nvidia-cuda-toolkit
```

```bash
nvcc
```

```
You need 387 driver for 9.1 toolkit, 384 corresponds to 9.0 (as the error message tells you)
```

But I have driver 390.151 which should be compatible with CUDA 9.1:

CUDA Tookit version 9.1 (9.1.85) requires Linux x86_64 Driver Version >= 390.46
CUDA Toolkit version 11.7 GA 	requries Linux x86_64 Driver Version >=515.43.04 (and I now have 515.48.07)

https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#major-components


https://gist.github.com/DaneGardner/accd6fd330348543167719002a661bd5


# CUDA 11.7 Installation Test

```bash
lsmod | grep nouv && echo FAIL || echo OKAY
lsmod | grep nvid && echo OKAY || echo FAIL

grep -E 'NVIDIA.*515.[0-9]+' /proc/driver/nvidia/version &>/dev/null && echo OKAY || echo FAIL
nvcc -V | grep -E "V11.7.[0-9]+" &>/dev/null && echo OKAY || echo FAIL
```


## Install CUDA 11.7

```bash
wget https://developer.download.nvidia.com/compute/cuda/11.7.0/local_installers/cuda_11.7.0_515.43.04_linux.run
sudo sh cuda_11.7.0_515.43.04_linux.run --override --toolkit
```

```
===========
= Summary =
===========

Driver:   Not Selected
Toolkit:  Installed in /usr/local/cuda-11.7/

Please make sure that
 -   PATH includes /usr/local/cuda-11.7/bin
 -   LD_LIBRARY_PATH includes /usr/local/cuda-11.7/lib64, or, add /usr/local/cuda-11.7/lib64 to /etc/ld.so.conf and run ldconfig as root

To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-11.7/bin
***WARNING: Incomplete installation! This installation did not install the CUDA Driver. A driver of version at least 515.00 is required for CUDA 11.7 functionality to work.
To install the driver using this installer, run the following command, replacing <CudaInstaller> with the name of this run file:
    sudo <CudaInstaller>.run --silent --driver


```


