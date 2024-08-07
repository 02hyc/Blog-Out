---
title: "再建 Arch Linux"
categories:
  - Arch Linux
tags:
  - Arch Linux, VMWare Workstation Pro
---

## 和 Arch Linux 的渊源纠葛

在大一入学后，我开始接触到了 Linux 操作系统，觉得这种命令行交互的方式很酷炫（程序员不就应该咔咔敲键盘吗）。但是最开始我也只知道 Ubuntu、Centos 这种发行版本，对于 Arch Linux 几乎没有了解过。恰好我有个学长在某一天无意间给我展示了他的桌面，酷似苹果的 UI 瞬间给我种了草（虽然桌面 UI 和发行版没啥关系），他的系统正是 Arch Linux。于是乎我就想开始尝试安装自己安装一下 Arch Linux，这个号称最难安装、可玩性最高、软件包维护方便的 Linux 版本。

其实在去年几乎同一时间，我已经在 VMWare Workstation Pro 上成功安装过 Arch Linux，但由于虚拟机性能有限，再加上当时只是无脑跟着教程走了一遍（~~虽然这遍也是跟着教程无脑走的~~），再加上当时 pacman 包给我留下了鱼龙混杂的印象，总的来说使用体验不如我另一台 Ubuntu20.04 的虚拟机。为了再体验一下 Arch Linux 的魅力（其实只是下午摸鱼，但弄得我头昏脑胀，已经远远超出摸鱼的范畴了），我今天就又尝试安装一个 Arch Linux 的虚拟机，给我将来刷物理机做准备。

好吧，不得不事先声明一下，其实今天安装失败了说是，属于是白忙活一下午，看到这里的读者已经可以退出了==

![](https://box.nju.edu.cn/f/73a386297ec94030b9a9/?dl=1)

## 动机

除了上述原因之外，这两天在 Westlake University 的服务器上下 python 包的时候，连接 pypl 官方镜像很不稳定，网上常用的镜像源是清华源、中科大源、阿里源。但我突然想到，我们南大不也有镜像仓库吗，为什么我们南大学生清一色都是换的清华源或中科大源呢？本着物尽其用的原则，于是我就给服务器换上了南大源，让我自豪地挺起了胸膛。在浏览南大镜像仓库的时候发现还有对应的 Arch Linux 的软件仓库，这一下子勾起了我遥远的 Arch Linux 的回忆，所以我就想这次用南大镜像配一下 Arch Linux（很莫名其妙的动机了属于是）。

再次声明，本教程为失败教程，看到这里的读者已经可以退出了==

## 流程

### 镜像下载

从[南京大学镜像仓库](https://mirror.nju.edu.cn/)中下载 Arch Linux x86-64 的镜像（~~南大人不就该用南大镜像仓库吗~~）

![](https://box.nju.edu.cn/f/1e75c8f1405a488f9760/?dl=1)

### 验证镜像签名

这一步就先跳过了，好像是可有可无的步骤

### 虚拟机的创建

在 VMWare Station 中创建一个新的虚拟机，版本就选择图中的 Ubuntu 64 位。磁盘我直接分了 100GB，内存分配了 8GB，其余配置均是默认配置

![](https://box.nju.edu.cn/f/d215d94766c8415d8672/?dl=1)
![](https://box.nju.edu.cn/f/fe09caf9799c447d8d15/?dl=1)

虚拟机配置完成，启动虚拟机，启动成功（接下来每当我以为系统安装完成重启之后还会反复看到这个画面，今晚梦里都是这个了）

![](https://box.nju.edu.cn/f/952f1e0a6cbe42e0adb1/?dl=1)

### Arch Linux 安装

#### 键盘布局和终端字体配置

键盘配置的是 US，终端字体选择 ter-132b

#### 网络连接配置

还没有配置网络连接就是正常的，能够 ping 通 archlinux.org（貌似物理机里网络这里是比较复杂的，虚拟机的好处就体现出来了）

![](https://box.nju.edu.cn/f/6f171cf3edfc4dad8d10/?dl=1)

但不知道为什么这里我的 root 变成 130 root 了 （[reddit 帖文](https://www.reddit.com/r/archlinux/comments/bl55hd/what_are_the_numbers_preceding_rootarchiso/)在这里找到了有同样的疑问，但是没有人回答）

#### 更新系统时间

![](https://box.nju.edu.cn/f/9eae645beef74bc994b8/?dl=1)

#### 进行分盘操作

最开始硬盘分布是这样的

![](https://box.nju.edu.cn/f/203862dbbb3242f88d1e/?dl=1)

创建 GPT 分区

![](https://box.nju.edu.cn/f/de9ff50810b140569f4c/?dl=1)

创建根分区（第一次只分配了 10G，然后删除分区重新分了 40G 上去）

![](https://box.nju.edu.cn/f/f57f084cb7df4e6e8419/?dl=1)

创建 home 分区

![](https://box.nju.edu.cn/f/056af3d75a2a45b49b37/?dl=1)

分区状态最终打印如下

![](https://box.nju.edu.cn/f/af38a81eb35f4ab6ab79/?dl=1)

#### 挂载分区

挂载分区时失败了

![](https://box.nju.edu.cn/f/7cd5bb78503040be911a/?dl=1)

原因是没有将分区格式化为 ext4 文件系统，之后再挂载就没有报错了

![](https://box.nju.edu.cn/f/aca7edd2d1bd45ae9977/?dl=1)

接着给仓库镜像换成南大源 `https://mirror.nju.edu.cn/archlinux/$repo/os/$arch` 然后更新软件包缓存

![](https://box.nju.edu.cn/f/ea811c9300fc49908670/?dl=1)

#### 安装三件套（姑且称呼为三件套吧）

安装 base linux linux-firmware 软件包

![](https://box.nju.edu.cn/f/61b28b60b4974cc5a935/?dl=1)

安装成功，但是中间出现了很多 WARNING，没有 ERROR 就先不管了

![](https://box.nju.edu.cn/f/34b074f398474bbb8c0b/?dl=1)

生成 fstab

![](https://box.nju.edu.cn/f/f9b925722ddd48358af1/?dl=1)

#### 进入 arch-chroot

设置时区和硬件时间

![](https://box.nju.edu.cn/f/79a6ad7223c0450ba85e/?dl=1)

在新系统中安装 vim 后，编辑/etc/locale.conf

![](https://box.nju.edu.cn/f/c027360366d14fa8a016/?dl=1)

#### 使用 pacman 安装 Networkmanager

```shell
Pacman -S networkmanager
```

将之作为网络管理工具，并配置开机自启动

#### 设置 root 密码

在此步骤中配置了 root 密码

#### 安装 Boot Loader

这里安装的是 intel-ucode

#### 退出 arch-chroot 并重启

按照官方教程，在上一步骤完成后 `exit` 退出 arch-chroot，取消挂载后，重启就可以了

然而刚刚一通操作下来，一直无法正确引导启动，重启之后界面居然还是这样的：

![](https://box.nju.edu.cn/f/e214730a07da4140afd2/?dl=1)

于是我找到了去年这个时候我看的教程，按照教程继续尝试了一下

#### 尝试挣扎 做了一些官方教程中没有的步骤

首先是配置 host

![](/images/static/A7drb7aawo5DEnxBpQacJUjNnzh.png)

安装 EFI 启动管理器

![](https://box.nju.edu.cn/f/6b79652f10b5485eb975/?dl=1)

配置/boot/loader/loader.conf 启动文件

![](https://box.nju.edu.cn/f/90452e0f01a54db3a8b5/?dl=1)

配置/boot/loader/entries/arch/conf

![](https://box.nju.edu.cn/f/eaf278fb7a344a2fbaad/?dl=1)

运行以下命令

```shell
blkid -s PARTUUID -o value /dev/sda3 >> /boot/loader/entries/arch.conf
```

然后再次尝试开机，再次失败了

## 总结

感觉如果要刷物理机的话，关于刷 linux 的很多坑都得好好填一下，关于分区操作，关于挂载的机制，关于启动引导......

但是接下来我还有另外的大坑要补，对于深度学习的很多内容我的理解并不深刻，对于一些数学方面的如概率统计、微分方程等都需要好好加强一下，不然看一些论文很难有深层次的理解，也正是因为这种不理解，让我在这个阶段对读论文并没有特别的兴趣，导致这几天一直在划水摸鱼......

对于 linux 刷机相关的内容，或许等到我有新的设备后，可以尝试将我这台 y9000p 2021 刷成纯血的 Arch Linux，这段时间就先不折腾了。