
Android分区大致可以分为四类：
- 1.系统分区
- 2.Cache分区
- 3.数据分区
- 4.SD卡分区
## 系统分区
系统分区一般被加载为只读分区，包括系统函数库，系统内核，实时运行框架，系统应用，应用框架等。系统分区由厂商植入，一般外界不能更改。当系统出现安全问题一般页就只加载这个分区进行恢复。
## Cache 分区
Cache 分区就是目录分区，不同目录加载不同内容
- /system/app 存放系统应用
- /system/lib 存放系统库
- /system/bin   /system/xbin 存放系统管理命令
- /system/framework 存放安卓应用系统框架里的jar文件
## 数据分区
数据分区用于存储各类应用数据和应用程序，我们下载安装的应用程序一般存放在这里，Android数据分区加载的目录主要为/data，子目录有

- /data/data： 保存所有apk程序
- /data/app：保存用户安装apk
- /data/system：保存用于记录安装的软件及widget等
- /data/msic：用于保存wifi及vpn设置等

## SDK 分区
SDK属于外设，一般不受android系统控制
