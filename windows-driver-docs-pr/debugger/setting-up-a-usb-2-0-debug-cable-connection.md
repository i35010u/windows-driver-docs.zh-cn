---
title: 内核模式调试通过 USB 2.0 电缆手动设置
description: 调试工具的 Windows 支持通过 USB 2.0 电缆内核调试。 本主题介绍如何设置调试手动的 USB 2.0。
ms.assetid: 8dd0703a-ddcd-461f-b164-1c079a93bb3a
keywords:
- 安装程序，使 USB 2.0 电缆连接
- 电缆连接，USB 2.0 调试电缆
- USB 2.0 调试连接
- USB 2.0 调试连接、 设置的硬件
- USB 2.0 调试连接，软件要求
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: b22f16ceaec12ebec4d0f5fc5d72f44e6eeac8b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520170"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-manually"></a>内核模式调试通过 USB 2.0 电缆手动设置


调试工具的 Windows 支持通过 USB 2.0 电缆内核调试。 本主题介绍如何设置调试手动的 USB 2.0。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

通过 USB 2.0 电缆调试需要以下硬件：

-   USB 2.0 调试电缆。 此电缆不是标准的 USB 2.0 电缆，因为它具有一个额外的硬件组件，使其与 USB2 调试设备功能规范兼容。 您可以找到与通过 Internet 搜索术语这些电缆*USB 2.0 调试电缆*。

-   在主计算机，EHCI (USB 2.0) 主控制器上

-   在目标计算机上，支持调试 EHCI (USB 2.0) 主控制器

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>在目标计算机上安装的设置


1.  在目标计算机上启动 UsbView 工具。 UsbView 工具包含在为 Windows 调试工具。
2.  在 UsbView 中, 找到的所有主机控制器与 EHCI 规范兼容的。 例如，您可以查找列为增强的控制器。
3.  在 UsbView，依次展开 EHCI 主控制器的节点。 指示主机控制器支持调试，查找并查看调试端口号。 例如，UsbView 显示此支持调试端口 1 上 EHCI 主控制器的输出。

    ```console
    Xxx xxx xxx USB2 Enhanced Host Controller - 293A
    ...
    Debug Port Number:  1
    Bus.Device.Function (in decimal): 0.29.7
    ```

    **请注意**  许多 EHCI 主控制器支持 1，但某些 EHCI 主控制器支持调试端口 2 上的端口上进行调试。

     

4.  记下你想要用于调试的 EHCI 控制器的总线、 设备和函数编号。 UsbView 显示这些数字。 在前面的示例中，总线数为 0，设备号是 29，函数数为 7。

5.  确定 EHCI 控制器以及支持调试的端口号后下, 一步是找到正确的端口号与相关联的物理 USB 连接器。 若要查找实际的连接器，请将任何 USB 2.0 设备插入目标计算机上任何 USB 连接器。 刷新 UsbView 若要查看你的设备所在的位置。 如果 UsbView 显示你的设备连接到 EHCI 主控制器和标识为调试端口的端口，您已找到可用于调试的物理 USB 连接器。 它可能是没有外部的物理 USB 连接器与 EHCI 控制器上的调试端口相关联。 在这种情况下，您可以查找计算机内部的物理 USB 连接器。 执行相同的步骤来确定内部的 USB 连接器是否适用于内核调试。 如果找不到物理 USB 连接器 （外部或内部） 与该键相关联的调试端口，则不能将计算机用作目标通过 USB 2.0 电缆进行调试。

    **请注意**  请参阅[此批注](#what-if-usbview-shows-a-debug-capable-port)的异常。

> [!IMPORTANT]
> 使用 bcdedit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。 您可以重新启用安全启动完成后，调试和您禁用了内核调试。  

   

6. 在目标计算机上，打开命令提示符窗口，以管理员身份，并输入以下命令：

   - **bcdedit /debug 上**
   - **bcdedit /dbgsettings usb targetname:**<em>TargetName</em>

   其中*TargetName*是为目标计算机创建的名称。 请注意， *TargetName*不一定要在目标计算机; 的正式名称可能会创建，只要它满足这些限制的任何字符串：

   -   字符串的最大长度为 24 个字符。
   -   在字符串中的唯一字符是连字符 （-）、 下划线 (\_)，0 到 9 的数字和字母 A 到 Z （上限或下限的情况下）。

7. 如果目标计算机上有多个 USB 主控制器，输入以下命令：

   <span id="Windows_7_or_later"></span><span id="windows_7_or_later"></span><span id="WINDOWS_7_OR_LATER"></span>Windows 7 或更高版本  
   **bcdedit /set "{dbgsettings}" busparams** *b.d.f*

   其中*b*， *d*，并*f*是总线、 设备和主机控制器函数数字。 总线、 设备和函数编号必须是以十进制格式 (例如， **busparams 0.29.7**)。

   <span id="Windows_Vista"></span><span id="windows_vista"></span><span id="WINDOWS_VISTA"></span>Windows Vista  
   **bcdedit /set "{current}" loadoptions busparams=**<em>f.d.f</em>

   其中*b*， *d*，并*f*是总线、 设备和主机控制器函数数字。 总线、 设备和函数编号必须是以十六进制格式 (例如， **busparams = 0.1 D.7**)。

8. 重新启动目标计算机。

## <a name="span-idsetting-up-the-host-computerspanspan-idsettingupthehostcomputerspanspan-idsettingupthehostcomputerspansetting-up-the-host-computer"></a><span id="Setting-Up-the-Host-Computer"></span><span id="setting_up_the_host_computer"></span><span id="SETTING_UP_THE_HOST_COMPUTER"></span>设置主计算机


1.  验证主计算机未配置为作为目标的 USB 调试。 (如果有必要，请打开命令提示符窗口，以管理员身份，请输入**bcdedit /debug 关闭**，并重新启动。)
2.  在主计算机上使用 UsbView 查找 EHCI 主控制器和支持调试的端口。 如果可能，将 USB 2.0 调试电缆的一端插入不支持调试的 EHCI 端口到主机的计算机上）。 否则，将电缆插入任何 EHCI 端口在主计算机上。
3.  USB 2.0 调试电缆另一端插入之前标识目标计算机的连接器。

## <a name="span-idstarting-a-debugging-session-for-the-first-timespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting-a-Debugging-Session-for-the-First-Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>启动调试会话的第一次


1.  确定主机计算机上运行的 Windows 的位数 （32 位或 64 位）。
2.  在主计算机上打开的 Windows 主机计算机上运行的位数相匹配 （以管理员身份） 的 WinDbg 的版本。 例如，如果主机计算机运行 Windows 的 64 位版本，请以管理员身份打开 WinDbg 的 64 位版本。
3.  上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**USB**选项卡。输入你设置的目标计算机时创建的目标名称。 单击“确定” 。

此时，主机计算机上安装的 USB 调试驱动程序。 这是为什么务必要匹配的位数 WinDbg 到 Windows 的位数。 安装 USB 调试驱动程序后，你可以使用 32 位或 64 位版本的 WinDbg 后续调试会话。

**请注意**  USB 2.0 调试电缆是两个电缆实际上用在中间的转换器。 硬件保护装置的方向很重要;一侧为设备提供支持，而另一端不。 如果 USB 调试不起作用，请尝试交换硬件保护装置的方向。 也就是说，拔出从硬件保护装置，两条电缆，交换电缆连接到的方面。

 

## <a name="span-idstarting-a-debugging-sessionspanspan-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanstarting-a-debugging-session"></a><span id="Starting-a-Debugging-Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusing-windbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using-WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**USB**选项卡。输入你设置的目标计算机时创建的目标名称。 单击“确定” 。

您还可以启动会话使用 WinDbg 通过输入以下命令在命令提示符窗口中，其中*TargetName*是创建时设置的目标计算机的目标名称：

**windbg /k usb:targetname=**<em>TargetName</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

主计算机上打开命令提示符窗口并输入以下命令，其中*TargetName*是创建时设置的目标计算机的目标名称：

**kd /k usb:targetname=**<em>TargetName</em>

## <a name="span-idwhat-if-usbview-shows-a-debug-capable-portspanspan-idwhatifusbviewshowsadebugcapableportspanwhat-if-usbview-shows-a-debug-capable-port-but-does-not-show-the-port-mapped-to-any-physical-connector"></a><span id="what-if-usbview-shows-a-debug-capable-port"></span><span id="WHAT_IF_USBVIEW_SHOWS_A_DEBUG_CAPABLE_PORT"></span>如果 USBView 显示了支持调试的端口，但不显示的端口映射到任何物理连接器？


在某些计算机上 USBView 显示了支持调试的端口，但不显示映射到任何物理 USB 连接器的端口。 例如，USBView 可能显示端口 2 为 eHCI 控制器的调试端口号。

```console
... USB Enhanced Host Controller ...
...
Debug Port Number:  2
Bus.Device.Function (in decimal): 0.29.0
```

此外，当使用 USBView 来查看单个端口，则将它列出为支持调试的。

```console
[Port 2]
Is Port User Connectiable: Yes
Is Port Debug Capable: Yes
...
Protocols Supported
  USB 1.1      yes
  USB 2.0      yes
  USB 3.0      no
```

但 USBView 时插入到计算机上的所有 USB 连接器的 USB 2.0 设备 （如闪存驱动器） 中，永远不会显示你的设备连接到支持调试的端口 （在此示例中的端口 2）。 USBView 可能会显示映射到一个端口的 xHCI 控制器端口时实际上外部连接器已映射到 eHCI 控制器支持调试的端口的外部连接器。

![xhci 和 ehci usbview 中的屏幕截图](images/usbview01.png)

在这种情况下，你仍可能能够建立内核模式下通过 USB 2.0 电缆调试。 在此处提供示例中，将显示为映射到端口的 xHCI 控制器 2 在连接器插入 USB 2.0 调试缆线。 然后你将在总线参数设置为总线、 设备和 eHCI 控制器 （在此示例中，0.29.0） 的函数数量。

**bcdedit /set "{dbgsettings}" busparams 0.29.0**

### <a name="span-idsoftware-setupspanspan-idsoftwaresetupspanadditional-support"></a><span id="software-setup"></span><span id="SOFTWARE_SETUP"></span>其他支持

有关故障排除提示和设置内核调试通过 USB 的详细的说明，请参阅[设置内核调试与 USB 2.0](https://go.microsoft.com/fwlink/p?linkid=389435)。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关的主题


[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






