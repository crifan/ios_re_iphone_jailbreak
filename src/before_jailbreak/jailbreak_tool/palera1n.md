# palera1n

* palera1n
  * 资料
    * 主页
      * https://palera.in/
        * palera1n is a developer-oriented jailbreak for checkm8 devices (A8-A11) on iOS 15.0-16.3
    * github
      * https://github.com/palera1n/
        * https://github.com/palera1n/palera1n
  * 前提条件
    * checkm8 vulnerable iOS device
  * 支持的iOS版本：`iOS/iPadOS 15+`
    * iOS 15.x or 16.x
      * iOS 15.0 ~ iOS 16.3.1
  * 支持的iOS设备
    * 芯片类型/架构：`arm64`
      * `A11`及之前
        * 注：`A12+`（架构是`arm64e`）就不支持了
    * 机型
      * iPhone 6s Plus
      * iPhone SE (2016)
      * iPhone 7
      * iPhone 7 Plus
      * iPhone 8
      * iPhone 8 Plus
      * iPhone X
      * 
      * iPad mini 4
      * iPad Air 2
      * iPad (5th generation)
      * iPad (6th generation)
      * iPad (7th generation)
      * iPad Pro (9.7")
      * iPad Pro (12.9") (1st generation)
      * iPad Pro (10.5")
      * iPad Pro (12.9") (2nd generation)
      * 
      * iPod Touch (7th generation)
  * 支持2种越狱模式/越狱类型
    * `rootful` = `fakefs-rootful` = `普通越狱` = `有根越狱`：rootfs可写，包括根目录/也可以写
    * `rootless` = `无根越狱`：rootfs只读，只有/var可写
  * 推荐的越狱模式
    * rootful越狱=有根越狱=普通越狱
      * 这样对于之前的兼容性会更好
      * 很多插件等，应该可以正常工作了
      * 比如希望的`frida`等等
  * 越狱的核心步骤
    * Mac中给iPhone越狱
      * Mac中
        * 下载Mac版的`palera1n-macos-universal`
          * 此处版本：palera1n v2.0.0-beta.4
        * `palera1n -c -f`
          * Enter
          * 进入DFU模式
            * 长按 `音量减键`➖ 和 `电源键`
            * （不要松手，继续）长按 `音量减键`➖
        * `palera1n -c`
      * iPhone中
        * palera1n的app中：点击`Install`

## palera1n越狱的前提条件

* 要满足一系列条件
  * If you want the device to be semi-tethered, you will need 5-10GB of space for the fakefs. This means that 16GB devices cannot be semi-tethered
  * If you are on A10(X), use checkp4le instead for full SEP functionality (Passcode, TouchID, Apple Pay)
  * On A11, you must disable your passcode while in the jailbroken state (on iOS 16, you need to reset your device before proceeding with palera1n A11).
  * USB-A cables are recommended to use, USB-C may have issues with palera1n and getting into DFU mode.
  * A Linux or macOS computer
    * Python 3 must be installed
    * AMD CPUs have an issue [with (likely) their USB controllers] that causes them to have a very low success rate with checkm8. It is not recommended that you use them with palera1n. If your device does not successfully jailbreak, try a computer with an Intel or other CPU

## palera1n越狱的相关说明

* 注意事项和说明
  * palera1n jailbreaks any iOS/iPadOS device with an arm64 (arm64e excluded) on iOS 15+, utilizing the checkm8 bootROM exploit.
    * 不支持A11之后的arm64e
      * 注：我之前的iPhone11，就是A12芯片，就是arm64e，所以不支持
  * arm64e devices will NEVER be supported.
    * 永远不会支持arm64e
  * palera1n is able to jailbreak the device in fakefs-rootful mode, where / is writable, as well as rootless mode, where / cannot be written to.
    * palera1n支持：
      * fakefs-rootful = rootful=伪造根文件系统 越狱：根目录/可写入
      * rootless=无根越狱：根目录/不可写入
  * Due to the nature of the checkm8 exploit, palera1n is semi-tethered. That is, you must run the palera1n tool after the device reboot in order to enter the jailbroken state. However, it is not required for the device to boot.
    * 是非完美越狱：
      * 原因：checkm8决定的
        * 结果：每次重启（iPhone）后，要重新运行palera1n（去恢复越狱）
          * 注：启动boot时不需要
  * On A11 devices, that is, iPhone 8, iPhone 8 Plus and iPhone X, the passcode cannot be used.
    * A11设备（iPhone8、iPhone 8P、iPhoneX）中，不能用passcode
  * On iOS 15, the passcode must be off while jailbroken.
    * iOS 15中必须关闭passcode（才能越狱）
  * On iOS 16, the passcode must be off since restore, and Reset All Contents and Settings from settings app counts as a restore. A backup may be used in this case.
    * iOS 16中，passcode必须关闭，且如果之前开启过passcode，则需要恢复出厂设置=重置系统

## 要清楚palera1n越狱工具的版本

* `palera1n`越狱工具的版本
  * Windows用：`palen1x`
    * 文档：
      * [Using palen1x | iOS Guide (cfw.guide)](https://ios.cfw.guide/using-palen1x/)
      * [palera1n/docs: GitBook docs for palera1n (github.com)](https://github.com/palera1n/docs)
        * [docs/flashing-palen1x.md](https://github.com/palera1n/docs/blob/main/palen1x/flashing-palen1x.md)
        * [docs/booting-palen1x.md](https://github.com/palera1n/docs/blob/main/palen1x/booting-palen1x.md)
        * [docs/jailbreak-with-palen1x.md](https://github.com/palera1n/docs/blob/main/palen1x/jailbreak-with-palen1x.md)
    * 代码仓库
      * palera1n/palen1x: Alpine-based distro that lets you install rootful and rootless palera1n-c. (github.com)
        * https://github.com/palera1n/palen1x/
  * Linux/Mac的用：`palera1n`，有2个版本
    * `shell script`
      * 旧版本是个`palera1n.sh`脚本
      * 旧版本的教程
        * [Installing palera1n (Legacy) | iOS Guide (cfw.guide)](https://ios.cfw.guide/installing-palera1n-legacy/)
          * 核心命令
            * `./palera1n.sh --tweaks 15.6.1 --semi-tethered`
    * （ 编译好的 电脑端的 直接可用的）`二进制`
      * 代码仓库
        * [palera1n/palera1n-c: palera1n written in C (github.com)](https://github.com/palera1n/palera1n-c)
          * palera1n written in C
            * 是个用C写的，在PC端（Mac、Linux等）中运行的，palera1n的二进制程序
      * 下载地址
        * [Releases · palera1n/palera1n-c (github.com)](https://github.com/palera1n/palera1n-c/releases)
          * macOS
            * palera1n-macos-universal
              * 截至20230302最新版：v2.0.0-beta.4
                * https://github.com/palera1n/palera1n-c/releases/download/v2.0.0-beta.4/palera1n-macos-universal
      * 常用参数
        * `-c`, `--setup-fakefs`       Setup fakefs
          * When used with -f, --fakefs, Create the new APFS volume required for rootful. Will fail if one already exists.
        * `-f`, `--fakefs`              Boots fakefs
          * Jailbreak in rootful mode.
        * `-l`, `--rootless`            Boots rootless. This is the default
        * `-v`, `--debug-logging`      Enable debug logging
          * This option can be repeated for extra verbosity.
        * `-V`, `--verbose-boot`       Verbose boot
      * 常见用法
        * `palera1n -cf` == `palera1n -c -f`
          * 创建fakefs
        * `palera1n -f`
          * 启动设备
        * `palera1n` == `palera1n -l` == `palera1n --rootless`
          * 无任何参数的启动，（默认）以rootless方式去越狱
            * 注意：rootless模式下支持的tweak插件很少
        * 常见用法对比
          * `palera1n -f`：`f`=`Fakefs`=`rootFul`
          * `palera1n` == `palera1n -l`：`l`=`rootLess`
      * 完整用法=语法=帮助
        * `palera1n --help`
        * 或 在线的html文档
          * palera1n - nickchan.lol
            * https://cdn.nickchan.lol/palera1n/c-rewrite/releases/v2.0.0-beta.4/palera1n.1.html
            * https://cdn.nickchan.lol/palera1n/artifacts/c-rewrite/palera1n.1.html
