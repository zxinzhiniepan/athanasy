
## 内核
1.lspci 查看硬件
2.
```shell
```
根据这里安装对应的firmware https://wiki.gentoo.org/wiki/Wifi
BCM43142驱动 https://tutorialforlinux.com/2020/08/28/step-by-step-broadcom-wl-driver-gentoo-installation/
```
emerge -avt broadcom-sta

reboot
```
PS: 安装完一定要重启

## 配置wifi
https://blog.csdn.net/weixin_30661579/article/details/116884944
我正在使用wpa_supplicant创建一个访问点：

wpa_supplicant -D nl80211 -i wlan0 -c /etc/wpa_supplicant_ap.conf

问题是当在接入点配置设备时,我不允许扫描网络：

iw dev

wlan0 scan command failed: Invalid argument (-22)

或者在wpa_cli中：

> scan

OK

<3>CTRL-EVENT-SCAN-FAILED ret=-22

在dmesg：

[85769.193376] CFG80211-ERROR) __wl_cfg80211_scan : Invalid Scan Command at SoftAP mode

[85769.200133] CFG80211-ERROR) wl_cfg80211_scan : scan error (-22)

而且似乎在wl_cfg80211.c里面：

if (dhd->op_mode & DHD_FLAG_HOSTAP_MODE) {undefined

WL_ERR(("Invalid Scan Command at SoftAP mode\n"));

return -EINVAL;

}

所以问题是如果wifi在HOSTAP中,则不允许扫描.

有解决方案吗

ap-force不再有效吗？

iw dev wlan0 scan ap-force
