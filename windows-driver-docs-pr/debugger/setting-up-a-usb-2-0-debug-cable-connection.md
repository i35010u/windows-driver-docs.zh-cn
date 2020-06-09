---
title: 手动设置通过 USB 2.0 线缆进行的内核模式调试
description: 适用于 Windows 的调试工具支持通过 USB 2.0 电缆进行内核调试。 本主题介绍如何手动设置 USB 2.0 调试。
ms.assetid: 8dd0703a-ddcd-461f-b164-1c079a93bb3a
keywords:
- 安装程序，建立 USB 2.0 电缆连接
- 电缆连接，USB 2.0 调试电缆
- USB 2.0 调试连接
- USB 2.0 调试连接，设置硬件
- USB 2.0 调试连接，软件要求
ms.date: 02/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: d796a1fb9bb99d8f0684c916bcf1e8c4204222d1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534764"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-manually"></a>手动设置通过 USB 2.0 线缆进行的内核模式调试


适用于 Windows 的调试工具支持通过 USB 2.0 电缆进行内核调试。 本主题介绍如何手动设置 USB 2.0 调试。

运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。

通过 USB 2.0 电缆进行调试需要以下硬件：

-   USB 2.0 调试电缆。 此电缆不是标准 USB 2.0 电缆，因为它具有额外的硬件组件，使其与 USB2 调试设备功能规范兼容。 可以通过 Internet 搜索术语 " *USB 2.0 调试电缆*" 找到这些缆线。

-   在主计算机上，EHCI （USB 2.0）主机控制器

-   在目标计算机上，支持调试的 EHCI （USB 2.0）主机控制器

## <a name="setting-up-the-target-computer"></a>设置目标计算机


1.  在目标计算机上，启动 UsbView 工具。 UsbView 工具包含在 Windows 调试工具中。
2.  在 UsbView 中，找到与 EHCI 规范兼容的所有主机控制器。 例如，你可以查找列为 "增强" 的控制器。
3.  在 UsbView 中，展开 EHCI 主机控制器的节点。 查找主机控制器支持调试的指示，并查找调试端口的数量。 例如，UsbView 显示在端口1上支持调试的 EHCI 主机控制器的此输出。

    ```console
    Xxx xxx xxx USB2 Enhanced Host Controller - 293A
    ...
    Debug Port Number:  1
    Bus.Device.Function (in decimal): 0.29.7
    ```

    **注意**   许多 EHCI 主机控制器支持在端口1上进行调试，但某些 EHCI 主机控制器支持在端口2上进行调试。

     

4.  记下要用于调试的 EHCI 控制器的总线、设备和功能号。 UsbView 显示这些数字。 在前面的示例中，总线号为0，设备号为29，而函数号为7。

5.  确定 EHCI 控制器和支持调试的端口号后，下一步是找到与正确的端口号关联的物理 USB 连接器。 若要查找物理连接器，请将任何 USB 2.0 设备插入目标计算机上的任何 USB 连接器。 刷新 UsbView 以查看设备所在的位置。 如果 UsbView 显示已连接到 EHCI 主机控制器的设备和标识为调试端口的端口，则已找到可用于调试的物理 USB 连接器。 可能没有与 EHCI 控制器上的调试端口关联的外部物理 USB 连接器。 在这种情况下，可以在计算机中查找物理 USB 连接器。 执行相同的步骤，确定内部 USB 连接器是否适用于内核调试。 如果找不到与调试端口关联的物理 USB 连接器（外部或内部），则不能使用该计算机作为通过 USB 2.0 电缆进行调试的目标。

    **注意**   对于异常，请参阅[此注释](#what-if-usbview-shows-a-debug-capable-port)。

> [!IMPORTANT]
> 使用 bcdedit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。 完成调试并禁用内核调试之后，可以重新启用安全启动。  

6. 在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令：

   - **bcdedit/debug on**
   - **bcdedit/dbgsettings usb targetname：**<em>targetname</em>

   其中*TargetName*是您为目标计算机创建的名称。 请注意， *TargetName*不必是目标计算机的正式名称;它可以是您创建的任何字符串，只要它满足以下限制：

   -   字符串不得以大写或小写的任意组合包含在*TargetName*中任意位置的 "debug"。 例如，如果在 targetname 中的任何位置使用 "调试" 或 "调试"，则调试将不会正常工作。  
   -   字符串中的唯一字符是连字符（-）、下划线（ \_ ）、0到9的数字以及从 A 到 Z 的字母（大写或小写）。
   -   字符串的最大长度为24个字符。

7. 如果目标计算机上存在多个 USB 主机控制器，请输入以下命令：

   <span id="Windows_7_or_later"></span><span id="windows_7_or_later"></span><span id="WINDOWS_7_OR_LATER"></span>Windows 7 或更高版本  
   **bcdedit/set "{dbgsettings}" busparams** *b.d.f*

   其中， *b*、 *d*和*f*是主机控制器的总线、设备和函数号。 总线、设备和函数编号必须为十进制格式（例如**busparams 0.29.7**）。

   <span id="Windows_Vista"></span><span id="windows_vista"></span><span id="WINDOWS_VISTA"></span>Windows Vista  
   **bcdedit/set "{current}" loadoptions busparams =**<em>f. f</em>

   其中， *b*、 *d*和*f*是主机控制器的总线、设备和函数号。 总线、设备和函数编号必须是十六进制格式（例如， **busparams = 0.1 d. 7**）。

8. 重新启动目标计算机。

## <a name="setting-up-the-host-computer"></a>设置主计算机


1.  验证主机计算机未配置为 USB 调试的目标。 （如有必要，请以管理员身份打开命令提示符窗口，输入**bcdedit/debug off**，然后重新启动。）
2.  在主计算机上，使用 UsbView 查找 EHCI 主机控制器和支持调试的端口。 如果可能，请将 USB 2.0 调试电缆的一端插入不支持调试的 EHCI 端口（在主机计算机上）。 否则，请将电缆插入主机计算机上的任何 EHCI 端口。
3.  将 USB 2.0 调试电缆的另一端插入到之前在目标计算机上标识的连接器。

## <a name="starting-a-debugging-session-for-the-first-time"></a>首次启动调试会话


1.  确定主机计算机上运行的 Windows 的位数（32位或64位）。
2.  在主计算机上，打开与主计算机上运行的 Windows 的位数相匹配的 WinDbg 版本（以管理员身份）。 例如，如果主计算机运行的是64位版本的 Windows，请以管理员身份打开该版本的 WinDbg 的64位版本。
3.  在 "**文件**" 菜单上，选择 "**内核调试**"。 在 "内核调试" 对话框中，打开 " **USB** " 选项卡。输入在设置目标计算机时创建的目标名称。 单击 **“确定”** 。

此时，将在主计算机上安装 USB 调试驱动程序。 这就是将 WinDbg 的位数与 Windows 的位数相匹配的原因。 安装 USB 调试驱动程序之后，可以使用32位或64位版本的 WinDbg 来执行后续的调试会话。

**注意**   USB 2.0 调试电缆实际上是两条电缆，其中的连接器位于中间。 转换器的方向非常重要;一侧为设备供电，而另一端则不支持。 如果 USB 调试不起作用，请尝试交换转换器的方向。 也就是说，从转换器拔出两根电缆，并交换电缆连接到的边。


## <a name="starting-a-debugging-session"></a>启动调试会话

### <a name="using-windbg"></a>使用 WinDbg

在主计算机上，打开 WinDbg。 在 "**文件**" 菜单上，选择 "**内核调试**"。 在 "内核调试" 对话框中，打开 " **USB** " 选项卡。输入在设置目标计算机时创建的目标名称。 单击 **“确定”** 。

还可以通过在命令提示符窗口中输入以下命令来启动与 WinDbg 的会话，其中*TargetName*是设置目标计算机时创建的目标名称：

**windbg/k usb： targetname =**<em>targetname</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

在主计算机上，打开命令提示符窗口并输入以下命令，其中*TargetName*是设置目标计算机时创建的目标名称：

**kd/k usb： targetname =**<em>targetname</em>

## <a name="span-idwhat-if-usbview-shows-a-debug-capable-portspanspan-idwhat_if_usbview_shows_a_debug_capable_portspanwhat-if-usbview-shows-a-debug-capable-port-but-does-not-show-the-port-mapped-to-any-physical-connector"></a><span id="what-if-usbview-shows-a-debug-capable-port"></span><span id="WHAT_IF_USBVIEW_SHOWS_A_DEBUG_CAPABLE_PORT"></span>如果 USBView 显示了支持调试的端口，但没有显示映射到任何物理连接器的端口，会怎么样？

在某些计算机上，USBView 会显示一个支持调试的端口，但不会显示映射到任何物理 USB 连接器的端口。 例如，USBView 可能显示端口2作为 eHCI 控制器的调试端口号。

```console
... USB Enhanced Host Controller ...
...
Debug Port Number:  2
Bus.Device.Function (in decimal): 0.29.0
```

此外，当你使用 USBView 来查看单个端口时，它会列为调试功能。

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

但是，当你将 USB 2.0 设备（如闪存驱动器）插入计算机上的所有 USB 连接器时，USBView 将不会显示你的设备连接到支持调试的端口（在本示例中为端口2）。 USBView 可能会显示映射到 xHCI 控制器的端口的外部连接器，但实际上，外部连接器映射到 eHCI 控制器的支持调试的端口。

![usbview 中 xhci 和 ehci 的屏幕截图](images/usbview01.png)

在这种情况下，你仍可以通过 USB 2.0 电缆建立内核模式调试。 在此处提供的示例中，将 USB 2.0 调试电缆插入到显示为映射到 xHCI 控制器的端口2的连接器中。 然后，将总线参数设置为 eHCI 控制器的总线、设备和功能编号（在本例中为0.29.0）。

`bcdedit /set "{dbgsettings}" busparams 0.29.0`

### <a name="additional-support"></a>其他支持

有关疑难解答提示和其他信息，请参阅[MICROSOFT USB 博客](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/bg-p/MicrosoftUSBBlog)。

## <a name="related-topics"></a>相关主题

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
