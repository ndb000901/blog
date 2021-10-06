# grub-rescue解决


## 1.执行ls命令

```
ls

# output

(hd0) (hd0,gpt1) (hd0,gpt2) (hd1) (hd1,gpt1) (hd1,gpt2)
```

## 2.执行以下命令

```
ls (hd0,gpt1)

# 依次试，找到输出不是Filesystem is unknown的，找到安装系统的分区
```

## 3.配置

```

# 假设我第二步得到(hd1,gpt7)

set boot=(hd1,gpt7)   #需替换为实际情况

set prefix=(hd1,gpt7)/boot/grub  #需替换为实际情况

insmod normal

normal

进入系统
```


## 4.进入系统后配置

```
sudo update-grub
sudo grub-install /dev/sda
```

## 5.完成
