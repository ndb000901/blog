## VMWare - Could not connect 'Ethernet0' to virtual network '/dev/vmnet0'.

```
sudo modprobe vmnet && sudo vmware-networks --start
sudo systemctl start vmware-networks.service
```


## 解决Could not open /dev/vmmon: ?????????. Please make sure that the kernel module vmmon is loaded
查看系统内核
```
# uname -r
5.4.18-1-MANJARO
```
安装 linux-headers
```
sudo pacman -S linux54-headers
```
启用相关模块
```
sudo modprobe -a vmw_vmci vmmon
```


## Fail Network configuration is missing. Ensure that /etc/vmware/-networking exists.
```
systemctl start vmware-networks-configuration.service
systemctl enable vmware-networks-configuration.service
```



## Fail Network configuration is missing. Ensure that /etc/vmware/-networking exists.
```
systemctl start vmware-networks-configuration.service
systemctl enable vmware-networks-configuration.service



## 解决Could not open /dev/vmmon: ?????????. Please make sure that the kernel module vmmon is loaded
查看系统内核
```
# uname -r
5.4.18-1-MANJARO
```
安装 linux-headers
```
sudo pacman -S linux54-headers
```
启用相关模块
```
sudo modprobe -a vmw_vmci vmmon
```


## VMWare - Could not connect 'Ethernet0' to virtual network '/dev/vmnet0'.

```
sudo modprobe vmnet && sudo vmware-networks --start
sudo systemctl start vmware-networks.service