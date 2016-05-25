*****************************************************************
***                  PXE Network boot Server                  ***
***                         rhel 6.5                          ***
*****************************************************************


[root@abhiteckshack Red-Hat-Tech]# cat /etc/redhat-release 
Red Hat Enterprise Linux Server release 6.5 (Santiago)
[root@abhiteckshack Red-Hat-Tech]# 

*********************************************

Step 1 : First we Need to set Desabled Selinux and Flush all Firewall(Iptables) and make it permanent?


[root@abhiteckshack Red-Hat-Tech]# setenforce 0
[root@abhiteckshack Red-Hat-Tech]# cat /etc/selinux/config 
	
	# This file controls the state of SELinux on the system.
	# SELINUX= can take one of these three values:
	#     enforcing - SELinux security policy is enforced.
	#     permissive - SELinux prints warnings instead of enforcing.
	#     disabled - No SELinux policy is loaded.
	SELINUX=disabled							<<<<<<<<<<<<<<< (Make it disabled)
	# SELINUXTYPE= can take one of these two values:
	#     targeted - Targeted processes are protected,
	#     mls - Multi Level Security protection.
	SELINUXTYPE=targeted 


[root@abhiteckshack Red-Hat-Tech]# iptables -F
[root@abhiteckshack Red-Hat-Tech]# service iptables save
iptables: Saving firewall rules to /etc/sysconfig/iptables:[  OK  ]
[root@abhiteckshack Red-Hat-Tech]# 


*****************************

Step 2 : Now We need to install following Software ?

=====>> dhcp tftp-server syslinux  vsftpd ftp system-config-kickstart



[root@abhiteckshack Red-Hat-Tech]# yum install dhcp tftp-server syslinux vsftpd ftp system-config-kickstart -y
Loaded plugins: product-id, refresh-packagekit, security, subscription-manager
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
Repository 'os' is missing name in configuration, using id
Setting up Install Process
Resolving Dependencies
--> Running transaction check
---> Package dhcp.x86_64 12:4.1.1-38.P1.el6 will be installed
---> Package ftp.x86_64 0:0.17-54.el6 will be installed
---> Package syslinux.x86_64 0:4.02-8.el6 will be installed
---> Package system-config-kickstart.noarch 0:2.8.6.5-1.el6 will be installed
--> Processing Dependency: pykickstart >= 0.96 for package: system-config-kickstart-2.8.6.5-1.el6.noarch
--> Processing Dependency: anaconda >= 11.4.0.42-1 for package: system-config-kickstart-2.8.6.5-1.el6.noarch
--> Processing Dependency: system-config-language for package: system-config-kickstart-2.8.6.5-1.el6.noarch
---> Package tftp-server.x86_64 0:0.49-7.el6 will be installed
--> Processing Dependency: xinetd for package: tftp-server-0.49-7.el6.x86_64
---> Package vsftpd.x86_64 0:2.2.2-11.el6_4.1 will be installed
--> Running transaction check
---> Package anaconda.x86_64 0:13.21.215-1.el6 will be installed
--> Processing Dependency: python-pyblock >= 0.45-2 for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: python-cryptsetup >= 0.0.6 for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: pyparted >= 3.0 for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: fcoe-utils >= 1.0.12-3.20100323git for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: createrepo >= 0.4.7 for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: tigervnc-server for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: squashfs-tools for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: makebootfat for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: isomd5sum for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: anaconda-yum-plugins for package: anaconda-13.21.215-1.el6.x86_64
--> Processing Dependency: libiscsi.so.0()(64bit) for package: anaconda-13.21.215-1.el6.x86_64
---> Package pykickstart.noarch 0:1.74.14-1.el6 will be installed
---> Package system-config-language.noarch 0:1.3.4-6.el6 will be installed
---> Package xinetd.x86_64 2:2.3.14-39.el6_4 will be installed
--> Running transaction check
---> Package anaconda-yum-plugins.noarch 1:1.0-5.1.el6 will be installed
---> Package createrepo.noarch 0:0.9.9-18.el6 will be installed
--> Processing Dependency: python-deltarpm for package: createrepo-0.9.9-18.el6.noarch
---> Package fcoe-utils.x86_64 0:1.0.28-3.el6 will be installed
--> Processing Dependency: lldpad >= 0.9.43 for package: fcoe-utils-1.0.28-3.el6.x86_64
--> Processing Dependency: libhbalinux >= 1.0.13 for package: fcoe-utils-1.0.28-3.el6.x86_64
--> Processing Dependency: device-mapper-multipath for package: fcoe-utils-1.0.28-3.el6.x86_64
--> Processing Dependency: libHBAAPI.so.2()(64bit) for package: fcoe-utils-1.0.28-3.el6.x86_64
---> Package iscsi-initiator-utils.x86_64 0:6.2.0.873-10.el6 will be installed
---> Package isomd5sum.x86_64 1:1.0.6-1.el6 will be installed
---> Package makebootfat.x86_64 0:1.4-10.el6 will be installed
---> Package pyparted.x86_64 0:3.4-4.el6 will be installed
---> Package python-cryptsetup.x86_64 0:0.0.11-1.el6 will be installed
---> Package python-pyblock.x86_64 0:0.48-1.el6 will be installed
---> Package squashfs-tools.x86_64 0:4.0-5.el6 will be installed
---> Package tigervnc-server.x86_64 0:1.1.0-5.el6_4.1 will be installed
--> Running transaction check
---> Package device-mapper-multipath.x86_64 0:0.4.9-72.el6 will be installed
--> Processing Dependency: device-mapper-multipath-libs = 0.4.9-72.el6 for package: device-mapper-multipath-0.4.9-72.el6.x86_64
--> Processing Dependency: libmultipath.so()(64bit) for package: device-mapper-multipath-0.4.9-72.el6.x86_64
--> Processing Dependency: libmpathpersist.so.0()(64bit) for package: device-mapper-multipath-0.4.9-72.el6.x86_64
---> Package libhbaapi.x86_64 0:2.2.9-1.el6 will be installed
---> Package libhbalinux.x86_64 0:1.0.16-1.el6 will be installed
---> Package lldpad.x86_64 0:0.9.46-2.el6 will be installed
--> Processing Dependency: lldpad-libs(x86-64) = 0.9.46-2.el6 for package: lldpad-0.9.46-2.el6.x86_64
--> Processing Dependency: liblldp_clif.so.1()(64bit) for package: lldpad-0.9.46-2.el6.x86_64
--> Processing Dependency: libconfig.so.8()(64bit) for package: lldpad-0.9.46-2.el6.x86_64
---> Package python-deltarpm.x86_64 0:3.5-0.5.20090913git.el6 will be installed
--> Processing Dependency: deltarpm = 3.5-0.5.20090913git.el6 for package: python-deltarpm-3.5-0.5.20090913git.el6.x86_64
--> Running transaction check
---> Package deltarpm.x86_64 0:3.5-0.5.20090913git.el6 will be installed
---> Package device-mapper-multipath-libs.x86_64 0:0.4.9-72.el6 will be installed
---> Package libconfig.x86_64 0:1.3.2-1.1.el6 will be installed
---> Package lldpad-libs.x86_64 0:0.9.46-2.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                        Arch     Version                     Repository
                                                                           Size
================================================================================
Installing:
 dhcp                           x86_64   12:4.1.1-38.P1.el6          os   817 k
 ftp                            x86_64   0.17-54.el6                 os    58 k
 syslinux                       x86_64   4.02-8.el6                  os   859 k
 system-config-kickstart        noarch   2.8.6.5-1.el6               os   924 k
 tftp-server                    x86_64   0.49-7.el6                  os    39 k
 vsftpd                         x86_64   2.2.2-11.el6_4.1            os   151 k
Installing for dependencies:
 anaconda                       x86_64   13.21.215-1.el6             os   3.2 M
 anaconda-yum-plugins           noarch   1:1.0-5.1.el6               os    12 k
 createrepo                     noarch   0.9.9-18.el6                os    94 k
 deltarpm                       x86_64   3.5-0.5.20090913git.el6     os    71 k
 device-mapper-multipath        x86_64   0.4.9-72.el6                os   116 k
 device-mapper-multipath-libs   x86_64   0.4.9-72.el6                os   180 k
 fcoe-utils                     x86_64   1.0.28-3.el6                os   103 k
 iscsi-initiator-utils          x86_64   6.2.0.873-10.el6            os   686 k
 isomd5sum                      x86_64   1:1.0.6-1.el6               os    24 k
 libconfig                      x86_64   1.3.2-1.1.el6               os    50 k
 libhbaapi                      x86_64   2.2.9-1.el6                 os    21 k
 libhbalinux                    x86_64   1.0.16-1.el6                os    32 k
 lldpad                         x86_64   0.9.46-2.el6                os   216 k
 lldpad-libs                    x86_64   0.9.46-2.el6                os    28 k
 makebootfat                    x86_64   1.4-10.el6                  os    42 k
 pykickstart                    noarch   1.74.14-1.el6               os   309 k
 pyparted                       x86_64   3.4-4.el6                   os   184 k
 python-cryptsetup              x86_64   0.0.11-1.el6                os    22 k
 python-deltarpm                x86_64   3.5-0.5.20090913git.el6     os    27 k
 python-pyblock                 x86_64   0.48-1.el6                  os    67 k
 squashfs-tools                 x86_64   4.0-5.el6                   os    80 k
 system-config-language         noarch   1.3.4-6.el6                 os   143 k
 tigervnc-server                x86_64   1.1.0-5.el6_4.1             os   1.1 M
 xinetd                         x86_64   2:2.3.14-39.el6_4           os   122 k

Transaction Summary
================================================================================
Install      30 Package(s)

Total download size: 9.7 M
Installed size: 31 M
Downloading Packages:
--------------------------------------------------------------------------------
Total                                            14 MB/s | 9.7 MB     00:00     
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : pykickstart-1.74.14-1.el6.noarch                            1/30 
  Installing : pyparted-3.4-4.el6.x86_64                                   2/30 
  Installing : libhbaapi-2.2.9-1.el6.x86_64                                3/30 
  Installing : libhbalinux-1.0.16-1.el6.x86_64                             4/30 
  Installing : python-pyblock-0.48-1.el6.x86_64                            5/30 
  Installing : syslinux-4.02-8.el6.x86_64                                  6/30 
  Installing : makebootfat-1.4-10.el6.x86_64                               7/30 
  Installing : system-config-language-1.3.4-6.el6.noarch                   8/30 
  Installing : device-mapper-multipath-libs-0.4.9-72.el6.x86_64            9/30 
  Installing : device-mapper-multipath-0.4.9-72.el6.x86_64                 10/30 
  Installing : python-cryptsetup-0.0.11-1.el6.x86_64                       11/30 
  Installing : lldpad-libs-0.9.46-2.el6.x86_64                             12/30 
  Installing : deltarpm-3.5-0.5.20090913git.el6.x86_64                     13/30 
  Installing : python-deltarpm-3.5-0.5.20090913git.el6.x86_64              14/30 
  Installing : createrepo-0.9.9-18.el6.noarch                              15/30 
  Installing : squashfs-tools-4.0-5.el6.x86_64                             16/30 
  Installing : 2:xinetd-2.3.14-39.el6_4.x86_64                             17/30 
  Installing : iscsi-initiator-utils-6.2.0.873-10.el6.x86_64               18/30 
  Installing : 1:isomd5sum-1.0.6-1.el6.x86_64                              19/30 
  Installing : 1:anaconda-yum-plugins-1.0-5.1.el6.noarch                   20/30 
  Installing : tigervnc-server-1.1.0-5.el6_4.1.x86_64                      21/30 
  Installing : libconfig-1.3.2-1.1.el6.x86_64                              22/30 
  Installing : lldpad-0.9.46-2.el6.x86_64                                  23/30 
  Installing : fcoe-utils-1.0.28-3.el6.x86_64                              24/30 
  Installing : anaconda-13.21.215-1.el6.x86_64                             25/30 
  Installing : system-config-kickstart-2.8.6.5-1.el6.noarch                26/30 
  Installing : tftp-server-0.49-7.el6.x86_64                               27/30 
  Installing : 12:dhcp-4.1.1-38.P1.el6.x86_64                              28/30 
  Installing : ftp-0.17-54.el6.x86_64                                      29/30 
  Installing : vsftpd-2.2.2-11.el6_4.1.x86_64                              30/30 
  Verifying  : libconfig-1.3.2-1.1.el6.x86_64                              1/30 
  Verifying  : tigervnc-server-1.1.0-5.el6_4.1.x86_64                      2/30 
  Verifying  : 1:anaconda-yum-plugins-1.0-5.1.el6.noarch                   3/30 
  Verifying  : 1:isomd5sum-1.0.6-1.el6.x86_64                              4/30 
  Verifying  : iscsi-initiator-utils-6.2.0.873-10.el6.x86_64               5/30 
  Verifying  : fcoe-utils-1.0.28-3.el6.x86_64                              6/30 
  Verifying  : vsftpd-2.2.2-11.el6_4.1.x86_64                              7/30 
  Verifying  : device-mapper-multipath-0.4.9-72.el6.x86_64                 8/30 
  Verifying  : 2:xinetd-2.3.14-39.el6_4.x86_64                             9/30 
  Verifying  : ftp-0.17-54.el6.x86_64                                      10/30 
  Verifying  : squashfs-tools-4.0-5.el6.x86_64                             11/30 
  Verifying  : deltarpm-3.5-0.5.20090913git.el6.x86_64                     12/30 
  Verifying  : lldpad-libs-0.9.46-2.el6.x86_64                             13/30 
  Verifying  : tftp-server-0.49-7.el6.x86_64                               14/30 
  Verifying  : libhbalinux-1.0.16-1.el6.x86_64                             15/30 
  Verifying  : libhbaapi-2.2.9-1.el6.x86_64                                16/30 
  Verifying  : system-config-kickstart-2.8.6.5-1.el6.noarch                17/30 
  Verifying  : python-cryptsetup-0.0.11-1.el6.x86_64                       18/30 
  Verifying  : lldpad-0.9.46-2.el6.x86_64                                  19/30 
  Verifying  : createrepo-0.9.9-18.el6.noarch                              20/30 
  Verifying  : anaconda-13.21.215-1.el6.x86_64                             21/30 
  Verifying  : python-deltarpm-3.5-0.5.20090913git.el6.x86_64              22/30 
  Verifying  : device-mapper-multipath-libs-0.4.9-72.el6.x86_64            23/30 
  Verifying  : pyparted-3.4-4.el6.x86_64                                   24/30 
  Verifying  : python-pyblock-0.48-1.el6.x86_64                            25/30 
  Verifying  : pykickstart-1.74.14-1.el6.noarch                            26/30 
  Verifying  : system-config-language-1.3.4-6.el6.noarch                   27/30 
  Verifying  : makebootfat-1.4-10.el6.x86_64                               28/30 
  Verifying  : syslinux-4.02-8.el6.x86_64                                  29/30 
  Verifying  : 12:dhcp-4.1.1-38.P1.el6.x86_64                              30/30 

Installed:
  dhcp.x86_64 12:4.1.1-38.P1.el6     ftp.x86_64 0:0.17-54.el6            syslinux.x86_64 0:4.02-8.el6    system-config-kickstart.noarch 0:2.8.6.5-1.el6   
  tftp-server.x86_64 0:0.49-7.el6    vsftpd.x86_64 0:2.2.2-11.el6_4.1   

Dependency Installed:
  anaconda.x86_64 0:13.21.215-1.el6                  anaconda-yum-plugins.noarch 1:1.0-5.1.el6         createrepo.noarch 0:0.9.9-18.el6                    
  deltarpm.x86_64 0:3.5-0.5.20090913git.el6          device-mapper-multipath.x86_64 0:0.4.9-72.el6     device-mapper-multipath-libs.x86_64 0:0.4.9-72.el6  
  fcoe-utils.x86_64 0:1.0.28-3.el6                   iscsi-initiator-utils.x86_64 0:6.2.0.873-10.el6   isomd5sum.x86_64 1:1.0.6-1.el6                      
  libconfig.x86_64 0:1.3.2-1.1.el6                   libhbaapi.x86_64 0:2.2.9-1.el6                    libhbalinux.x86_64 0:1.0.16-1.el6                   
  lldpad.x86_64 0:0.9.46-2.el6                       lldpad-libs.x86_64 0:0.9.46-2.el6                 makebootfat.x86_64 0:1.4-10.el6                     
  pykickstart.noarch 0:1.74.14-1.el6                 pyparted.x86_64 0:3.4-4.el6                       python-cryptsetup.x86_64 0:0.0.11-1.el6             
  python-deltarpm.x86_64 0:3.5-0.5.20090913git.el6   python-pyblock.x86_64 0:0.48-1.el6                squashfs-tools.x86_64 0:4.0-5.el6                   
  system-config-language.noarch 0:1.3.4-6.el6        tigervnc-server.x86_64 0:1.1.0-5.el6_4.1          xinetd.x86_64 2:2.3.14-39.el6_4                     

Complete!
[root@abhiteckshack Red-Hat-Tech]# 


*****************************

Step 2 : Now we are ceate our DHCP Server and make it permanent ON ?

[root@abhiteckshack Red-Hat-Tech]# cat /etc/dhcp/dhcpd.conf
	#
	# DHCP Server Configuration file.
	#   see /usr/share/doc/dhcp*/dhcpd.conf.sample
	#   see 'man 5 dhcpd.conf'
	#
	
	allow booting;
	allow bootp;
	authoritative;
	
		subnet 192.168.221.0 netmask 255.255.255.0
		{
			range 192.168.221.50 192.168.221.100;
	
			next-server 192.168.221.155;
			filename "pxelinux.0";	
	
		}
[root@abhiteckshack Red-Hat-Tech]# 
[root@abhiteckshack Red-Hat-Tech]# service dhcpd restart
Shutting down dhcpd:                                       [  OK  ]
Starting dhcpd:                                            [  OK  ]
[root@abhiteckshack Red-Hat-Tech]# chkconfig dhcpd on
[root@abhiteckshack Red-Hat-Tech]# 


*****************************

Step 3 : Now we are create our TFTP Server and make it permanent ON ?

[root@abhiteckshack Red-Hat-Tech]# vim /etc/xinetd.d/tftp 
[root@abhiteckshack Red-Hat-Tech]# cat /etc/xinetd.d/tftp
	# default: off
	# description: The tftp server serves files using the trivial file transfer \
	#	protocol.  The tftp protocol is often used to boot diskless \
	#	workstations, download configuration files to network-aware printers, \
	#	and to start the installation process for some operating systems.
	service tftp
	{
		socket_type		= dgram
		protocol		= udp
		wait			= yes
		user			= root
		server			= /usr/sbin/in.tftpd
		server_args		= -s /var/lib/tftpboot
		disable			= no  <++++++++++++++++++++++++======================= (change it from YES to NO)
		per_source		= 11
		cps			= 100 2
		flags			= IPv4
	}
[root@abhiteckshack Red-Hat-Tech]# 
[root@abhiteckshack Red-Hat-Tech]# cd /var/lib/tftpboot/                <<<<<<<<<<<<<<<<(go to this path and cp all file as below)
[root@abhiteckshack tftpboot]# cp /usr/share/syslinux/pxelinux.0  .
[root@abhiteckshack tftpboot]# cp /usr/share/syslinux/chain.c32  .
[root@abhiteckshack tftpboot]# cp /usr/share/syslinux/menu.c32  .
[root@abhiteckshack tftpboot]# cp /usr/share/syslinux/memdisk  .
[root@abhiteckshack tftpboot]# cp /usr/share/syslinux/mboot.c32  .
[root@abhiteckshack tftpboot]# cp /usr/share/syslinux/vesamenu.c32  .
[root@abhiteckshack tftpboot]# ls
chain.c32  mboot.c32  memdisk  menu.c32  pxelinux.0  vesamenu.c32
[root@abhiteckshack tftpboot]# 
[root@abhiteckshack tftpboot]# mkdir pxelinux.cfg                 <<<<<<<<<<<<<<<<<<<< (make new folder with same name)
[root@abhiteckshack tftpboot]# ls
chain.c32  mboot.c32  memdisk  menu.c32  pxelinux.0  pxelinux.cfg
[root@abhiteckshack tftpboot]# 
[root@abhiteckshack tftpboot]# mkdir redhat6.5			<<<<<<<<<<<<<<<<<<<<<< (make folder with same name that contain all related files)
[root@abhiteckshack tftpboot]# 
[root@abhiteckshack redhat6.5]# cp /media/RHEL_6.5\ x86_64\ Disc\ 1/isolinux/*  .    <<<<<<<<<<<<<<< (Copy all files from isolinux folder to redhat6.5)
[root@abhiteckshack redhat6.5]# ls
boot.cat  grub.conf   isolinux.bin  memtest     TRANS.TBL     vmlinuz
boot.msg  initrd.img  isolinux.cfg  splash.jpg  vesamenu.c32
[root@abhiteckshack redhat6.5]#
[root@abhiteckshack tftpboot]# cp /media/RHEL_6.5\ x86_64\ Disc\ 1/isolinux/isolinux.cfg   pxelinux.cfg/default  <<<< (Copy isolinux.cfg to pxelinux.cfg)
[root@abhiteckshack tftpboot]# 
[root@abhiteckshack redhat6.5]# cat  /var/lib/tftpboot/pxelinux.cfg/default
	default vesamenu.c32
	#prompt 1
	timeout 100
	
	display boot.msg
	
	menu background splash.jpg
	menu title Welcome to Red Hat Enterprise Linux 6.5!
	menu color border 0 #ffffffff #00000000
	menu color sel 7 #ffffffff #ff000000
	menu color title 0 #ffffffff #00000000
	menu color tabmsg 0 #ffffffff #00000000
	menu color unsel 0 #ffffffff #00000000
	menu color hotsel 0 #ff000000 #ffffffff
	menu color hotkey 7 #ffffffff #ff000000
	menu color scrollbar 0 #ffffffff #00000000
	
	label linux
	  menu label ^Install or upgrade an existing system
	  menu default
	  kernel redhat6.5/vmlinuz							     <<<<<<<<(Change this line)					
	  append initrd=redhat6.5/initrd.img ks=ftp://192.168.221.155/pub/redhat6.5/ks.cfg    <<<<<<<<< (Change this line also)
	label vesa
	  menu label Install system with ^basic video driver
	  kernel vmlinuz
	  append initrd=initrd.img xdriver=vesa nomodeset
	label rescue
	  menu label ^Rescue installed system
	  kernel vmlinuz
	  append initrd=initrd.img rescue
	label local
	  menu label Boot from ^local drive
	  localboot 0xffff
	label memtest86
	  menu label ^Memory test
	  kernel memtest
	  append -

[root@abhiteckshack redhat6.5]# 
[root@abhiteckshack tftpboot]# service xinetd restart
Stopping xinetd:                                           [FAILED]
Starting xinetd:                                           [  OK  ]
[root@abhiteckshack tftpboot]# service xinetd restart
Stopping xinetd:                                           [  OK  ]
Starting xinetd:                                           [  OK  ]
[root@abhiteckshack tftpboot]#
[root@abhiteckshack redhat6.5]# chkconfig xinetd on
[root@abhiteckshack redhat6.5]# 


*****************************

Step 3 : Make ftp server for our iso image ?

[root@abhiteckshack pub]# pwd
/var/ftp/pub
[root@abhiteckshack pub]# mkdir redhat6.5
[root@abhiteckshack pub]# cd redhat6.5/
[root@abhiteckshack redhat6.5]# cp -rvf /media/RHEL_6.5\ x86_64\ Disc\ 1/*   .
[root@abhiteckshack redhat6.5]# service vsftpd restart
Shutting down vsftpd:                                      [FAILED]
Starting vsftpd for vsftpd:                                [  OK  ]
[root@abhiteckshack redhat6.5]# service vsftpd restart
Shutting down vsftpd:                                      [  OK  ]
Starting vsftpd for vsftpd:                                [  OK  ]
[root@abhiteckshack redhat6.5]#
[root@abhiteckshack redhat6.5]# chkconfig vsftpd on
[root@abhiteckshack redhat6.5]# 


*****************************

Step 4 : Make kickstart file ?

[root@abhiteckshack redhat6.5]# pwd
/var/ftp/pub/redhat6.5
[root@abhiteckshack redhat6.5]# cat ks.cfg
	#platform=x86, AMD64, or Intel EM64T
	#version=DEVEL
	# Firewall configuration
	firewall --enabled --ssh --service=ssh
	# Install OS instead of upgrade
	install
	# Use network installation
	url --url="ftp://192.168.221.155/pub/redhat6.5/"
	# Root password
	rootpw --iscrypted $1$09wfz7y7$.CFklcRChZ6y9j1B1Dw37.
	# System authorization information
	auth  --useshadow  --passalgo=sha512
	# Use graphical install
	graphical
	firstboot --disable
	# System keyboard
	keyboard us
	# System language
	lang en_US
	# SELinux configuration
	selinux --enforcing
	# Installation logging level
	logging --level=info
	# Reboot after installation
	reboot
	# System timezone
	timezone  America/New_York
	# Network information
	network  --bootproto=dhcp --device=eth0 --onboot=on
	# System bootloader configuration
	bootloader --append="crashkernel=auto rhgb quiet" --location=mbr --driveorder="sda"
	# Clear the Master Boot Record
	zerombr
	# Partition clearing information
	clearpart --all  
	# Disk partitioning information
	part / --fstype="ext4" --size=12000
	part /boot --fstype="ext4" --size=1024
	part swap --fstype="swap" --size=2048
	
	%packages
	@base
	@basic-desktop
	@client-mgmt-tools
	@core
	@debugging
	@desktop-debugging
	@desktop-platform
	@directory-client
	@fonts
	@general-desktop
	@graphical-admin-tools
	@input-methods
	@internet-browser
	@java-platform
	@legacy-x
	@network-file-system-client
	@perl-runtime
	@print-client
	@remote-desktop-clients
	@server-platform
	@server-policy
	@x11
	abrt-gui
	certmonger
	device-mapper-persistent-data
	genisoimage
	krb5-workstation
	libXmu
	mtools
	oddjob
	pam_krb5
	pax
	perl-DBD-SQLite
	python-dmidecode
	samba-winbind
	sgpio
	wodim

	%end

[root@abhiteckshack redhat6.5]#
[root@abhiteckshack redhat6.5]#

