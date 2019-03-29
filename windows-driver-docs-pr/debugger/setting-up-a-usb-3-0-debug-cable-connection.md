---
title: 手动设置通过 USB 3.0 线缆进行的内核模式调试
description: 调试工具的 Windows 支持内核调试通过 USB 3.0 电缆。 本主题介绍如何设置调试手动的 USB 3.0。
ms.assetid: 9A9F5DA0-B98A-4C19-A723-67D06B2409B5
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 588f12f4fe1080e5df460743405e362a3bba73a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577340"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-manually"></a>手动设置通过 USB 3.0 线缆进行的内核模式调试


调试工具的 Windows 支持内核调试通过 USB 3.0 电缆。 本主题介绍如何设置调试手动的 USB 3.0。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

通过 USB 3.0 电缆调试需要以下硬件：

-   USB 3.0 调试电缆。 这是具有仅 USB 3.0 行和没有 Vbus 的一个交叉电缆。

-   主机 (USB 3.0) xHCI 主控制器上

-   在目标计算机上，支持调试 (USB 3.0) xHCI 主控制器

## <a name="span-idsettingupthecomputerusb3manualspanspan-idsettingupthecomputerusb3manualspansetting-up-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>在目标计算机上安装的设置


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

5.  确定支持调试的 xHCI 控制器后下, 一步是找到与 xHCI 控制器上的端口相关联的物理 USB 连接器。 若要查找实际的连接器，请在目标计算机上任何 USB 连接器中插入任何 USB 3.0 设备。 刷新 UsbView 若要查看你的设备所在的位置。 如果 UsbView 显示你的设备连接到你所选的 xHCI 主控制器，您已找到可以使用 USB 3.0 调试的物理 USB 连接器。

> [!IMPORTANT]
> 使用 bcdedit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。 您可以重新启用安全启动完成后，调试和您禁用了内核调试。  


6. 在目标计算机上，打开命令提示符窗口，以管理员身份，并输入以下命令：

   - **bcdedit /debug 上**
   - **bcdedit /dbgsettings usb targetname:**<em>TargetName</em>

   其中*TargetName*是为目标计算机创建的名称。 请注意， *TargetName*不一定要在目标计算机; 的正式名称可能会创建，只要它满足这些限制的任何字符串：

   -   字符串的最大长度为 24 个字符。
   -   在字符串中的唯一字符是连字符 （-）、 下划线 (\_)，0 到 9 的数字和字母 A 到 Z （上限或下限的情况下）。

7. 如果目标计算机上有多个 USB 主控制器，输入以下命令：

   **bcdedit /set "{dbgsettings}" busparams** *b.d.f*

   其中*b*， *d*，并*f*是总线、 设备和 USB 主控制器，你想要用于调试的函数数量。 总线、 设备和函数编号必须是以十进制格式。

   例如：

   **bcdedit /set "{dbgsettings}" busparams 48.0.0**

8. 重新启动目标计算机。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>启动调试会话的第一次


1.  通用串行总线 (USB) 3.0 调试电缆连接到主机和目标计算机上进行调试您的 USB 3.0 端口。
2.  确定主机计算机上运行的 Windows 的位数 （32 位或 64 位）。
3.  在主计算机上打开的 Windows 主机计算机上运行的位数相匹配 （以管理员身份） 的 WinDbg 的版本。 例如，如果主机计算机运行 Windows 的 64 位版本，请以管理员身份打开 WinDbg 的 64 位版本。
4.  上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**USB**选项卡。输入你设置的目标计算机时创建的目标名称。 单击 **“确定”**。

此时，主机计算机上安装的 USB 调试驱动程序。 这是为什么务必要匹配的位数 WinDbg 到 Windows 的位数。 安装 USB 调试驱动程序后，你可以使用 32 位或 64 位版本的 WinDbg 后续调试会话。

## <a name="span-idstartingthedebuggingsessionusb3manualspanspan-idstartingthedebuggingsessionusb3manualspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_manual"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_MANUAL"></span>启动调试会话


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**USB**选项卡。输入你设置的目标计算机时创建的目标名称。 单击 **“确定”**。

您还可以启动会话使用 WinDbg 通过输入以下命令在命令提示符窗口中，其中*TargetName*是创建时设置的目标计算机的目标名称：

**windbg /k usb:targetname=**<em>TargetName</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

主计算机上打开命令提示符窗口并输入以下命令，其中*TargetName*是创建时设置的目标计算机的目标名称：

**kd /k usb:targetname=**<em>TargetName</em>

## <a name="span-idtroubleshootingtipsfordebuggingoverusb30spanspan-idtroubleshootingtipsfordebuggingoverusb30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>通过 USB 3.0 进行调试的故障排除提示


在某些情况下，power 转换可能会影响调试通过 USB 3.0。 如果您遇到此问题，禁用选择性挂起的 xHCI 主控制器 （和其根集线器） 使用以进行调试。

1.  在设备管理器中，导航到 xHCI 主控制器的节点。 右键单击节点，然后选择**属性**。 如果没有**电源管理**选项卡上，打开选项卡，并清除**允许计算机关闭此设备以节约电源**复选框。
2.  在设备管理器中，导航到 xHCI 主控制器的根中心节点。 右键单击节点，然后选择**属性**。 如果没有**电源管理**选项卡上，打开选项卡，并清除**允许计算机关闭此设备以节约电源**复选框。

完成后对调试使用 xHCI 主控制器的操作后，启用选择性挂起 xHCI 主控制器的功能。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






