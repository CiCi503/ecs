# 使用软件连接Windows实例 {#concept_n31_wyx_wdb .concept}

如果您的实例不能访问公网，您可以 [使用管理终端连接 ECS 实例](cn.zh-CN/用户指南/连接实例/使用管理终端连接 ECS 实例.md#)。

## 前提条件 {#section_hxc_qcy_wdb .section}

在远程连接之前，必须先完成以下工作：

-   实例状态必须为 **运行中**。如果实例运行，必须 [启动或停止实例](cn.zh-CN/用户指南/实例/启动或停止实例.md#)。
-   实例已经设置登录密码。如果未设置或密码丢失，必须 [重置实例密码](cn.zh-CN/用户指南/实例/重置实例密码.md#)。
-   实例能访问公网：
    -   专有网络（VPC）下，您应该在创建实例时购买带宽分配到一个公网IP地址，或者在创建实例后 [绑定一个弹性公网IP（EIP）地址](https://help.aliyun.com/document_detail/27714.html)。
    -   经典网络下，您的实例必须分配了公网IP地址。以下是获取公网IP地址的方法：
        -   无论是包年包月实例还是按量计费实例，您在创建实例时购买了带宽即会被分配一个公网IP地址。
        -   如果您在创建包年包月实例时未设置带宽，可以 [升降配概述](cn.zh-CN/用户指南/实例/升降配/升降配概述.md#) 获取公网IP地址。
-   实例所在的安全组必须添加以下安全组规则（具体操作，请参考 [添加安全组规则](cn.zh-CN/用户指南/安全组/添加安全组规则.md#)）：

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |----|----|----|----|----|----|----|----|---|
    |VPC|不需要配置|入方向|允许|RDP\(3389\)|3389/3389|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 操作步骤 {#section_b55_ycy_wdb .section}

根据本地设备的操作系统不同，您可以用不同的远程连接软件连接 Windows 实例：

-   [本地设备使用Windows操作系统](#windows)
-   [本地设备使用Linux操作系统](#linux)
-   [本地设备使用Mac OS操作系统](#macOS2)
-   [本地设备使用Android或iOS系统](#mobile)

## 本地设备使用Windows操作系统 {#windows .section}

如果本地设备使用Windows操作系统，您可以使用Windows自带的远程桌面连接工具MSTSC连接Windows实例。

**说明：** 具体操作，您也可以观看视频：[小助手系列之如何远程连接Windows实例](https://help.aliyun.com/document_detail/62303.html?spm=a2c4g.11186623.2.14.PAoDa5)。

1.  选择以下任一方式启动 **远程桌面连接**（MSTSC\)：
    -   选择 **开始** \> **附件** \> **远程桌面连接**。
    -   单击 **开始** 图标，在搜索框里中输入 后按回车键确认。
    -   按快捷键 **Win**（Windows 徽标键）+**R** 启动 运行 窗口，输入 mstsc 后按回车键。
2.  在 v 对话框中：
    1.  单击 **显示选项**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5258_zh-CN.png)

    2.  输入实例的公网IP地址或EIP地址。
    3.  输入用户名，默认为 Administrator。

        **说明：** 如果您希望下次登录时不再手动输入用户名和密码，可以选择 **允许我保存凭据**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5259_zh-CN.png)

    4.  （可选）如果您希望将本地文件拷贝到实例中，您可以设置通过远程桌面共享本地电脑资源：单击 **本地资源** 选项卡，然后，
        -   如果您需要从本地直接复制文字信息到实例中，选择 **剪贴板**。
        -   如果您需要从本地复制文件到实例中，单击 **详细信息**，选择驱动器后再选择文件存放的盘符。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5260_zh-CN.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5261_zh-CN.png)

    5.  （可选）如果您对远程桌面窗口的大小有特定的需求，可以选择 **显示** 选项卡，再调整窗口大小。一般选择全屏。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5262_zh-CN.png)

    6.  单击 **连接**。

成功连接到实例后，您就可以开始操作实例了。

## 本地设备使用Linux操作系统 {#linux .section}

如果本地设备使用Linux操作系统，您可以使用远程连接工具连接Windows实例。这里以rdesktop为例说明。

1.  下载并启动rdesktop。
2.  运行以下命令连接Windows实例。将示例中的参数改为您自己的参数。

    ```
    rdesktop -u administrator -p password -f -g 1024*720 192.168.1.1 -r clipboard:PRIMARYCLIPBOARD -r disk:sunray=/home/yz16184
    ```

    参数说明如下表所示。

    |参数|说明|
    |:-|:-|
    |-u|用户名，Windows实例默认用户名是Administrator。|
    |-p|登录Windows实例的密码。|
    |-f|默认全屏，需要用 **Ctrl**+**Alt**+**Enter** 组合键进行全屏模式切换。|
    |-g|分辨率，中间用星号（\*）连接，可省略，省略后默认为全屏显示。|
    |192.168.1.1|需要远程连接的服务器IP地址。需要替换为您的Windows实例的公网IP地址或 EIP 地址。|
    |-d|域名，例如域名为INC，那么参数就是 `-d inc`。|
    |-r|多媒体重新定向。比如：    -   开启声音：`-r sound`。
    -   使用本地的声卡：`-r sound : local`。
    -   开启 U 盘：`-r disk:usb=/mnt/usbdevice`。
|
    |-r clipboard:PRIMARYCLIPBOARD|实现本地设备Linux系统和Windows实例之间直接复制粘贴文字。支持复制粘贴中文。|
    |-r disk:sunray=/home/yz16184|指定本地设备Linux系统上的一个目录映射到Windows实例上的硬盘， 这样就可以不再依赖Samba或者FTP传送文件。|


## 本地设备使用Mac OS操作系统 {#macOS2 .section}

从Mac OS上连接Windows实例时，您必须在 [Mac App Store](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?spm=a2c4g.11186623.2.15.PAoDa5&mt=12&ls=1) 先下载并安装Microsoft Remote Desktop Connection for Mac。如果只有中国Apple账号，您可以从 [HockeyApp](https://rink.hockeyapp.net/apps/5e0c144289a51fca2d3bfa39ce7f2b06/?spm=a2c4g.11186623.2.16.PAoDa5) 下载微软官方提供的Microsoft Remote Desktop for Mac Beta版。该软件只适用于Mac OS 10.10及以上版本系统。

这部分内容以Microsoft Remote Desktop for Mac Beta版（以下简称为MRD Beta）为例说明如何从Mac OS上连接Windows实例：

-   [首次连接](#firstConnection)
-   [再次连接](#notFirstConnection)

**首次连接**

您首次在Mac OS上使用MRD Beta连接Windows实例时，请按以下步骤操作：

1.  启动MRD Beta。
2.  单击 **Get started**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5291_zh-CN.png)

3.  在 Quick connect 窗口，输入Windows实例的公网IP地址或EIP地址，并单击 **Connect**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5292_zh-CN.png)

4.  在弹出对话框中，输入登录信息：
    -   User Name：输入 administrator。Windows实例的默认用户名是 administrator。
    -   Password：输入实例登录密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5295_zh-CN.png)

5.  在弹出对话框中，单击 **Continue**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5296_zh-CN.png)


至此，您已经成功登录Windows实例桌面。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5297_zh-CN.png)

**再次连接**

第二次及以后在Mac OS上使用MRD Beta连接Windows实例时，请按以下步骤操作：

1.  启动MRD Beta。
2.  单击 **Add desktop**，并在弹出的 Add Desktop 对话框中，设置 PC Name 并选择以后连接的方式（User Account），并单击 **Save**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5298_zh-CN.png)

3.  选中实例图标。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5300_zh-CN.png)

4.  在工具栏里，选择 **![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/25435/intl_zh/1509777290006/Setting_icon.png)** \> **Connect**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5301_zh-CN.png)

5.  在弹出对话框中，输入登录信息：
    -   User Name：输入 administrator。Windows实例的默认用户名是 administrator。
    -   Password：输入实例登录密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5302_zh-CN.png)

6.  在弹出对话框中，单击 **Continue**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5303_zh-CN.png)


至此，您已经成功登录Windows实例桌面。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5304_zh-CN.png)

## 本地设备使用Android或iOS系统 {#mobile .section}

如果要使用移动设备远程连接您的Windows实例时，您可以使用app。具体的操作描述，请参考 [在移动设备上连接实例](cn.zh-CN/用户指南/连接实例/在移动设备上连接实例.md#)。

## 参考链接 {#section_i43_fgz_wdb .section}

连接失败，您可以参考这个文档排查问题：[无法连接Windows实例](https://help.aliyun.com/document_detail/50982.html?spm=a2c4g.11186623.2.20.PAoDa5)。

