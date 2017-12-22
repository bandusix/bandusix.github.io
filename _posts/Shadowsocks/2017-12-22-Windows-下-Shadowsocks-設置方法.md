---
layout: post
title: Windows下Shadowsocks設置方法
category: Shadowsocks
keywords: Shadowsocks, ss
---

## Windows 下 Shadowsocks 設置方法

## 1、下載客戶端

我們推薦您使用最新版本的客戶端，點擊[這裏](https://github.com/shadowsocks/shadowsocks-windows/releases)下載最新的客戶端

備用链接: [https://pan.baidu.com/s/1bpbJl3x][1] 密码: 9p42

## 2、安裝 .NET Framework

一般 Windows 10 已經自帶，不需要額外安裝，如果您的系統版本略舊，請在[這裏](https://www.microsoft.com/zh-tw/download/details.aspx?id=53345)下載適用於 Windows 7 SP1、Windows 8.1、Windows Server 2008 R2 SP1、Windows Server 2012 及 Windows Server 2012 R2 的 Microsoft .NET Framework 4.6.2 (Web 安裝程式)

## 3、解壓 Shadowsocks 客戶端

閣下完成下載後，可以在熟悉的位置創建一個便於找到的文件夾，在本文中我們嘗試在桌面新建名為 `Shadowsocks` 的文件夾，之後請打開下載的 Shadowsocks 客戶端文件 請選中其中`Shadowsocks.exe`文件拖動至剛剛新建的 Shadowsocks 文件夾，並雙擊運行 `Shadowsocks.exe`

![](https://ooo.0o0.ooo/2017/05/22/5922f811318ad.png)

## 4、配置 Shadowsocks 賬號

您通過二維碼方式或者複製URL的方式增加節點，在您右下方狀態欄 Shadowsocks 圖標右鍵-服務器-掃描屏幕上的二維碼

*提示*: 此二維碼和URL同樣適應於其他客戶端

![](https://ooo.0o0.ooo/2017/05/22/5922fa22e6d8e.png)

雙擊您右下方狀態欄的 Shadowsocks 圖標，即可看到您的節點信息和賬號已經自動配置完成

## 5、配置系統代理

右擊您右下方狀態欄的 Shadowsocks 圖標，勾選 啟用系統代理 並選擇 Pac 模式

![](https://ooo.0o0.ooo/2017/05/22/5922fe379b134.png)

如果使用`PAC 模式` 無法訪問網站，請前往[這裡](https://portal.shadowsocks.la/dl.php?type=d&id=14) 下載 pac 配置文件，將 `pac.txt` 放在與shadowsocks.exe 相同的目錄文件夾下即可

注意事項:

1. 負載均衡模式高可用模式與在於分散流量和提高可用性上，對於速度的提升沒有幫助，如果對某一節點的連接質量較佳，推薦直接選中該服務器
2. 推薦使用 `PAC模式`，該模式可以實現自動代理，及沒被屏蔽的網站的流量不會經過代理。但是在 `Shadowsocks Win 2.x` 版本中因內置的 GFWList 鏈接已失效，導致 PAC 規則無法更新，您可以從選擇從本站下載 PAC 文件，或者遇到無法代理的網站時，通過編輯本地 PAC 文件，自己添加規則不包含但自己所需要代理的網站
3. `全局模式`表示基本上電腦內所有的流量都會經過代理，不推薦日常使用，因為很容易導致您的國內網站的流量以及迅雷等下載網站流量經過代理造成我們收到 ISP 投訴的嚴重后果

## 6、瀏覽器配置

如果您使用 Internet Expolor 或 Microsoft Edge 瀏覽器，您無需進行任何操作，如果您使用 Chrome 或 Firefox 瀏覽器，請查看對應教程

1. [Firefox 瀏覽器設置教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-1-firefox-settings.md)
2. [Chrome 瀏覽器設置教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-2-chrome-settings.md)


  [1]: https://pan.baidu.com/s/1bpbJl3x
