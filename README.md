## README
> Notes and links to install TensorFlow GPU

If `pip 3 -U install tensorflow-gpu` did not work and you need compile TensorFlow GPU.

I had this messege: `The TensorFlow library was compiled to use AVX instructions, but these aren't available on your machine.`

### TL;DR

If just want to download compiled version, go to `Compiled python wheels` section

### General steps
1. Check versions of OS, CUDA capability of GPU, python
2. Install nVidia driver
3. Install CUDA
4. Install cuDNN
5. Compile TensorFlow GPU
6. Install TensorFlow and some other useful packages
7. Test installation
8. Compiled python wheels
9. Other useful links

### Check versions of OS, CUDA capability of GPU, python

#### OS version (Ubuntu)

**GUI**: Settings > Details > *Ubuntu 18.04LTS*

**Bash**: `$ lsb_release -a` # See **Description** line

#### CUDA capability (version)

Find in table here: https://en.wikipedia.org/wiki/CUDA#GPUs_supported

#### python version

```bash
$ python3 --version # e.g. Python 3.6.8
```

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

* visit & download CUDA 9.0: 
[official (recommended)](https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1704&target_type=runfilelocal) | 
[mirror](https://drive.google.com/open?id=1BqQIj4Xsx48rX6eZ9EBFqrHFOLObJZHA)
* base installer must suffice, read instructions there

### Install cuDNN

> cuDNN 7 (v7.0.5)

* download cuDNN 7 (v7.0.5): 
[origina page (need account, recommended)](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/9.0_20171129/cudnn-9.0-linux-x64-v7) | 
[mirror](https://drive.google.com/open?id=1uYd045bIragK4RbdSLZhEw0Q9-8jk7U0)
* download appropriate tar archive (`cuDNN vX.X.X` Library for `CUDA Y.Y`) 

```bash
$ tar -xzvf cudnn-9.0-linux-x64-v7.tgz
$ sudo cp cuda/include/cudnn.h /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
[installation instructions taken from here](https://developer.download.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/Doc/cuDNN-Installation-Guide.pdf?3XnViXudgpO1wDx_qLlC-EW1BJHGwxpEDDYBXFUCKtjgc_18oxXgfG49FSZWck_m1FTa09g5GTk57LGYPb7jB5TgtAIOlIrZTCuPf1CIJC2VemxIh9kfrjlUGonMMLnztHttD5LT_oF3huMnNVju7jIW6ca10uW3dZ3kZOti9uIs7B3wSulhKi9sdDwZgdHzQw#%5B%7B%22num%22%3A19%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C108%2C275.369%2Cnull%5D)

* after installing driver, CUDA and cuDNN, to check whether installation is good, run

```bash
$ nvidia-smi
```

Table with info about GPU usage should be shown.

### Compile TensorFlow GPU

* build TF from source as in [instructions here](https://www.tensorflow.org/install/source)
* **Note**: Used Bazel version 0.19.2: 
[official repo (recommended)](https://github.com/bazelbuild/bazel/releases/download/0.19.2/bazel-0.19.2-installer-linux-x86_64.sh) | 
[mirror](https://drive.google.com/open?id=1almk3dxHYxnTzdbkOefgLTQDoKnCT_9b)

### Install TensorFlow and some other useful packages

If done all above TensorFlow should have already been installed.

Additional packages you may like to install:
* keras
* numpy
* scikit-learn
* matplotlib

#### Test installation

To test whether TF uses GPU, run in Terminal:

```bash
$ watch -n1 nvidia-smi
```

And run any example for model training.

#### Compiled python wheels

| TF Version | Python version | Compiler | Build tools | cuDNN | CUDA | Links |
| --- | --- | --- | --- | --- | --- | --- |
| 1.12.0 GPU | 3.6.8 | GCC 6.5 | Bazel 0.19.2 | 7.0.5 | 9 | [download wheel](https://drive.google.com/open?id=1uxVJO72k7O5ymVsADLU19GjkENPUIQ2w) |

#### Other useful links (used while compiling wheels)

* [TF 1.12.0, CPU/GPU, CUDA 9.0, CuDNN 7.4, Python 3.5, Ubuntu 16.04, Skylake, -AVX, +SSE4 #99](https://github.com/yaroslavvb/tensorflow-community-wheels/issues/99)
* [Prebuilt binaries do not work with CPUs that do not have AVX instruction sets. #19584](https://github.com/tensorflow/tensorflow/issues/19584)
* [My CPU doesn't support Tensorflow AVX instructions #34](https://github.com/openai/gpt-2/issues/34)
* [TensorFlow - Build from source](https://www.tensorflow.org/install/source)
* [Wikipedia > CUDA > GPUs supported](https://en.wikipedia.org/wiki/CUDA#GPUs_supported)
* [CUDA Toolkit 9.0 Downloads](https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1704&target_type=runfilelocal)
* [Bazel 0.19.2](https://github.com/bazelbuild/bazel/releases/tag/0.19.2)
* [cuDNN 7 Manual](https://developer.download.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/Doc/cuDNN-Installation-Guide.pdf?3XnViXudgpO1wDx_qLlC-EW1BJHGwxpEDDYBXFUCKtjgc_18oxXgfG49FSZWck_m1FTa09g5GTk57LGYPb7jB5TgtAIOlIrZTCuPf1CIJC2VemxIh9kfrjlUGonMMLnztHttD5LT_oF3huMnNVju7jIW6ca10uW3dZ3kZOti9uIs7B3wSulhKi9sdDwZgdHzQw#%5B%7B%22num%22%3A19%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C108%2C275.369%2Cnull%5D)
* [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)


_____________________________________________________________________________

*If you have any corrections, recommendations or editions, please create issues*
