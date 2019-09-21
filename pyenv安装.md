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
