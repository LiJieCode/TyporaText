# DLNotes

## remark

- cmd --> conda list : 列举anaconda安装的库
- [显卡天梯图|最新版 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/133845310)







## Pytorch 开发环境安装

- anaconda安装
  - [Anaconda官网](https://www.anaconda.com/)
- CUDA的下载与安装
  - [CUDA Toolkit 11.8 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64)
  - [CUDA的下载与安装](https://blog.csdn.net/David_house/article/details/125314103)
  - 安装默认位置：C:\Program Files\NVIDIA Corporation
  - cmd --> nvcc -V  ：查看安装版本
  - cmd --> nvidia-smi：也可以查看CUDA的版本
- Pytorch下载安装
  - [Start Locally | PyTorch](https://pytorch.org/get-started/locally/#windows-prerequisites)
  - conda install pytorch torchvision torchaudio pytorch-cuda=11.6 -c pytorch -c nvidia
  - [pytorch安装保姆级教程及安装缓慢的解决方案（超时Timeout导致安装失败解决方案）_wendy_ya的博客-CSDN博客_pytorch安装慢](https://blog.csdn.net/didi_ya/article/details/107841714)（没验证是否可行？？？）



```shell
# 查看conda clean使用参数
$ conda clean -H
usage: conda clean [-h] [-a] [-i] [-l] [-p] [-t] [-f]
                   [-c TEMPFILES [TEMPFILES ...]] [-d] [--json] [-q] [-v] [-y]

Remove unused packages and caches.

Options:

optional arguments:
  -h, --help            Show this help message and exit.

Removal Targets:
  -a, --all             Remove index cache, lock files, unused cache packages,
                        and tarballs.
  -i, --index-cache     Remove index cache.
  -l, --lock            Remove all conda lock files.
  -p, --packages        Remove unused packages from writable package caches.
                        WARNING: This does not check for packages installed
                        using symlinks back to the package cache.
  -t, --tarballs        Remove cached package tarballs.
  -f, --force-pkgs-dirs
                        Remove *all* writable package caches. This option is
                        not included with the --all flag. WARNING: This will
                        break environments with packages installed using
                        symlinks back to the package cache.
  -c TEMPFILES [TEMPFILES ...], --tempfiles TEMPFILES [TEMPFILES ...]
                        Remove temporary files that could not be deleted
                        earlier due to being in-use. Argument is path(s) to
                        prefix(es) where files should be found and removed.

Output, Prompt, and Flow Control Options:
  -d, --dry-run         Only display what would have been done.
  --json                Report all output as json. Suitable for using conda
                        programmatically.
  -q, --quiet           Do not display progress bar.
  -v, --verbose         Can be used multiple times. Once for INFO, twice for
                        DEBUG, three times for TRACE.
  -y, --yes             Do not ask for confirmation.

Examples:

    conda clean --tarballs
```





























