# Untitled





$y=\left\{\begin{array}{ll}
\sqrt{x}, & x<10 \\
x^{2}, & 10 \leq x<12 \text { 或 } x>15 \\
2 x+1,& 12 \leq x \leq 15
\end{array}\right.$















<img src="./002.jpg" alt="image" style="zoom: 80%;" />













````
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main


sudo yum install -y gcc gccc++ libffi-devel python-devel python-pip python-wheel pythonsetuptools openssl-devel cyrus-sasl-devel openldap-devel

pip install --upgrade setuptools pip -i https://pypi.douban.com/simple/

pip install apache-superset -i https://pypi.douban.com/simple/
pip install apache-superset --trusted-host https://repo.huaweicloud.com -i https://repo.huaweicloud.com/repository/pypi/simple


pip install cryptography==3.3.2 -i https://repo.huaweicloud.com/repository/pypi/simple



# pip 是 python 的包管理工具，可以和 centos 中的 yum 类比

# 

# 扩容：
lvextend -L +99.8G /dev/mapper/centos-root
lvresize -L +99.9G /dev/mapper/centos-root

pvdisplay

lvextend -l +100%FREE /dev/mapper/centos

````













<img src="./001.jpg" alt="image" style="zoom: 80%;" />







