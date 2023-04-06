# 名词解释

越狱前，要了解很多基本概念：

## `jb`=`jailbreak`=越狱

* 技术角度
  * 越狱=iOS越狱=iOS jailbreak = iPhone越狱
    * 含义：获取iOS设备的Root权限的技术手段
* 类比：iPhone=iOS系统，就像一个监狱
  * 普通iPhone的用户，就像在监狱内，虽然被iOS系统管理约束着，也很安全，但是失去了很多自由
  * 想要更加自由，就要从监狱中逃出来 = 越狱
  * 摆脱iOS系统的约束，拥有更多自由
  * 可以安装更多更好的插件、应用等，做之前非越狱时的不能做的各种事情

## 普通越狱 vs rootless无根越狱

* 概述
  * 普通越狱= 有根越狱
    * rootfs可写，包括根目录/也可以写
      * palera1n中也叫：`fakefs-rootful` = `rootful`越狱
  * `rootless`越狱 = 无根越狱
    * rootfs只读，只有/var可写
* 详解
  * 之前的`普通越狱`=`成熟越狱`=`有根越狱` vs `无根越狱`=`rootless jailbreak`
    * 之前的`普通越狱`=`成熟越狱`=`有根越狱`：`iOS 15`之前
      * 越狱工具（有机会利用系统漏洞实现）：对于iOS的根文件系统`rootfs`，去读写
        * 重新挂载根文件系统（为读写）
    * `无根越狱`=`rootless jailbreak`：`iOS 15`之后
      * iOS
        * 内部机制增加了：（Apple的）`SSV`=`Signed System Volume`
          * 细节：对于原本的，被iOS设计为只读readonly的各种系统目录
            * 如果尝试去写入，则会由于filter过滤 和 nullifying而被拒绝 -》即，不允许写入
        * 效果：不允许对于rootfs去写 == `sealed ROOT File System`
      * 越狱工具
        * 无法改动/写入iOS的根文件系统`rootfs`
        * 想要实现越狱，则只能：避免写入=改动iOS 15的`rootfs`
        * 所以：新的iOS 15之后的越狱工具，都是 `rootless jailbreak`=`无根越狱`
          * rootless=对于rootfs没有写入的权限=没法改动rootfs根文件系统
          * 特殊
            * 不过有2个特殊的目录，可以写入：
              * `/var`
              * `/private/preboot`
            * 而新的iOS 15之后的越狱系统，基本上都是利用这个机制，去实现越狱的效果
              * 即：把越狱相关工具和内容，都放到`/var`（和`/private/preboot`）中
        * 说明
          * rootless jailbreak，并不表示没有root用户=root user
            * 你还是可以以`root user`身份去操作：SSH连接到设备，修改（`/var`和`/private/preboot`）中的文件的
          * 由此使得，取消越狱=卸载越狱=恢复原始设备，就变得很容易
            * 因为只是涉及到`/var`和`/private/preboot`，不涉及到整个rootfs的改动和恢复，所以很快很方便
          * 相对来说：绕过越狱检测，相对容易一些
            * 估计指的是，只是针对`/var`，而不是整个系统，所以简单点？
      * rootless有哪些影响
        * **部分插件**`tweak`失效
          * 之前的各种(依赖于旧的rootfs存放文件的)插件tweak：就失效了
            * 需要tweak插件作者去更新，才能支持新的`rootless jailbreak`
        * `bootstrap`也失效了
          * bootstrap：用于启动阶段，安装各种Unix工具，包管理器等等
          * 现在需要用改用：兼容rootless的bootstrap = rootless (compatible) bootstrap
            * 比如
              * `Procursus`
                * 【整理】iOS越狱相关：Procursus
              * `Elucubratus`
        * 文件管理器filesystem browsers：`Filza`, `SSH`, and `Apple File Conduit`
          * 基本可用：只是无法write修改系统目录中文件了（可以读取read和执行execute）
            * 可以写入`/var`和`/private/preboot`目录

## 完美越狱 vs 不完美越狱 vs 半完美越狱 vs 半不完美越狱

* 核心逻辑：2种类型
  * 重启后，是否要（用特殊软件）引导才能开机
    * 是
      * 全越狱=完美越狱
        * 越狱后的iPhone可以正常关机和重启
    * 否
      * 半越狱=不完美越狱
        * iPhone重启后
          * 屏幕就会一直停留在启动画面，也就是“白苹果”状态
          * 或者能正常开机，但已经安装的破解软件都无法正常使用
        * 需要将设备与PC连接后，使用软件进行引导才能使用
  * 重启后，是否还保留越狱状态
    * 是
      * 全越狱
    * 否
      * 半越狱
* 2种核心逻辑组合出4种：越狱类型=Types of Jailbreaks
  * `untethered` = `Untethered jailbreak`= 完美越狱：不需要引导启动
    * 指设备在进行重启后，越狱状态仍被完整保留
  * `semi-untethered`=`Semi-untethered jailbreak`=半完美越狱
    * 指设备在重启后，将丢失越狱状态；而若想要再恢复越狱环境，只需在设备上进行某些操作即可恢复越狱
  * `tethered`=`Tethered jailbreak`=不完美越狱：需要引导启动
    * 当处于此状态的iOS设备开机重启后，之前进行的越狱程序就会失效，用户将失去Root权限，需要将设备连接电脑来使用（如特定版本下的红雪（redsn0w））等越狱软件进行引导开机以后，才可再次使用越狱程序。否则设备将无法正常引导
  * `semi-tethered`=`Semi-tethered jailbreak`=半不完美越狱
    * 指设备在重启后，将丢失越狱状态，并恢复成未越狱状态。如果想要恢复越狱环境，必须连接计算机并在越狱工具的引导下引导来恢复越狱状态

=> 典型越狱效果：

* 很久之前：越狱后，就一直保持越狱状态（完美越狱）
  * 重启iPhone也能保持越狱状态
* 现在：越狱后，重启iPhone会**丢失越狱**（半完美越狱）
  * 所以重启iPhone后，往往还要去：**恢复越狱**
    * 恢复越狱，等于重新执行一遍越狱流程，重新（再次）越狱

## `Respring`=`Reboot SpringBoard`=重启桌面=注销

iOS系统内有个默认的，自带的应用：SpringBoard
也就是：你所看到，iPhone的桌面
每次安装越狱插件，为了使得越狱插件生效，则需要，重启桌面，也就是Respring

常见的重启桌面的方式有：

* Filza安装ipa后-》右上角的动作-》注销（就是 Respring）
* 命令行操作：
  * 进入命令行方式
    * Mac中通过ssh进入iPhone的命令行
    * iPhone中通过终端类插件进入命令行
  * 具体命令
    * `killall SpringBoard`

## `uicache`=清除界面缓存

有时候，需要清理图标等UI的缓存，桌面上才能看到最新的变化

比如：

* （通过某些工具）安装了app后，uicache后，桌面上才能看到已安装的app的图标
* 删除了app后，由于某些原因，需要uicache后，桌面上的app图标才消失
清理UI的cache缓存，有个专门的工具叫做：
* `uicache`

TODO：

* 【整理】UICache是什么和作用
