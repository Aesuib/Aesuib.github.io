---
export_on_save:
  pandoc: true
title: "在国产麒麟操作系统上如何安装ONLYOFFICE Docs 7.3"
author: 天哥
date: Feb 2, 2023
output: word_document
---
# 在国产麒麟操作系统上如何安装ONLYOFFICE Docs 7.3

![](题头图.png)

在二月初，ONLYOFFICE发布更新了最新的7.3版本。新版本提供了高级表单、SmartArt图形插入、增强密码保护和公式计算、幻灯片特殊粘贴项等多项新功能。同时发布了服务器端的文档服务器和客户端的桌面编辑器的最新7.3版本。

![](ServerAndClient.drawio.png)

这里仅仅介绍其服务器端的文档服务器如何在国产的麒麟操作系统上安装，而客户端的安装使用下一期再仔细讲解。互联网行业中，服务器端基本上都是用Linux操作系统作为服务器，国内比较专业的同行都会比较关心ONLYOFFICE的文档服务器是否能在国产的Linux发行版本上面安装，这里就可以明确的告诉大家，这是可以的，请往下看。至于Linux操作系统如何安装部署，选择真实物理计算机还是在虚拟机软件里面安装，安装桌面环境还是不安装桌面环境仅仅安装为服务器模式，Linux安装好后一般都要先安装那些必要的软件源，等等Linux的基础问题，我都写在另外一篇攻略图文里面了。

// 插入链接

## 安装ONLYOFFICE文档服务器的系统需求：

|            |                                                              |
| ---------- | ------------------------------------------------------------ |
| CPU        | 双核2Ghz                                                     |
| 内存       | 2G                                                           |
| 硬盘       | 40G                                                          |
| SWAP       | 4G                                                           |
| OS         | 64位Debian、Ubuntu或其他发行版，内核版本号3.13以上 |
| PostgreSQL | 12.9                                                         |
| NGINX      | 1.3.13                                                       |
| libstdc++6 | 4.8.4                                                        |
| RabbitMQ   |                                                              |

## 使用终端文字符

这里假定你已经安装好了国产的麒麟操作系统，在该电脑上安装ONLYOFFICE Docs文档服务器。我从官方网站下载的麒麟操作系统安装光盘默认安装Desktop桌面环境，既来之则安之，我也就默认安装了桌面环境，因此下面的众多截图你们可以看见是在桌面环境下，但即使如此，大部分操作也还是在桌面环境下打开的终端程序里面来操作的，如下图所示从开始菜单找到Mate终端打开：

![](VirtualBox_AnotherPC_03_02_2023_19_22_07.png)

作为服务器的正经操作，应该是远程通过terminal类程序ssh登陆服务器在终端中各种操作。

## 在线安装指南

首先是在麒麟操作系统自带的软件市场里面搜一下，有没有上架ONLYOFFICE的文档服务器软件，如果能搜到那就直接点击安装是最简单的了，然而并没有搜索到，作为对比，另一款国产Linux，深度操作系统的软件市场是能搜索到ONLYOFFICE的，更为方便，那么，麒麟操作系统下就需要选择自己手动安装ONLYOFFICE了，按照一般的Debian、Ubuntu系列的发行版的方式来安装，在ONLYOFFICE官方网站找到服务器端下载安装页面：

[ONLYOFFICE Docs Community](https://www.onlyoffice.com/download-docs.aspx?from=default#docs-community)

![img](Screenshot_2023-02-03_at_19-13-52_Download_ONLYOFFICE_Docs_ONLYOFFICE.png)

选择第二条，在Debian、Ubuntu及其派生发行版上安装，选择Intel的CPU，点击后打开其安装指南网页页面按照说明执行安装：

[Installing ONLYOFFICE Docs Community Edition for Debian, Ubuntu, and derivatives](https://helpcenter.onlyoffice.com/installation/docs-community-install-ubuntu.aspx?_ga=2.136308209.110839153.1675419797-433964955.1670329690)

![](Screenshot_2023-02-03_at_19-15-47_Installing_ONLYOFFICE_Docs_for_Debian_Ubuntu_and_derivatives_-_ONLYOFFICE.png)

纯英文的看不懂？中文版本的可以参考上一个版本7.2版本的安装攻略：

[如何在 Fedora Linux 上安装 ONLYOFFICE Docs 7.2](https://mp.weixin.qq.com/s?__biz=MzI2MjUyNzkyNw==&mid=2247503100&idx=1&sn=c98e427295781ec40e77291b72f705d4&chksm=ea4b4224dd3ccb324863728afdbd9de470dfff5e1709bf7f3ef518d81a6abc83c71d466f78f2#rd)

安装过程大同小异，小异的意思是说，Linux下面安装软件，每次安装都会有各种各样意想不到的小问题让你自己去搜索解决，比如我在安装过程中遇到了没有公钥无法验证签名的错误，于是架好了木弟子Goo歌搜到了这一篇：

![](Screenshot_2023-02-03_at_20-21-59_更新linux时候提示无法“由于没有公钥，无法验证下列签名_”的解决方案_sanbo_xyz的博客-CSDN博客.png)

照此办理解决问题。

## 安装依赖项

按照上述官网安装手册网页说明，先安装所依赖的软件*postgresql*：

![](VirtualBox_AnotherPC_03_02_2023_19_23_13.png)

输入root管理员的密码继续

![](VirtualBox_AnotherPC_03_02_2023_19_23_58.png)

直接找不到postgresql，看来麒麟操作系统本身的官方软件源还缺少这样的真正生产力工具类的软件的，稍微吐槽一下国内的某些扯大旗的老板们还是不太务实啊。

![](VirtualBox_AnotherPC_03_02_2023_19_27_25.png)

update刷新一下官方源最后尝试一下还是不行，于是打开软件源配置文件，做好备份，准备修改添加其它更好用的更快的国内软件源，比如163的、大清的、阿里的等等
![img](VirtualBox_AnotherPC_03_02_2023_19_40_21.png)

截图中的都是Linux终端下的基本常用命令了，这里就不解释了，这篇图文攻略不再给你补习Linux基本技能。

![img](VirtualBox_AnotherPC_03_02_2023_19_41_21.png)

用世界上最好的代码编辑器VIM来修改软件源配置文件，不服来辩
![img](VirtualBox_AnotherPC_03_02_2023_19_49_20.png)

加入大清的软件源，大清的软件源的配置代码在这里：

[Ubuntu 镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

![img](Screenshot_2023-02-03_at_19-39-20_ubuntu_镜像站使用帮助_清华大学开源软件镜像站_Tsinghua_Open_Source_Mirror.png)

原有的麒麟软件源先不删除而是注释掉，保存退出

![img](VirtualBox_AnotherPC_03_02_2023_19_50_07.png)

确认修改成功后再次update刷新一下，国内的各大软件源最起码在网络速度上都是很快的
![img](VirtualBox_AnotherPC_03_02_2023_19_50_53.png)

然而刷新失败
![img](VirtualBox_AnotherPC_03_02_2023_19_51_59.png)

搜索一番得到解决方式是加入签名

![img](Screenshot_2023-02-03_at_20-22-28_ubuntu_apt_update报错：由于没有公钥，无法验证下列签名_GDB_er的博客-CSDN博客.png)

我再换用阿里源尝试一下
![img](VirtualBox_AnotherPC_03_02_2023_20_19_17.png)

终于把麒麟操作系统的软件源配置好了，接下来安装各种生产力软件就应该都不会出太多问题了，执行下面命令安装postgresql：

```bash
sudo apt-get install postgresql
```


![img](VirtualBox_AnotherPC_03_02_2023_20_20_24.png)

*postgresql*安装好后创建并配置ONLYOFFICE文档服务器的数据库和系统用户：

```bash
sudo -i -u postgres psql -c "CREATE DATABASE onlyoffice;"
sudo -i -u postgres psql -c "CREATE USER onlyoffice WITH password 'onlyoffice';"
sudo -i -u postgres psql -c "GRANT ALL privileges ON DATABASE onlyoffice TO onlyoffice;"
```


![img](VirtualBox_AnotherPC_03_02_2023_20_26_06.png)

然后安装ONLYOFFICE依赖的另一个软件：*rabbitmq-server*兔子服务器

```bash
sudo apt-get install rabbitmq-server
```


![img](VirtualBox_AnotherPC_03_02_2023_20_27_09.png)

这个下载数据量如果使用国外的软件源，在现在的网速下你可以先去看一集电视剧狂飙了，再安装*nginx-extras*

```bash
sudo apt-get install nginx-extras
```


![img](VirtualBox_AnotherPC_03_02_2023_20_28_39.png)

## 可以设置不同的端口号

如果你的文档服务器上的端口号80已经被其他服务占用了，那么你可以修改ONLYOFFICE服务器的端口号

```bash
echo onlyoffice-documentserver onlyoffice/ds-port select <PORT_NUMBER> | sudo debconf-set-selections
```

在该命令中把 `<PORT_NUMBER>`替换为你要修改到的端口号即可。

如果要改变设置https端口号，不要改到443，请参考下列手册配置：

[Switching ONLYOFFICE Docs to HTTPS protocol](https://helpcenter.onlyoffice.com/installation/docs-community-https-linux.aspx)

## 安装GPG key密钥

```bash
mkdir -p -m 700 ~/.gnupg
gpg --no-default-keyring --keyring gnupg-ring:/tmp/onlyoffice.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CB2DE8E5
chmod 644 /tmp/onlyoffice.gpg
sudo chown root:root /tmp/onlyoffice.gpg
sudo mv /tmp/onlyoffice.gpg /usr/share/keyrings/onlyoffice.gpg
```

![img](VirtualBox_AnotherPC_03_02_2023_20_32_16.png)
![img](VirtualBox_AnotherPC_03_02_2023_20_34_42.png)
![img](VirtualBox_AnotherPC_03_02_2023_20_36_21.png)

## 安装ONLYOFFICE DOCS文档服务器

添加ONLYOFFICE DOCS官方软件源

```bash
echo "deb [signed-by=/usr/share/keyrings/onlyoffice.gpg] https://download.onlyoffice.com/repo/debian squeeze main" | sudo tee /etc/apt/sources.list.d/onlyoffice.list
```

![img](VirtualBox_AnotherPC_03_02_2023_20_38_06.png)

刷新软件源：

```bash
sudo apt-get update
```

安装mscorefonts

```bash
sudo apt-get install ttf-mscorefonts-installer
```

![img](VirtualBox_AnotherPC_03_02_2023_20_39_14.png)

安装ONLYOFFICE DOCS：

```bash
sudo apt-get install onlyoffice-documentserver
```

![img](VirtualBox_AnotherPC_03_02_2023_20_40_19.png)

看到提示它将下载这么大体积的数据，是不是就可以离开电脑去看电视剧狂飙了呢？不要走开！因为这个安装过程中会出现这么一个对话框需要手动填写继续的：

![img](VirtualBox_AnotherPC_03_02_2023_20_44_43.png)

输入之前安装依赖项postgresql时候创建的数据库的名称和密码，如果严格按照此片攻略操作没有设定不同的密码的话，是onlyoffice，确认下一步后稍后即可安装完成。

![img](VirtualBox_AnotherPC_03_02_2023_20_48_45.png)

装好后如何查看使用呢？自己的麒麟操作系统是安装了桌面环境的，于是打开自带的火狐浏览器，输入本地地址*http://localhost*即可打开ONLYOFFICE DOCS文档服务器的欢迎首页了：

![img](VirtualBox_AnotherPC_03_02_2023_20_51_24.png)

如果是通过纯文字终端安装在服务器上，从本地客户端打开网页浏览器访问服务器，则需要在服务器端输入ip地址查询命令ifconfig来查询服务器的ip：

![img](VirtualBox_AnotherPC_03_02_2023_20_53_10.png)

如果想先测试编辑器功能，请点击“Go to test example”按钮。这将会打开一个网页，在这里就可以创建示例内容文档（不要在这个环境下写入真实生产环境敏感数据）

ONLYOFFICE DOCS 7.3文档服务器最终完成！现在就可以把ONLYOFFICE Docs集成到你现有的服务平台上了，并开始在网络文档上协同编辑了！

## 参考文献：
