# openvpn-as-unlimited
参考 https://github.com/byxkbyxk/openvpn_as_crack 项目拿最新版本改的 (2023年12月份)
# 我的部署环境是 proxmox LXC 环境 ubuntu 22.04 
dpkg -i *.deb    
cp pyovpn-2.0-py3.10.egg.crack /usr/local/openvpn_as/lib/python/pyovpn-2.0-py3.10.egg   
reboot
# 初始化 
/usr/local/openvpn_as/bin/ovpn-init
# 还遇到的问题包括 缺少 /dev/net/tun 
vim /etc/pve/lxc/104.conf   
增加    
lxc.cgroup.devices.allow: c 10:200 rwm   
lxc.mount.entry: /dev/net dev/net none bind,create=dir   

# /sys/fs/cgroup xxx
cgroup v1 v2 需要在启动项  
vim /etc/default/grub  
GRUB_CMDLINE_LINUX="systemd.unified_cgroup_hierarchy=0"  

update-grub && reboot  
