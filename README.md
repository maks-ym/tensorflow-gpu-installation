## README
> Notes and links to install TensorFlow GPU

If `pip 3 -U install tensorflow-gpu` did not work and you need compile TensorFlow GPU.

I had this messege: `The TensorFlow library was compiled to use AVX instructions, but these aren't available on your machine.`

### General steps
0. Check versions of OS, CUDA capability of GPU, python
1. Install nVidia driver
2. Install CUDA
3. Install cuDNN
4. Compile TensorFlow GPU
5. Install TensorFlow and some other useful packages
6. Test installation
7. Compiled python wheels
8. Other useful links

### Check versions of OS, CUDA capability of GPU, python

#### OS version (Ubuntu)

**GUI**: Settings > Details > *Ubuntu 18.04LTS*

**Bash**: `$ lsb_release -a` # See **Description** line

#### CUDA capability (version)

Find in table here: https://en.wikipedia.org/wiki/CUDA#GPUs_supported

#### python version

> $ python3 --version # e.g. Python 3.6.8

### Install nVidia driver

Check versions used for prebuilt packages: https://www.tensorflow.org/install/source#linux

For example, for TF 12
| Version | Python version | Compiler | Build tools | cuDNN | CUDA |
| --- | --- | --- | --- | --- | --- |
| tensorflow_gpu-1.12.0 | 2.7, 3.3-3.6 | GCC 4.8 | Bazel 0.15.0 | 7 | 9 |

`nvidia-390` is OK for CUDA 9.

Google for instructions.

### Install CUDA

*CUDA Toolkit 9.0* for *Ubuntu 18.04* is not available, but version for *17.04* should work fine.

* visit & download: https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1704&target_type=runfilelocal
* base installer must suffice, read instructions there

### Install cuDNN

> cuDNN 7 (v7.0.5)

* download cuDNN 7 (v7.0.5): [origina page (need account)](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/9.0_20171129/cudnn-9.0-linux-x64-v7)
* download appropriate tar archive (`cuDNN vX.X.X` Library for `CUDA Y.Y`) 

```bash
$ tar -xzvf cudnn-9.0-linux-x64-v7.tgz
$ sudo cp cuda/include/cudnn.h /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
[installation instructions taken from here](https://developer.download.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/Doc/cuDNN-Installation-Guide.pdf?3XnViXudgpO1wDx_qLlC-EW1BJHGwxpEDDYBXFUCKtjgc_18oxXgfG49FSZWck_m1FTa09g5GTk57LGYPb7jB5TgtAIOlIrZTCuPf1CIJC2VemxIh9kfrjlUGonMMLnztHttD5LT_oF3huMnNVju7jIW6ca10uW3dZ3kZOti9uIs7B3wSulhKi9sdDwZgdHzQw#%5B%7B%22num%22%3A19%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C108%2C275.369%2Cnull%5D)
