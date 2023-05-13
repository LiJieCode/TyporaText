# Conda Notes 

## Conda 常用命令

- **Conda信息**

  - <span style= "color:blue; font-weight:bold">查看</span>
    `conda --version`：查看当前conda版本
    `conda config --show`：查看conda所有的配置信息
    `conda create --help`：查看某个命令（例如create）的帮助信息

  - 更新
    `conda update conda`：将conda自身更新到最新版本
    `conda update Anaconda`：将整个Anaconda都更新到确保稳定性和兼容性的最新版本

  - 环境
    Conda允许你创建相互隔离的独立环境，这些环境被称之为**虚拟环境**（Virtual Environment），这些环境各自包含属于自己的文件、包以及他们的依存关系，并且不会相互干扰

    Anaconda有一个缺省的名为base的环境，但是不建议把程序放在base环境中，应该创建不同的虚拟环境分别管理不同的开发项目（不同项目可能用到相同的包，但版本不同）

  - 创建
    `conda create -n env_name python=3.8 -y`：创建一个名为env_name的虚拟环境，并指定python版本为3.8，且不需要询问（yes or no），直接创建。创建后，env_name文件可以在Anaconda安装目录envs文件下找到。在不指定python版本时，自动创建基于最新python版本的虚拟环境

  - 激活&退出
    `conda activate env_name`：激活（即进入）创建的虚拟环境

    `conda activate、conda deactivate`：回到base环境

    以上两条命令只中任一条都会让你回到base environment，它们从不同的角度出发到达了同一个目的地

    activate的缺省值是base

    deactivate的缺省值是当前环境

    因此它们最终的结果都是回到base

  - 查看
    `conda env list`
    `conda info -e`
    `conda info --envs`
    以上三条命令均可以查看有哪些环境（base和虚拟环境）

  - 删除
    `conda remove -n env_name --all`：将该指定虚拟环境及其中所安装的包全部删除
    `conda remove -n env_name package_name`：只删除虚拟环境中的某个或者某些包

- **包管理**

  - 查看
    `conda list`：查看当前环境中安装了哪些包
    `conda search package_name`：查看当前Anaconda Repository中是否有你想要安装的包（需要联网）

  - 安装&更新
    `conda install package_name`：在当前环境中安装一个包
    `conda install numpy=0.20.3`：指定安装包的版本
    `conda update numpy`：将某个包更新到最新版本

  - 删除
    `conda uninstall package_name`：将依赖于这个包的所有其它包也同时删除
    `conda uninstall package_name --force`：只删除指定包，不删除依赖该包的其他包（不推荐）

  - 清理缓存
    `conda clean -p`：删除没有用的包
    `conda clean -t`：删除tar打包
    `conda clean -y -all`：删除所有的安装包及cache（索引缓存、锁定文件、未使用过的包和tar包）

- **Python管理**

  - 查看

    `python --version`：查看当前Python版本

  - 更新

    `conda install python=3.9`：将版本变更到指定版本

    `conda update python`：将python版本更新到最新版本

- **镜像管理**

  - 清华源

  ```shell
  conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  conda config --set show_channel_urls yes
  # pytorch
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  # 安装时PyTorch，官网给的安装命令需要去掉最后的-c pytorch，才能使用清华源
  # conda-forge
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  # msys2
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
  # bioconda
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
  # menpo
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/
  # 设置搜索时显示通道地址
  conda config --set show_channel_urls yes
  ```

  - 中科大

  ```shell
  conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
  conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
  conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
  conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
  conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
  conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
  conda config --set show_channel_urls yes
  ```

- 其他文章

  - [Getting started with conda — conda 23.1.0.post22+31fe66bed documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html)
  - [ Anaconda conda常用命令：从入门到精通_笨牛慢耕的博客-CSDN博客_anaconda conda命令怎么用](https://blog.csdn.net/chenxy_bwave/article/details/119996001)
  - [conda常用命令:安装，更新，创建，激活，关闭，查看，卸载，删除，清理，重命名，换源，问题_阿尔发go的博客-CSDN博客_conda activate](https://blog.csdn.net/zhayushui/article/details/80433768)

## Anaconda相关

- [Conda常用命令及解释 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/501303675)

- 显示conda的配置信息

  `conda config --show`  找到channel，对应的就是我们的镜像配置

- 清华源 : [Index of /anaconda/ | 清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/)

  > 清华源的资源容易下载成cpu版本的pytorch

  ```
  # 添加清华镜像源
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  
  # 配置conda第三方源
  # pytorch
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  
  # 设置搜索时显示通道地址
  conda config --set show_channel_urls yes
  
  # 删除镜像源
  conda config --remove channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
  ```

  > C:\Users\Lxuan9897\.condarc
  >
  > 如果出现连接错误或者连接超时，输入以下命令，把里面的所有https改成http即可
  >
  > \.condarc  -   运行期配置文件
  >
  > > .condarc默认是不会自动创建的，只有当用户第一次使用`conda config`命令时，系统才会自动创建.condarc文件。

- 增加虚拟环境 & 删除虚拟环境

  `conda create -n py38 python=3.8` 其中，“py38”为环境名，可以随意改；”python=3.8“为指定python版本，可以随意改。

  `conda remove -n py38 --all` 其中，“py38”为要删除的环境名。

- 查看虚拟环境

  `conda env list`   或者   `conda info --env `

- 激活环境 & 退出环境

  `activate env_name` 激活环境     或者 `conda activate env_name`

  `deactivate` 退出环境     或者 `conda deactivate`

- 在当前环境中的操作

  `conda list`   安装了那些包

  `conda install package_name(包名)`  安装包

- 其他命令

  - conda info ：显示当先环境的基本信息
  - pip list : 查看环境中已经安装的包

> [Anaconda安装Pytorch镜像详细教程](https://www.jianshu.com/p/3bed91f4f3ad)

- <span style= "color:blue; font-weight:bold">不用清华源，直接安装pytorch</span>

  ```
  # 不用清华源，下列代码安装成功 - 
  conda install pytorch==1.12.0 torchvision==0.13.0 torchaudio==0.12.0 cudatoolkit=11.6 -c pytorch -c conda-forge  
  
  
  # 检查pytorch是否安装成功、查看torch和cuda的版本
  >python 
  >>>import torch # 如果pytorch安装成功即可导入
  >>>print(torch.cuda.is_available()) # 查看CUDA是否可用
  True
  >>>print(torch.cuda.device_count()) # 查看可用的CUDA数量
  1
  >>>print(torch.version.cuda) # 查看CUDA的版本号
  '11.6'
  ```





