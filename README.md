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
        	create mask = 777
        	directory mask = 777

         其中设置的path目录设置成777的权限
  （3）关闭selinux，打开/etc/selinux/config文件，将SELINUX设置为disabled,（SELINUX=disabled）。
  （4）关闭防火墙,chkconfig iptables off。                      
  （5）修改完成后，重启服务器。
	
5、测试windows是否可以正常访问linux共享的文件夹，并向其中写入和读取文件。从windows系统的应用菜单中打开运行，或者使用windows+R组合见打开，输入\\linux_IP\file path后按回车，看看是否能够进入共享文件夹，然后将window上的文件拖入到该文件夹中，测试是否具有写权限。如果前面步骤操作正确，是没有任何问题的。

6、在window主机上打开我的电脑，右击左侧列表中的网络，然后选择映射网络驱动器，将linux上共享的文件夹在window系统上映射成一个网络驱动器，方便后续对共享目录的操作。到此为止，linux和window服务器实现了文件的共享，这是vs远程调试linux code 的基础保障。
