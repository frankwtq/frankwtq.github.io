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