
# 如何用VirtualBox虚拟机安装国产麒麟深度操作系统

不打嘴炮，这里开始折腾国产操作系统，麒麟和深度，而不去谈论评论这两款操作系统涉及嘴仗的东西。一说起虚拟机软件那就必然是VMware，但是个人使用的话，那只能找破解盗版的，对于我这样有洁癖的程序员，那就绝对推荐个人可以免费使用的VirtualBox这个开源软件。

首先是在深度和麒麟的官方网站下载到这两个操作系统的.iso安装光盘映像文件：

![](isos.png)

好在国产操作系统的官方网站都是中文的，这绝对比那些国外的Linux网站友好多了

在VirtualBox里面新建一个虚拟机：

![](New一个VM.png)

如上图所示，在ISOImage栏内选择已经下载到本地的Linux光盘映像文件，然后下一步：

![](CPU与内存.png)

主机硬件性能高这里就可以高配一些，主机性能低的话这里就配置低一些

![](new一个harddisk.png)

为虚拟机创建一块虚拟硬盘，分配大了就会浪费，分配小了又怕不够用，比较纠结，我按照经验分配20G，说G不说吧，文明你我他

![](摘要.png)

上述配置再确认一下，最后一次反悔的机会，点击下一步就真的开始创建这台虚拟机了：

![](creating.png)

别忘了可以在虚拟机的描述里面随便写写，我一般是在虚拟机系统安装好之后，在这里记录下给虚拟机系统设置的用户名和密码，方便以后使用虚拟机的时候不会忘了登陆密码

![](描述.png)

然后就可以点击右上角的启动按钮给虚拟机开机：

![](AnotherPC.png)

![](启动啊.png)

注意看virtualbox虚拟机软件提示的操作切换键，一旦键盘鼠标把热点切换进虚拟机内，那么如何再切出虚拟机回到主机操作呢？就是有一个关键的切换键，在virtualbox里面默认的是右的ctrl按键

![](启动完.png)

![](rightctrl.png)

![](虚拟机截图操作.png)

![](VirtualBox_AnotherPC_03_02_2023_17_22_50.png)

![](VirtualBox_AnotherPC_03_02_2023_17_26_16.png)

![](VirtualBox_AnotherPC_03_02_2023_17_27_12.png)

![](VirtualBox_AnotherPC_03_02_2023_17_28_26.png)

![](VirtualBox_AnotherPC_03_02_2023_17_45_01.png)

![](VirtualBox_AnotherPC_03_02_2023_17_46_01.png)

![](VirtualBox_AnotherPC_03_02_2023_17_46_32.png)

![](VirtualBox_AnotherPC_03_02_2023_17_47_15.png)

![](VirtualBox_AnotherPC_03_02_2023_17_53_23.png)

![](弹出光盘.png)

![](强弹.png)htt

![](reboot.png)

![](硬重启.png)

![](VirtualBox_AnotherPC_03_02_2023_18_14_25.png)

![](VirtualBox_AnotherPC_03_02_2023_18_15_25.png)

![](VirtualBox_AnotherPC_03_02_2023_18_16_07.png)

![](VirtualBox_AnotherPC_03_02_2023_18_22_36.png)



