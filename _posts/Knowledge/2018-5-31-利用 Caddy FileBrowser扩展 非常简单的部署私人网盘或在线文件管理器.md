---
layout: post
title: 利用 Caddy FileBrowser扩展 非常简单的部署 私人网盘/在线文件管理器
category: Knowledge
keywords: Caddy,FileBrowser,简单部署,私人网盘,私人云盘
---


[利用 Caddy FileBrowser扩展 非常简单的部署 私人网盘/在线文件管理器](https://doub.io/jzzy-3/)
======================================================================

来源： [逗比根据地](https://doub.io/jzzy-3/) 


![](https://img.doub.pw/thumbs/FileBrowser-03.png)

* * *

Caddy FileBrowser扩展介绍
---------------------

FileBrowser 是基于Caddy 的扩展。它提供文件管理界面，可用于 上传/下载/删除/预览和重命名 等该目录中的文件。

1.  **支持** 上传文件
2.  **支持** 按类型 搜索文件
3.  **支持** 批量压缩 文件下载
4.  **支持** 多用户管理(权限可控)
5.  **支持** 在网页执行 **Linux命令**
6.  **支持** 创建 **共享链接(限时/永久)**
7.  **支持** 在线编辑 各类文本文件
8.  **支持** 在线浏览 图片/文本/视频等
9.  **支持** 新建/重命名/移动/删除 文件和文件夹等
10.  **部署简单，几步完成，无需任何依赖环境**
11.  **等等 ...**

> 目前这个扩展新版本已经支持中文， **[简体中文语言文件](https://github.com/hacdias/filemanager/issues/168)** 由本人制作！

**Caddy 文档：**[https://caddyserver.com/docs/http.filemanager](https://caddyserver.com/docs/http.filemanager)

**Github 项目：**[https://github.com/filebrowser/filebrowser](https://github.com/filebrowser/filebrowser)

前面的几篇教程，我都用到了Caddy，大家应该都能看出来Caddy的易用性，所以本篇教程也很简单，我会提供一些示例，不懂的也可以留言。

**其他私人网盘教程：[https://doub.io/all-one/#私有网盘 相关教程](https://doub.io/all-one/#私有网盘 相关教程)**

> _注意：_因为自从该扩展 **v1.5.0** 开始，就从 **FileManager 改名为 FileBrowser** 了，但是其作为 Caddy 扩展的使用代码没区别，所以我只修改了本文章里的部分名称，代码什么的都不变。

安装 Caddy
--------

    wget -N --no-check-certificate https://softs.loan/Bash/caddy\_install.sh && chmod +x caddy\_install.sh && bash caddy_install.sh install http.filemanager

\# 如果上面这个脚本无法下载，尝试使用备用下载：

    wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy\_install.sh && chmod +x caddy\_install.sh && bash caddy_install.sh install http.filemanager

安装Caddy成功后，继续新建一个用于使用的虚拟主机文件夹，例如 **file**（可以自己改）：

    mkdir /usr/local/caddy/www && mkdir /usr/local/caddy/www/file

配置 Caddy
--------

首先，我们先讲一下，FileBrowser扩展各个参数。

    filemanager \[url\] \[scope\] {
     database path
    }

1.  **url** 是要设置的网站URL。默认是 `/` (比如 `/doubi` 那么访问入口就是 `http://ip/doubi` )。
2.  **scope** 是要浏览的服务器文件目录路径，可以使相对或绝对路径。默认是 `./` (服务器上面文件的绝对或相对路径)。
3.  **database path** 是 filemanager 的数据库路径（如果不写这个参数，则默认就是 **/usr/local/caddy/filemanager.db**）。

配置示例
----

以下示例中，虚拟主机文件夹皆为 `/usr/local/caddy/www/file`

示例域名皆为 `toyoo.pw`

### IP HTTP

本示例是，绑定虚拟主机为IP（即通过IP访问），HTTP协议（80端口）。

[点击展开 查看内容](#)

**\# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行！**

    echo ":80 {
     root /usr/local/caddy/www/file
     timeouts none
     gzip
     filemanager / /usr/local/caddy/www/file {
      database /usr/local/caddy/filemanager.db
     }
    }" \> /usr/local/caddy/Caddyfile

### 域名 HTTP

本示例是，绑定虚拟主机为域名（即通过域名访问），HTTP协议（80端口）。

[点击展开 查看内容](#)

**\# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行（注意替换示例域名）！**

    echo "http://toyoo.pw {
     root /usr/local/caddy/www/file
     timeouts none
     gzip
     filemanager / /usr/local/caddy/www/file {
      database /usr/local/caddy/filemanager.db
     }
    }" \> /usr/local/caddy/Caddyfile

### 域名 HTTPS

本示例是，绑定虚拟主机为域名（即通过域名访问），HTTPS协议（443端口）。

[点击展开 查看内容](#)

如果你有 SSL证书和密匙的话，把 SSL证书(xxx.crt)和密匙(xxx.key)文件放到 `/root` 文件夹下（也可以是其他文件夹，自己改下面代码），然后这样做：

**\# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行（注意替换示例域名）！**

    echo "toyoo.pw {
     root /usr/local/caddy/www/file
     timeouts none
     tls /root/xxx.crt /root/xxx.key
     gzip
     filemanager / /usr/local/caddy/www/file {
      database /usr/local/caddy/filemanager.db
     }
    }" \> /usr/local/caddy/Caddyfile

如果你没有 SSL证书和密匙，那么你可以这样做：

下面的 `[email protected]` 改成你的邮箱，同时需要注意的是，申请 SSL证书前，**请务必提前解析好域名记录(解析后最好等一会，以全球生效)，否则 Caddy会申请并配置失败！**

**\# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行（注意替换示例域名）！**

    echo "toyoo.pw {
     root /usr/local/caddy/www/file
     timeouts none
     tls \[email protected\]
     gzip
     filemanager / /usr/local/caddy/www/file {
      database /usr/local/caddy/filemanager.db
     }
    }" \> /usr/local/caddy/Caddyfile

### 域名 HTTP重定向 HTTPS(仅手动指定SSL证书和密匙)

本示例是，域名HTTP重定向为HTTPS。

当你是手动指定 SSL证书和密匙 来配置的话，Caddy只会监听 443端口(https)，并不会自动设置 80端口(http)的重定向，如果要做重定向的话，可以这样做：

[点击展开 查看内容](#)

下面的示例代码中，是把 http://toyoo.pw 重定向到了 https://toyoo.pw 。

**\# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行（注意替换示例域名）！**

    echo "http://toyoo.pw {
     timeouts none
     redir https://toyoo.pw{url}
    }
    toyoo.pw {
     root /usr/local/caddy/www/file
     timeouts none
     tls /root/xxx.crt /root/xxx.key
     gzip
     filemanager / /usr/local/caddy/www/file {
      database /usr/local/caddy/filemanager.db
     }
    }" \> /usr/local/caddy/Caddyfile

当你已经配置完上面步骤后，那就需要启动Caddy了。

    /etc/init.d/caddy start
    \# 如果启动失败可以看Caddy日志： tail -f /tmp/caddy.log

FileBrowser 使用说明
----------------

> 配置并打开网站后，默认账号和密码都是 **admin**，可以登陆后修改。**\[Settings\]**

### 切换中文

进入后可以点击左边侧栏 **\[Settings\]** 进入设置页面，然后选择 **\[language - Chinese (Simplified)\]** ，并点击右下角第一个 **\[Update\]** 按钮更新。

### 使用技巧

一些按键有对应的作用：

1.  **F1** \- 查看帮助
2.  **F2** \- 重命名 文件/文件夹
3.  **DEL** \- 删除所选 文件/文件夹
4.  **ESC** \- 清除当前选择 或 关闭提示
5.  **CTRL + S** \- 保存下载 文件/文件夹（zip压缩）
6.  **CTRL + 鼠标左键 单击** \- 选择多个文件/文件夹
7.  **鼠标左键 双击** \- 打开文件/文件夹
8.  **鼠标左键 单击** \- 选择文件/文件夹

Caddy 使用说明
----------

**启动：**/etc/init.d/caddy start

**停止：**/etc/init.d/caddy stop

**重启：**/etc/init.d/caddy restart

**查看状态：**/etc/init.d/caddy status

**查看Caddy启动日志：** tail -f /tmp/caddy.log

**Caddy配置文件位置：**/usr/local/caddy/Caddyfile

**FileBrowser数据库位置：**/usr/local/caddy/filemanager.db

**Caddy自动申请SSL证书位置：**/.caddy/acme/acme-v01.api.letsencrypt.org/sites/xxx.xxx(域名)/

升级FileBrowser
-------------

因为FileBrowser是Caddy的扩展，是融合成一个文件的，升级FileBrowser=升级Caddy（加扩展），所以只需要重新执行下面的命令覆盖安装Caddy即可**（只会覆盖 Caddy自身，不影响配置文件）**，覆盖安装后启动Caddy即可（ `/etc/init.d/caddy start` ）。

    wget -N --no-check-certificate https://softs.loan/Bash/caddy\_install.sh && chmod +x caddy\_install.sh && bash caddy_install.sh install http.filemanager

\# 如果上面这个脚本无法下载，尝试使用备用下载：

    wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy\_install.sh && chmod +x caddy\_install.sh && bash caddy_install.sh install http.filemanager

卸载
--

只需要把安装命令 **install** 改成 **uninstall** 就是卸载了，因为扩展是集成于Caddy中的，所以无法单独卸载某个扩展。

    wget -N --no-check-certificate https://softs.loan/Bash/caddy\_install.sh && chmod +x caddy\_install.sh && bash caddy_install.sh uninstall

\# 如果上面这个脚本无法下载，尝试使用备用下载：

    wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy\_install.sh && chmod +x caddy\_install.sh && bash caddy_install.sh uninstall

其他说明
----

### 启动显示成功，但是实际未运行

因为 服务脚本判断的问题，只判断了nohub是否运行 Caddy成功，但没有判断 Caddy 是否保持正常运行。

你可以理解为，nohub成功启动了 Caddy，但是 Caddy因为配置文件错误等原因，启动后又退出了。

所以这种情况下，你应该去查看启动日志：

    tail -f /tmp/caddy.log

### 单网站/多网站

当然，上面的几个示例，实际上都算是单网站。  

[点击展开 查看更多](#)

  
最后一句代码都是 `}" > /usr/local/caddy/Caddyfile` ，也就是清空了 Caddy配置文件，然后再写入了配置信息。

如果你要设置多个网站，那么把最后一句代码改成 `}" >> /usr/local/caddy/Caddyfile` 即可，注意是把 `> 改成 >>` ，这样就不会清空原来的配置信息了，而是会把要添加的配置信息加到配置文件最后！  

### Caddy下载文件频繁中断

可能是因为 Caddy的超时时间机制导致的，可以在配置文件中加入这句代码 `timeouts none` ，例如这样：

[点击展开 查看更多](#)

    http://toyoo.pw (
     timeouts none
     root /home/www
     ...(省略号代表 这下面的内容是重复的，请不要直接写省略号到配置文件中)
    )

### Caddy启动失败，打开 http://ip 显示的是 It works !

一些系统会自带 apache2 ，而 apache2 会占用80端口，导致Caddy无法绑定端口，所以只要关掉就好了。

[点击展开 查看更多](#)

netstat -lntp
\# 我们可以通过这个命令查看是不是被其他软件占用了 80 端口。

不过 apache2 会默认开机自启动，如果不需要可以关闭自启动或者卸载 apache2 。

**停止 Apache2**

/etc/init.d/apache2 stop
\# 尝试使用上面这个关闭，如果没效果或者提示什么错误无法关闭，那就用下面这个强行关闭进程。

    kill -9 $(ps -ef|grep "apache2"|grep -v "grep"|awk '{print $2}')

**取消开机自启动**

\# 以下代码仅限 Debian/Ubuntu 系统 #
update-rc.d -f apache2 remove

**卸载 Apache2**

\# 以下代码仅限 Debian/Ubuntu 系统 #
apt-get remove --purge apache2

关闭 Apache2后，就可以尝试启动 Caddy ，并试试能不能打开网页。

/etc/init.d/caddy start

### 如果你是 Aria2 教程里过来的，那么请看这个示例和说明

使用这个扩展的时候，请先确定你的caddy安装了这个扩展(2017/03/23 17:50 以前通过我网站其他教程安装的皆没有)，否则请卸载重装！  

[点击展开 查看更多](#)

**卸载 Caddy：**

bash caddy_install.sh uninstall

使用这个扩展，那么就不需要 caddy 自带的列表功能了，所以可以删除参数 `browse` ，然后如下设置即可。

因为只有一个用户，所以不需要设置全局配置，你访问下载的BT文件就可以通过 `http://ip或域名/Download/ [](http://toyoo.pw/Download/usr/local/caddy/www/aria2/Download/)` 来访问和操作了，默认用户名和密码都是 admin。

更多的示例，请[查看这里](https://doub.io/jzzy-3/#Caddy FileManager扩展介绍)。

**\# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行（注意替换示例域名）！**

    echo -e "http://toyoo.pw {
     root /usr/local/caddy/www/aria2
     timeouts none
     gzip
     filemanager /Download /usr/local/caddy/www/aria2/Download {
      database /usr/local/caddy/filemanager.db
     }
    }" \> /usr/local/caddy/Caddyfile

### 启动 Caddy后，无法访问

[点击展开 查看更多](#)

这个可能是防火墙的问题，开放防火墙端口即可。

    iptables -I INPUT -m state --state NEW -m tcp -p tcp --dport 端口 -j ACCEPT
    iptables -I INPUT -m state --state NEW -m udp -p udp --dport 端口 -j ACCEPT
    
    \# 删除防火墙规则，内容一样把 -I 换成 -D 就行了：
    iptables -D INPUT -m state --state NEW -m tcp -p tcp --dport 端口 -j ACCEPT
    iptables -D INPUT -m state --state NEW -m udp -p udp --dport 端口 -j ACCEPT

### FileBrowser账号密码忘了或想要重置账号信息

FileBrowser没有找回密码功能，所以一旦你忘记了密码，那么GG，不过没事 有办法重置。

[点击展开 查看更多](#)

当然我们可以重置FileBrowser的数据库文件来清除所有账号信息，这样我们就变成初始账号和密码了(admin/admin)。

> 注意：删除数据库文件只会影响数据库内储存的各账号信息，并不会影响服务器本地的文件夹/文件。

很简单，关闭Caddy，然后删除FileBrowser数据库文件，启动Caddy，使用初始账号密码登陆。

    /etc/init.d/caddy stop
    rm -rf /usr/local/caddy/filemanager.db
    /etc/init.d/caddy start

* * *






