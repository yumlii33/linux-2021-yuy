# H1 无人值守Linux安装镜像制作

## 实验环境
* Virtualbox
* Ubuntu 20.04.3 Server 64bit

## 实验目的

## 实验问题
* 如何配置无人值守安装iso并在Virtualbox中完成自动化安装。
* Virtualbox安装完Ubuntu之后新添加的网卡如何实现系统开机自动启用和自动获取IP？
* 如何使用sftp在虚拟机和宿主机之间传输文件？

## 实验过程
### Part 0 配置无人值守安装iso并在Virtualbox中完成自动化安装
* 首先在有人值守的情况下安装一个ununtu20.04的虚拟机
* 下载老师给的[`user-data`](https://c4pr1c3.github.io/LinuxSysAdmin/exp/chap0x01/cd-rom/nocloud/user-data)文件到本地，并使用sftp上传到虚拟机的工作目录（自定义，本次实验中使用`~/workspace/`）里
* 修改`identity`信息：
    ```
    identity:{
        hostname: ubuntu2004,
        password: $6$V30...Ln/,
        realname: molly,
        username: molly
    }

    # 其中password为明文密码的hash值，生成命令：
    sudo apt update && sudo apt install whois
    mkpasswd -m help # 获取当前版本支持的哈希算法
    mkpasswd -m sha-512 mypassword
    ```
* 在工作目录里创建一个空文件`meta-data`
* 在工作目录下制作包含`user-data`和`meta-data`的iso文件，本次实验中命名为`init.iso`：
    ```
    sudo apt update && sudo apt install cloud-init genisoimage
    genisoimage -output init.iso -volid cidata -joliet -rock user-data meta-data
    ```
* 使用`sftp`下载到宿主机
* 也可以直接下载课程仓库里做好的镜像文件：[`focal-init.iso`](https://github.com/c4pr1c3/LinuxSysAdmin/blob/master/exp/chap0x01/cd-rom/nocloud/focal-init.iso)
* 在`Oracle VM VirtualBox`中同手工安装系统步骤，新建可以用于安装 Ubuntu 64位系统 的虚拟机配置
* 移除上述虚拟机「设置」-「存储」-「控制器：IDE」
* 在「控制器：SATA」下新建 2 个虚拟光盘，按顺序 先挂载「纯净版 Ubuntu 安装镜像文件」后挂载 `focal-init.iso`（课程仓库的iso文件）或`init.iso`（自己做的iso文件）。
* 启动虚拟机，稍等片刻会看到命令行中出现以下提示信息。此时，需要输入 yes 并按下回车键，剩下的就交给「无人值守安装」程序自动完成系统安装和重启进入系统可用状态了（本次实验尝试了四次无人值守安装，实测速度并不快，每次至少15min+）
    ```
    Continue with autoinstall? (yes|no)
    ```
### Part 1 Virtualbox安装完Ubuntu之后新添加的网卡如何实现系统开机自动启用和自动获取IP
* 修改配置文件,添加新网卡并设置为`dhcp`：
    ```
    sudo vim /etc/netplan/00-installer-config.yaml
    
    # add
    enp0s8:
        dhcp4: true
    ```

### Part 2 如何使用sftp在虚拟机和宿主机之间传输文件？
* 宿主机连接虚拟机：
    ```
    # win+R打开命令行
    sftp username@ip
    # 回车，然后输入密码，连接成功
    ```
* 上传文件：
    ```
    put filepath1(宿主机) filepath2(虚拟机)
    ```
* 下载文件：
    ```
    get filepath2(虚拟机) filepath1(宿主机)
    ```

## 参考链接
* [H1 无人值守Linux安装镜像制作（2学时）：定制用户名和默认密码、定制安装OpenSSH Server、安装过程禁止自动联网更新软件包等](https://c4pr1c3.github.io/LinuxSysAdmin/chap0x01.exp.md.html#/title-slide)
* [Github - c4pr1c3/LinuxSysAdmin](https://github.com/c4pr1c3/LinuxSysAdmin)