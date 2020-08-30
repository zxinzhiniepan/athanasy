# software

## 时间
> windows和linux双系统时间不一致问题

> UTC时间:协调世界时,是以原子时秒长为基础，在时刻上尽量接近世界时的一种时间计量系统
> GMT时间:格林尼治所在地的标准时间

**GMT（格林威治时间）、CST（北京时间）、PST（太平洋时间）等等是具体的时区。**
```
GMT: UTC +0    =    GMT: GMT +0
CST: UTC +8    =    CST: GMT +8
PST: UTC -8    =    PST: GMT -8
```

### manjaro时间同步
```
ntpdate -u ntp.api.bz
```

### 电脑时间区别
硬件时间：BIOS保存的时间，无时区和夏令时的概念
系统时间：独立硬件时间，有时区和夏令时的区别
windos和linux使用了两种不同的时间管理方式：
* localtime: 本地时间，目前只有windows在使用
* UTC: 世界标准时间
* windows将bios时间看成本地时间
* linux则是默认将bios时间看出UTC时间
#### 解决办法
##### a. windows修改注册表
```
# 以管理员身份使用运行
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f

# 以上方法无效或64位系统：
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_QWORD /f
```
##### b.修改linux使用localtime
```
sudo timedatectl set-local-rtc true # manjaro、arch设置
```
