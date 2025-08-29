# ubuntu 使用笔记 

# 备忘

## 开机引导

- Ubuntu 安装完后默认启动项是 Ubuntu 按需改成默认 Windows 启动。

#### 打开终端：

- 在 Ubuntu 桌面右键，选择“在终端中打开”。

- 打开GRUB配置文件
~~~
sudo vi /etc/default/grub
~~~
#### 修改配置文件：
- 设置默认启动项：:找到 `GRUB_DEFAULT` 这一行，将其值改为您希望默认启动的系统在菜单中的顺序（例如，`GRUB_DEFAULT=2` 表示第三个选项）。

- 设置引导菜单显示时间：:找到 `GRUB_TIMEOUT`，将其值改为您希望菜单显示的秒数，例如 `GRUB_TIMEOUT=10`。

- 取消隐藏引导菜单：:如果存在 `GRUB_TIMEOUT_STYLE=hidden`，请在其前面添加 `#` 注释掉。

#### 使其生效
~~~
sudo update-grub
~~~
#### 重启验证

- 重启电脑后，您应该能看到修改后的引导菜单。

## 系统切换导致的时间不同步

- Windows将硬件时间(RTC)作为系统显示的时间。
- Linux将硬件时间(RTC)作为UTC, 然后将UTC+8作为系统时间。
- 这就导致了二者之间的不同, windows 时间会慢 8小时。

### Ubuntu 下解决方案
~~~
//在Ubuntu下更新本地时间
sudo apt-get install ntpdate					
sudo ntpdate time.windows.com
//将本地时间更新到硬件上
sudo hwclock --localtime --systohc
~~~
### Windows 下解决方案
~~~
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
~~~