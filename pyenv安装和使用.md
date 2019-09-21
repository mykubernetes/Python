1、安装git
```
# yum install git -y
```  

2、安装Python编译依赖
```
# yum -y install gcc make patch gdbm-devel openssl-devel sqlite-devel readline-devel zlib-devel bzip2-devel
```  
3、创建用户python
```
# useradd python
# passwd python
```  

4、使用python用户登录后安装Pyenv
```
# su python
$ curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```  
注意：  
1、在 https://github.com/pyenv/pyenv-installer 有安装文档  
2、如果curl出现 curl: (35) SSL connect error ，是nss版本低的问题，更新它。 可能需要配置一个有较新包的yum源  
```
[updates]
name=CentOS-Updates
baseurl=https://mirrors.aliyun.com/centos/6.9/os/x86_64
gpgcheck=0


然后更新nss
# yum update nss
```  

5、在python用户的~/.bash_profile中追加  
```
$ vim ~/.bash_profile
export PATH="/root/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

重载环境变量
$ source ~/.bash_profile
```  

6、验证是否正确安装  
```
$ python --version
Python 2.7.5

$ python -V
Python 2.7.5

$ echo $PATH
/root/.pyenv/plugins/pyenv-virtualenv/shims:/root/.pyenv/shims:/root/.pyenv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin:/root/bin
```  

7、pyenv命令  
```
# pyenv
pyenv 1.2.13
Usage: pyenv <command> [<args>]

Some useful pyenv commands are:
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   which       Display the full path to an executable
   whence      List all Python versions that contain the given executable

See `pyenv help <command>' for information on a specific command.
For full documentation, see: https://github.com/pyenv/pyenv#readme
```  

8、查看pyenv可用版本  
```
$ pyenv help install 

列出所有可用版本 
$ pyenv install --list
``` 

9、通过pyenv的可用版本安装python3.5.3版本  
```
# pyenv install 3.5.3 -v
```  

10、查看当前版本和所有版本  
```
查看当前版本
$ pyenv version
system (set by /root/.pyenv/version)

查看所有版本，发现带*号的为当前版本
$ pyenv versions
* system (set by /root/.pyenv/version)
  3.5.3
  
切换版本
$ mkdir test/projects/cmdb -p
$ cd test/projects/cmdb/
$ pyenv local 3.5.3
查看pyenv版本
$ pyenv version
3.5.3 (set by /root/test/projects/.python-version)
查看python版本
$ python -V
Python 3.5.3
```  
- global 全局设置 作用域全局，切换后会导致所有shell都会切换，禁用
- shell 会话设置 影响只作用于当前会话
- local 本地设置 使用pyenv local设置从当前工作目录开始向下递归都继承这个设置


Virtualenv 虚拟环境设置  
需要对版本和包管理进行隔离，以免冲突，通过Virtualenv插件  
```
$ cd test/projects/cmdb
$ pyenv virtualenv 3.5.3 test353
Requirement already satisfied: setuptools in /root/.pyenv/versions/3.5.3/envs/test353/lib/python3.5/site-packages
Requirement already satisfied: pip in /root/.pyenv/versions/3.5.3/envs/test353/lib/python3.5/site-packages


$ pyenv versions
* system (set by /root/test/projects/.python-version)
  3.5.3
  3.5.3/envs/test353    #新加隔离环境
  3.6.1
  test353               #新加隔离环境

切换隔离环境
$ pyenv  local test353
(test353) [root@node01 cmdb]$
```  
