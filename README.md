# debug_linux_code_by_visual_Studio
本文介绍如何使用visual studio远程调试linux服务器C/C++程序，侧重点是环境搭建。
1、在windows系统的电脑上安装visual studio工具；

2、如果visual studio为vs2019之前的版本，则需要额外安装wingdb插件，安装步骤如下：
  (1)解压wingdb破解版.rar，得到crack_wingdb.bat、setdll.exe、wingdb_patch.dll、WinGDB-5.0.msi四个文件；
	(2)点击WinGDB-5.0.msi进行安装；
	(3)WinGDB安装完成后进行破解。首先进入C:\Windows\System32目录，以管理员身份打开cmd.exe; 然后通过cd命令进入到wingdb破解版.rar解压后的文件夹目录下，执行crack_wingdb.bat，然后按回车键推出，破解完成。

3、打开vs软件，此时菜单栏中会WinGDB的选项。	 

4、在linux上设置samba服务。
  （1）设置samba服务开机自启（执行chkconfig smb on）
  （2）进入/etc/samba/目录，将原来的smb.conf备份一份，然后打开smb.conf进行修改。
       * security设置为share模式, 即security = share
       * 在文件末端增加一下几行（）：
             [samba]
                comment = samba
                path = /samba
                public = yes
                writable = yes
                browseable = yes
                guest_ok= yes
         其中设置的path目录设置成777的权限
  （3）关闭selinux，打开/etc/selinux/config文件，将SELINUX设置为disabled,（SELINUX=disabled）。
  （4）关闭防火墙,chkconfig iptables off。                      
  （5）修改完成后，重启服务器。
	
	
	
	
