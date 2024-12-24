# respring

* `Respring`=`Reboot SpringBoard`=重启桌面=注销

iOS系统内有个默认的，自带的应用：`SpringBoard`

也就是你所看到的：`iPhone的桌面`

每次安装越狱插件，为了使得越狱插件生效，则需要，重启桌面，也就是Respring

常见的重启桌面的方式有：

* 命令行操作：
  * 进入命令行方式
    * Mac中通过ssh进入iPhone的命令行
    * iPhone中通过终端类插件进入命令行
  * 具体命令
    * 方式1：杀掉SpringBoard进程
      ```bash
      killall SpringBoard
      killall -9 SpringBoard
      ```
    * 方式2：`ldrestart`
      ```bash
      ldrestart
      ```
      * 说明：更彻底的一种重启桌面 == 软重启 = soft reboot
    * 方式3：
      ```bash
      launchctl reboot userspace
      ```
      * 说明：暂时还没试过
* 图形界面操作
  * `Filza`安装ipa后-》`右上角`-》`动作`-》`注销`（==`Respring`）
  * palera1n越狱后，`palera1n的app`中-》`Tools`->`Respring`
    * ![palera1n_app_tools_uicache](../../assets/img/palera1n_app_tools_uicache.jpg)
  * XinaA15越狱后，`XinaA15`的app中->`注销`=`Respring`
    * ![xinaa15_respring](../../assets/img/xinaa15_respring.jpg)
