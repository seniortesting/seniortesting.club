---
title: Python Linux安装及其环境配置
categories: []
abbrlink: VsD26t2JsS
date: 2021-04-05 09:52:55
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210419092310.png
---


## Python2.7 installaction [更新到2019年9月1日]

参考网站地址: [安装Python2.7](https://tecadmin.net/install-python-2-7-on-ubuntu-and-linuxmint/)
命令如下:

```shell
sudo wget https://www.python.org/ftp/python/2.7.16/Python-2.7.16.tgz
sudo tar xzf Python-2.7.16.tgz
cd Python-2.7.16
sudo ./configure --enable-optimizations
sudo make altinstall 
```

`make altinstall` is used to prevent replacing the default python binary file /usr/bin/python.

## Python3.8 apt安装步骤【更新2020年02月22日】

01. Run the following commands as root or user with sudo access to update the packages list and install the prerequisites:

```shell
sudo apt update
sudo apt install software-properties-common
sudo apt install dirmngr
```

02. Add the deadsnakes PPA to your system’s sources list,参考仓库：<https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa>

```shell
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
```

When prompted press Enter to continue:

```shell
Press [ENTER] to continue or Ctrl-c to cancel adding it.
```

03. Once the repository is enabled, install Python 3.8 with:

```shell
sudo apt install python3.8
```

04. Verify that the installation was successful by typing:

```
python3.8 --version
```

## Python3.8 installation [更新到2019年8月10日]

[How to Install Python 3.7 on Debian 9](https://linuxize.com/post/how-to-install-python-3-7-on-debian-9/)
[Modify python command](https://jcutrer.com/linux/upgrade-python37-ubuntu1810)

```shell script
$ sudo apt-get purge  python3 -y
$ sudo apt-get purge --auto-remove python3 -y
$ whereis python3 python3.5
$ sudo apt update
$ sudo apt install make build-essential libssl-dev zlib1g-dev bzip2 libbz2-dev liblzma-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev  libncursesw5-dev libc6-dev libgdbm-dev libnss3-dev libffi-dev xz-utils openssl git tk-dev

    以下的包bzip2 libbz2-dev解决问题: pip.exceptions.DistributionNotFound: No matching distribution found for Twisted,主要是因为如果包是：tar.bz2则pip不能安装
$ sudo apt-get install bzip2 libbz2-dev
    lxml安装出错误:  make sure the development packages of libxml2 and libxslt are installed 
$ sudo apt install libxml2-dev libxslt-dev
$ wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tar.xz
$ tar -xf Python-3.8.1.tar.xz
$ cd Python-3.8.1
$ ./configure --enable-optimizations --enable-ipv6 --enable-loadable-sqlite-extensions
$ nproc
$ make -j 8  / make -j 4
$ sudo make altinstall
$ python3.9 -V
$ ls /usr/bin/python*
$ update-alternatives --list python
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
$ sudo update-alternatives --install /usr/bin/python python /usr/local/bin/python3.8 2
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.8 2
$ update-alternatives --list python
$ update-alternatives --config python

```

## `pip`, `pipenv` installation

[How to install Pip](https://linuxize.com/post/how-to-install-pip-on-debian-9/)

[How to install pipenv](https://www.ostechnix.com/pipenv-officially-recommended-python-packaging-tool/)

1. `pip` 安装

```shell script
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
```

如果出现错误： Command '('lsb_release', '-a')' returned non-zero
参考 (<https://stackoverflow.com/questions/44967202/pip-is-showing-error-lsb-release-a-returned-non-zero-exit-status-1>)，
使用命令： `sudo nano  /usr/bin/lsb_release`
edited the first line from #! /usr/bin/python3 to #! /usr/bin/python3.7

```
如果出错：Package 'python3-distutils' has no installation candidat

执行如下命令确认pip对应的python版本是2.7还是3.8
$ pip -V

```

如果出现错误： ImportError: cannot import name 'main' from 'pip'，因为`pip`使用的是python2.7的命令，所以应该参考如下： <https://stackoverflow.com/questions/44455001/how-to-change-pip3-command-to-be-pip/44455078>

```
pip3 -V
alias pip=pip3
sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

```

## 切换python镜像源

a）Linux下，修改`~/.pip/pip.conf`(没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹,root用户安装时目录为：`/root/.config/pip/pip.conf`)
内容如下：

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
```

(b) windows下，直接在user目录中创建一个pip目录，如：`C:\Users\xx\pip`，然后新建文件`pip.ini`，即 `%HOMEPATH%\pip\pip.ini`，在`pip.ini`文件中输入以下内容（以豆瓣镜像为例）：

```
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host = pypi.douban.com
```

(c) 如果是使用的`pipenv`,则可以在脚本目录下面修改`Pipfile`,修改为对应的镜像地址。

常用镜像地址列表:

1. <https://pypi.tuna.tsinghua.edu.cn/simple>
2. <http://pypi.douban.com/simple>

3.

## pip install --upgrade升级安装包

例如需要升级安装scrapy为2.0，如下：

```shell
pip install --upgrade scrapy
```

如果需要升级pip包，如下：

```shell
python -m pip install --upgrade pip
```

## `pipenv`安装及常用命令

## pipenv命令操作

2020年0826永久更新改变默认的pipenv的路径：

在windows下使用pipenv shell时，虚拟环境文件夹会在C：\Users\Administrator\.virtualenvs\目录下默认创建，为了方便管理，将这个虚环境的文件的位置更改一下。

新建一个名为“ **WORKON_HOME** ”的环境变量（如果已存在就忽略此步骤），然后将环境变量的值设置为“ **.virtualenvs** ”

以后所有的虚拟环境都会在当前python项目下面创建一个.virtualenvs目录。

```
$ pip install --user pipenv
$ python -m site --user-base
$ sudo nano ~/.profile
 export PATH="$HOME/.local/bin:$PATH"
$ sudo source ~/.profile
$ . /etc/profile
$ pipenv --version

常用pipenv命令
$ pipenv --update
$ export PIPENV_VENV_IN_PROJECT=1 (for linux) / SET PIPENV_VENV_IN_PROJECT=1(for windows)
$ pipenv shell
$ pipenv install / pipenv install -r requirements.txt
$ pipenv lock -r  (export to requirement.txt文件)
$ pipenv update
$ pipenv graph

```

## 安装配置问题

- zipimport.ZipImportError: can't decompress data; zlib not available 解决办法

参考解决方案[zipimport.ZipImportError: can't decompress data; zlib not available 解决办法](https://www.cnblogs.com/zhangym/p/6226435.html)

- Microsoft Visual C++ 14.0 is required

python3 是用 VC++ 14 编译的, python27 是 VC++ 9 编译的, 安装 python3 的包需要编译的也是要 VC++ 14 以上支持的.
Visual Studio 2013 ---> 12
Visual Studio 2015 ---> 14
Visual Studio 2017 ---> 15

## requests报错 RequestsDependencyWarning: urllib3 (1.25.10) or chardet (3.0.4) doesn't match a supported version

```
pip install --upgrade requests

```

## THESE PACKAGES DO NOT MATCH THE HASHES FROM THE REQUIREMENTS FILE. If you have updated the package versions, please update the hashes. Otherwise, examine the package contents carefully; someone may have tampered with them

这个问题主要是在使用pipenv命令进行安装twisted出现的:

```
pipenv install "C:\Users\Administrator\Downloads\Twisted-20.3.0-cp38-cp38-win32.whl"
```

解决方法是首先进入pipenv环境，然后替换使用pip命令进行更新操作：

```
> pipenv shell
> pip install --upgrade "C:\Users\Administrator\Downloads\Twisted-20.3.0-cp38-cp38-win32.whl"
或者
> pip install --no-cache-dir "C:\Users\Administrator\Downloads\Twisted-20.3.0-cp38-cp38-win32.whl"
```

## ImportError: attempted relative import with no known parent package

Pycharm或者编译器打开项目，过多一层或者过少一层打开目录都会导致导入错误，是因为编译器打开那个目录，就将python的工作目录设置那一层，只有正确的目录结构才能导入正确包。

. 和 ..导入 相对位置是执行文件的当前目录

因为python的相对导入需要用到父级包作为相对的参考位置
而这个位置是通过__name__属性和__package__属性进行决定的，
当 __name__ 等于 __main__和 __package__ = None的时候导致的问题没有父级包
