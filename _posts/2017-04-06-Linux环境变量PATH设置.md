#Linux环境变量PATH设置

* 由来：安装RVM时，由于使用的是zsh的shell，所以需要设置环境变量才能正常启动RVM。所以了解了一下Linux中环境变量的设置，以便后面再遇到类似的问题能够很快解决。
  
## 参考资料：  
* 博客[峰子_仰望阳光](http://www.cnblogs.com/xiehongfeng100/)的博文[Linux中环境变量设置](http://www.cnblogs.com/xiehongfeng100/p/4969477.html)  
  
* 博文[/etc/profile文件详解](http://blog.chinaunix.net/uid-25749806-id-298287.html)  
  
* 博文[ Linux中profile、bashrc、bash_profile之间的区别和联系](http://blog.csdn.net/chenchong08/article/details/7833242)
   
## 相关背景  
* Linux是一个多用户的操作系统。每个用户登录系统后，都会有一个专用的运行环境。通常每个用户默认的环境都是相同的，这个默认环境实际上就是一组环境变量的定义。用户可以对自己的运行环境进行定制，其方法就是修改相应的系统环境变量。
  
## 相关文件介绍  
* /etc/profile:此文件为系统的每个用户设置环境信息，当用户第一次登录时，该文件被执行。在这里修改的内容是对所有用户起作用的。所以如果你有对/etc/profile有修改的话必须得重启系统，你的修改才会生效，此修改对每个用户都生效。
  
* /etc/bashrc:为每一个运行 bash shell 的用户执行此文件。当 bash shell 被打开时，该文件被读取。如果你想对所有的使用bash的用户修改某个配置并在以后打开的bash都生效的话可以修改这个文件，修改这个文件不用重启，重新打开一个bash即可生效。
  
* ~/.bash_profile: 每个用户都可使用该文件输入专用于自己使用的 shell 信息，当用户登录时，该文件仅仅执行一次。此文件类似于/etc/profile，也是需要需要重启才会生效，/etc/profile对所有用户生效，~/.bash_profile只对当前用户生效。  
  
* ~/.bashrc:该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该文件被读取.（每个用户都有一个.bashrc文件，在用户目录下，符号‘~’就表示用户目录）  
  
* ~/.bash_logout:当每次退出系统(退出bash shell)时,执行该文件。
   
/etc/profile和/etc/bashrc都是系统级别的，修改后可以在所有用户中起作用；~/.bash_profile、~/.bashrc和~/.bash_logout都是用户级别的，修改后只会作用于当前用户。  
  
带profile的文件都是需要重新进入用户时才会生效，带bashrc的则是打开新的shell时生效；  
  
## 启动过程  
  
执行顺序：/etc/profile -> (~/.bash_profile | ~/.bash_login | ~/.profile) -> ~/.bashrc -> /etc/bashrc -> ~/.bash_logout  
  
## Linux环境变量相关命令  
  
* 显示环境变量HOME  
  
``` $ echo $HOME ```  
  
* 设置新的环境变量HELLO  
  
``` $ export HELLO="Hello" ```  
  
* 显示所有环境变量  
  
``` $ env ```  
  
* 显示所有本地定义的Shell变量   
  
··· ￥ set ```  
  
* 清除环境变量  
  
```
$ export TEST="test"
$ env|grep TEST #此时显示：TEST =test  
$ unset $TEST
$ env|grep TEST #此时已经没有显示了，说明没有对应的环境变量了
```  
  
* 设置只读变量  
  
``` readonly TEST ```  
  
## 设置Linux环境变量  
之前介绍的使用**export**命令设置环境变量是在命令行中直接执行，这样设置的环境变量在退出shell时就会失效。要想设置永久有效的环境变量就需要修改之前提到的文件。  
  
### PATH声明  
```  PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N> ```    
你可以自己加上指定的路径，中间用冒号隔开
需要注意的是，最好不要把当前路径”./”放到PATH里，这样可能会受到意想不到的攻击。  

### 举例：在/etc/profile文件中添加环境变量  
   
特点：所有用户；永久有效；生效需要重新进入用户  
root权限：  
```
# vim /etc/profile
export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib
```  
要想修改完文件后就立即生效，可以在命令行中执行：  
``` # source /etc/profile ```  
Source命令也称为“点命令”，也就是一个点符号（.）。source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录
  
## 常用环境变量  
* PATH 决定了shell将到哪些目录中寻找命令或程序
* HOME 当前用户主目录
* HISTSIZE 历史记录数
* LOGNAME 当前用户的登录名
* HOSTNAME 指主机的名称
* SHELL 当前用户Shell类型
* LANGUGE 语言相关的环境变量，多语言可以修改此环境变量
* MAIL 当前用户的邮件存放目录
* PS1 基本提示符，对于root用户是#，对于普通用户是$