---
title: 手动设置通过 USB 3.0 线缆进行的内核模式调试
description: 适用于 Windows 的调试工具支持通过 USB 3.0 电缆进行内核调试。 本主题介绍如何手动设置 USB 3.0 调试。
ms.assetid: 9A9F5DA0-B98A-4C19-A723-67D06B2409B5
ms.date: 01/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8fb12186cdb0d395f75da1e3e399e8372697f874
ms.sourcegitcommit: 0a31c9fa18d5bf02373e7c000abd65e3db78b280
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "76910351"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-manually"></a>手动设置通过 USB 3.0 线缆进行的内核模式调试

适用于 Windows 的调试工具支持通过 USB 3.0 电缆进行内核调试。 本主题介绍如何手动设置 USB 3.0 调试。

运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。

通过 USB 3.0 电缆进行调试需要以下硬件：

- USB 3.0 调试电缆。 这是一条 A 交叉电缆，只包含 USB 3.0 线路，无 Vbus。

- 在主计算机上，xHCI （USB 3.0）主机控制器

- 在目标计算机上，支持调试的 xHCI （USB 3.0）主机控制器

## <a name="span-idsetting_up_the_computer_usb3_manualspanspan-idsetting_up_the_computer_usb3_manualspansetting-up-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>设置目标计算机

1. 在目标计算机上，启动 UsbView 工具。 UsbView 工具包含在 Windows 调试工具中。
2. 在 UsbView 中，找到所有 xHCI 主机控制器。
3. 在 UsbView 中，展开 xHCI 主机控制器的节点。 查找主机控制器上的端口是否支持调试。

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

4. 记下要用于调试的 xHCI 控制器的总线、设备和功能号。 UsbView 显示这些数字。 在以下示例中，总线号为48，设备号为0，并且函数号为0。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5. 确定了支持调试的 xHCI 控制器后，下一步是找到与 xHCI 控制器上的端口关联的物理 USB 连接器。 若要查找物理连接器，请将任何 USB 3.0 设备插入目标计算机上的任何 USB 连接器。 刷新 UsbView 以查看设备所在的位置。 如果 UsbView 显示设备已连接到所选的 xHCI 主机控制器，则已找到可用于 USB 3.0 调试的物理 USB 连接器。

> [!IMPORTANT]
> 使用 bcdedit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。 完成调试并禁用内核调试之后，可以重新启用安全启动。  

6. 在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令：

   - **bcdedit/debug on**
   - **bcdedit/dbgsettings usb targetname：** <em>targetname</em>

   其中*TargetName*是您为目标计算机创建的名称。 请注意， *TargetName*不必是目标计算机的正式名称;它可以是您创建的任何字符串，只要它满足以下限制：

   -  字符串不得以大写或小写的任意组合包含在*TargetName*中任意位置的 "debug"。 例如，如果在 targetname 中的任何位置使用 "调试" 或 "调试"，则调试将不会正常工作。  
   -  字符串中的唯一字符是连字符（-）、下划线（\_）、0到9的数字以及从 A 到 Z 的字母（大写或小写）。
   -  字符串的最大长度为24个字符。

7. 如果目标计算机上有多个 USB 主机控制器，请输入以下命令：

   **bcdedit/set "{dbgsettings}" busparams**

   其中， *b*、 *d*和*f*是要用于调试的 USB 主机控制器的总线、设备和功能号。 总线、设备和功能号必须为十进制格式。

   示例

   **bcdedit/set "{dbgsettings}" busparams 48.0。0**

8. 重新启动目标计算机。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>首次启动调试会话

1. 将通用串行总线（USB）3.0 调试电缆连接到在主机和目标计算机上选择进行调试的 USB 3.0 端口。
2. 确定主机计算机上运行的 Windows 的位数（32位或64位）。
3. 在主计算机上，打开与主计算机上运行的 Windows 的位数相匹配的 WinDbg 版本（以管理员身份）。 例如，如果主计算机运行的是64位版本的 Windows，请以管理员身份打开该版本的 WinDbg 的64位版本。
4. 在 "**文件**" 菜单上，选择 "**内核调试**"。 在 "内核调试" 对话框中，打开 " **USB** " 选项卡。输入在设置目标计算机时创建的目标名称。 单击**确定**。

此时，将在主计算机上安装 USB 调试驱动程序。 这就是将 WinDbg 的位数与 Windows 的位数相匹配的原因。 安装 USB 调试驱动程序之后，可以使用32位或64位版本的 WinDbg 来执行后续的调试会话。

## <a name="span-idstarting_the_debugging_session_usb3_manualspanspan-idstarting_the_debugging_session_usb3_manualspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_manual"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_MANUAL"></span>启动调试会话

### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上，打开 WinDbg。 在 "**文件**" 菜单上，选择 "**内核调试**"。 在 "内核调试" 对话框中，打开 " **USB** " 选项卡。输入在设置目标计算机时创建的目标名称。 单击**确定**。

还可以通过在命令提示符窗口中输入以下命令来启动与 WinDbg 的会话，其中*TargetName*是设置目标计算机时创建的目标名称：

**windbg/k usb： targetname =** <em>targetname</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

在主计算机上，打开命令提示符窗口并输入以下命令，其中*TargetName*是设置目标计算机时创建的目标名称：

**kd/k usb： targetname =** <em>targetname</em>

连接调试器后，请重新启动目标计算机。 重新启动计算机的一种方法是在管理员的命令提示符下使用 `shutdown -r -t 0 ` 命令。

在目标计算机重新启动后，调试器应该会自动连接。

## <a name="span-idtroubleshooting_tips_for_debugging_over_usb_30spanspan-idtroubleshooting_tips_for_debugging_over_usb_30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>通过 USB 3.0 进行调试的疑难解答提示

在某些情况下，电源转换可能会干扰 USB 3.0 上的调试。 如果遇到此问题，请为用于调试的 xHCI 主机控制器（及其根集线器）禁用选择性挂起。

1. 在设备管理器中，导航到 xHCI 主机控制器的节点。 右键单击该节点，然后选择 "**属性**"。 如果有 "**电源管理**" 选项卡，请打开该选项卡，并清除 "**允许计算机关闭此设备以节省电源**" 复选框。

2. 在设备管理器中，导航到 xHCI 主机控制器的根集线器的节点。 右键单击该节点，然后选择 "**属性**"。 如果有 "**电源管理**" 选项卡，请打开该选项卡，并清除 "**允许计算机关闭此设备以节省电源**" 复选框。

完成使用 xHCI 主机控制器进行调试时，为 xHCI 主机控制器启用选择性挂起。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
