- ## 定时更新固件测试，一定要先设置好发布密匙，因为检测更新是检测github的发布地址

- ### 理论上在openwet后台可以升级的都应该可以支持定时更新，后台升级地址｛openwrt-系统-备份/升级｝，R2S/R4S这些用TF卡的就不支持，N1不支持

- ### 测试方法，分别在两个时间段启动编译，比如1:00启动一个编译,然后1:05分启动一个编译，完成后，安装1:00的，就会自动检测到1:05的
#
- ### 在build/机型文件夹/settings.ini，以下三项设置好就可以把定时更新固件的插件编译进openwrt

```
REGULAR_UPDATE="false"        #把定时自动更新编译进固件（true=开启）（false=关闭）
Updete_firmware="squashfs-combined.img.gz"     #你在openwrt后台升级时候所用的固件名称
Extension=".img.gz"       #你在openwrt后台升级时候所用的固件名称的后缀，后缀要带点的，比如【x86是.img.gz】【k3是.trx】【newifi-d2是.bin】
```

- ### 自动在你现有的.config配置增加以下二个插件，免除SSH进去选择
```
luci-app-autoupdate=y    定时更新插件
luci-app-ttyd=y        openwrt内置SSH命令窗
```
---
- ### 使用命令更新固件脚本和扩展空间:
```
首先需要打开 Openwrt 主页,点击系统-TTYD 终端或命令窗,按需输入下方指令:

检查更新(保留配置): bash /bin/AutoUpdate.sh

检查更新(不保留配置): bash /bin/AutoUpdate.sh -n


使用一键扩展内部空间\挂载 Samba 共享脚本:
同上方操作,打开TTYD 终端或命令窗,输入bash /bin/AutoBuild_Tools.sh
```
---
- ### 定时更新设置:
- 首先需要打开 Openwrt 主页,点击系统-定时更新 ，定时更新勾选上，设置好时间，保存设置就可以了（定时自动更新是保留配置更新的）


---
## 鸣谢

   - [Hyy2001X](https://github.com/Hyy2001X/AutoBuild-Actions)

   - [dhxh](https://github.com/dhxh/Openwrt-Build)

   - 定时更新脚本是由[dhxh](https://github.com/dhxh/Openwrt-Build)从[Hyy2001X](https://github.com/Hyy2001X/AutoBuild-Actions)基础修改完成
