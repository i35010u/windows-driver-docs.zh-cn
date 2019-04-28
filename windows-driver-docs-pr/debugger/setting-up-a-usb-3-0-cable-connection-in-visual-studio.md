---
title: 在 Visual Studio 中设置通过 USB 3.0 线缆进行的内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行通过 USB 3.0 电缆内核模式调试。
ms.assetid: F8DD0475-13CE-464A-A491-AEFA962A96DB
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed02881634cb1ada2f2cf26a4b4cf8bc80e8ed05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342529"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-in-visual-studio"></a>在 Visual Studio 中设置通过 USB 3.0 线缆进行的内核模式调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

可以使用 Microsoft Visual Studio 设置和执行通过 USB 3.0 电缆内核模式调试。 若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。

使用 Visual Studio 来设置调试的 USB 3.0 的替代方法，您还可以手动执行安装程序。 有关详细信息，请参阅[设置内核模式调试通过 USB 3.0 电缆手动](setting-up-a-usb-3-0-debug-cable-connection.md)。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

通过 USB 3.0 连接调试需要以下硬件：

-   USB 3.0 调试电缆。 这是具有仅 USB 3.0 行和没有 Vbus 的一个交叉电缆。

-   主机 (USB 3.0) xHCI 主控制器上

-   在目标计算机上，支持调试 (USB 3.0) xHCI 主控制器

## <a name="span-idsettingupthecomputerusb3manualspanspan-idsettingupthecomputerusb3manualspanidentifying-a-debug-port-on-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>标识目标计算机上的调试端口


1.  在目标计算机上启动 UsbView 工具。 UsbView 工具包含在为 Windows 调试工具。
2.  在 UsbView 中, 找到所有 xHCI 主控制器。
3.  在 UsbView，展开 xHCI 主控制器的节点。 外观，用于指示主机控制器上的端口支持调试。

    ```console
    [Port1] 

    Is Port User Connectable:         yes
    Is Port Debug Capable:            yes
    Companion Port Number:            3
    Companion Hub Symbolic Link Name: USB#ROOT_HUB30#5&32bab638&0&0#{...}
    Protocols Supported:
     USB 1.1:                         no
     USB 2.0:                         no
     USB 3.0:                         yes
    ```

4.  记下你想要用于调试的 xHCI 控制器的总线、 设备和函数编号。 UsbView 显示这些数字。 在以下示例中，总线数为 48，设备号是 0，函数数为 0。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5.  确定支持调试的 xHCI 控制器后下, 一步是找到与 xHCI 控制器上的端口相关联的物理 USB 连接器。 若要查找实际的连接器，请在目标计算机上任何 USB 连接器中插入任何 USB 3.0 设备。 刷新 UsbView 若要查看你的设备所在的位置。 如果 UsbView 显示你的设备连接至 xHCI 主控制器，您已找到可以使用 USB 3.0 调试的物理 USB 连接器。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  开始配置主机和目标计算机中所述[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)。
2.  主机计算机上，在 Visual Studio 中，当您转至计算机配置对话框中，选择**预配计算机，并选择调试器设置**。
3.  有关**连接类型**，选择**USB**。

    ![屏幕截图显示调试程序的示例具有以下字段的值的设置： 连接类型、 目标名称和总线参数](images/setupusbvs.png)

    有关**目标名称**，输入字符串来表示目标计算机。 此字符串不一定要在目标计算机; 的正式名称它可以是任何字符串，只要它满足这些限制创建：

    -   字符串的最大长度为 24 个字符。
    -   在字符串中的唯一字符是连字符 （-）、 下划线 (\_)，0 到 9 的数字和字母 A 到 Z （上限或下限的情况下）。

    如果目标计算机上有多个 USB 主控制器，请输入**总线参数**的值*b*。*d*。*f*，其中*b*， *d*，并且*f*是总线、 设备和你想要用于调试在 USB 主控制器的函数数量目标计算机。 总线、 设备和函数编号必须是以十进制格式 (示例：48.0.0).

4.  配置过程需要几分钟时间，并可能会自动重新启动目标计算机一次或两次。 该过程完成后，单击**完成**。

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings


在目标计算机上，打开命令提示符窗口，以管理员身份，并输入以下命令：

**bcdedit /dbgsettings**

**bcdedit /enum**

```console
...
targetname              MyUsbTarget
debugtype               USB
debugport               1
baudrate                115200
...
busparams               48.0.0
```

确认*debugtype*是 USB 和*targetname*是在 Visual Studio 中指定主机计算机的名称。 你可以忽略的值*debugport*并*baudrate*; 它们不适用于通过 USB 调试。

如果您输入**总线参数**在 Visual Studio 中，确认*busparams*您指定的总线参数匹配。

如果您看不到值为输入**总线参数**，输入以下命令：

**bcdedit /set "{dbgsettings}" busparams** <em>b</em>**.**<em>d</em>**.**<em>f</em>

其中*b*， *d*，并*f*是总线、 设备和已选择要用于调试的目标计算机上的 xHCI 控制器的函数数量。

例如：

**bcdedit /set "{dbgsettings}" busparams 48.0.0**

重新启动目标计算机。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>启动调试会话的第一次


1.  通用串行总线 (USB) 3.0 调试电缆连接到主机和目标计算机上进行调试您的 USB 3.0 端口。
2.  在主计算机上以管理员身份打开 Visual Studio。
3.  上**工具**菜单中，选择**附加到进程**。
4.  有关**传输**，选择**Windows 内核模式调试程序**。
5.  有关**限定符**，选择以前配置的目标计算机的名称。
6.  单击**附加**。

此时，主机计算机上安装的 USB 调试驱动程序。 这就是原因务必以管理员身份运行 Visual Studio。 安装 USB 调试驱动程序后，您不需要以管理员身份运行后续调试会话。

## <a name="span-idstartingthedebuggingsessionusb3vsspanspan-idstartingthedebuggingsessionusb3vsspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_vs"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_VS"></span>启动调试会话


1.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 内核模式调试程序**。
3.  有关**限定符**，选择以前配置的目标计算机的名称。
4.  单击**附加**。

## <a name="span-idtroubleshootingtipsfordebuggingoverusb30spanspan-idtroubleshootingtipsfordebuggingoverusb30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>通过 USB 3.0 进行调试的故障排除提示


在某些情况下，power 转换可能会影响调试通过 USB 3.0。 如果您遇到此问题，禁用选择性挂起的 xHCI 主控制器 （和其根集线器） 使用以进行调试。

1.  在设备管理器中，导航到 xHCI 主控制器的节点。 右键单击节点，然后选择**属性**。 如果没有**电源管理**选项卡上，打开选项卡，并清除**允许计算机关闭此设备以节约电源**复选框。
2.  在设备管理器中，导航到 xHCI 主控制器的根中心节点。 右键单击节点，然后选择**属性**。 如果没有**电源管理**选项卡上，打开选项卡，并清除**允许计算机关闭此设备以节约电源**复选框。

完成后对调试使用 xHCI 主控制器的操作后，启用选择性挂起 xHCI 主控制器的功能。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






