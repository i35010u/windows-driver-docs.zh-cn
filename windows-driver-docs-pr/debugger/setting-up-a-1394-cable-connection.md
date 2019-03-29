---
title: 手动设置通过 1394 线缆进行的内核模式调试
description: 调试工具的 Windows 支持通过 1394年 (Firewire) 电缆内核调试。 本主题介绍如何设置 1394年调试手动。
ms.assetid: bcfc61a1-0315-451c-a279-f6305995b05f
keywords: 使 1394年电缆连接、 1394年连接，IEEE 1394 电缆、 FireWire 电缆
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6bd273e328d6fd6642f8ca6bf1b281b737383b10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562088"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-manually"></a>手动设置通过 1394 线缆进行的内核模式调试

> [!IMPORTANT]
> 1394 传输协议是可在 Windows 10，版本 1607年及更早版本中使用。 不在更高版本的 Windows 中可用。 应转换到其他传输，如使用以太网 KDNET 项目。 有关该传输的详细信息，请参阅[设置内核模式调试通过网络电缆手动](setting-up-a-network-debugging-connection.md)。
>

调试工具的 Windows 支持通过 1394年 (Firewire) 电缆内核调试。 本主题介绍如何设置 1394年调试手动。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 主机和目标计算机都必须 1394年适配器，并且必须运行 Windows XP 或更高版本。 在主机和目标计算机不需要运行相同版本的 Windows。

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>在目标计算机上安装的设置


1.  连接到已选择在主机和目标计算机上进行调试的 1394 年控制器 1394年电缆。

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

2. 在提升的命令提示符窗口，输入以下命令，其中*n*是您的选择，从 0 至第 62 频道号：

   **bcdedit /debug 上**

   **bcdedit /dbgsettings 1394年通道：**<em>n</em>

3. 如果有多个目标计算机上的 1394年控制器，必须指定总线、 设备和你想要用于调试的 1394年控制器的函数数量。 有关详细信息，请参阅[1394年调试故障排除提示](#troubleshooting-tips-for-debugging-over-a-1394-cable)。

4. 不要重新启动目标计算机尚未。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>启动调试会话的第一次


1.  确定主机计算机上运行的 Windows 的位数 （32 位或 64 位）。
2.  在主计算机上打开的 Windows 主机计算机上运行的位数相匹配 （以管理员身份） 的 WinDbg 的版本。 例如，如果主机计算机运行 Windows 的 64 位版本，请以管理员身份打开 WinDbg 的 64 位版本。
3.  上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**1394年**选项卡。输入你的频道号，然后单击**确定**。

    此时，主机计算机上安装的 1394年调试驱动程序。 这是为什么务必要匹配的位数 WinDbg 到 Windows 的位数。 1394 调试驱动程序安装后，你可以使用 32 位或 64 位版本的 WinDbg 后续调试会话。

4.  重新启动目标计算机。

## <a name="span-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

- 在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**1394年**选项卡。输入你的频道号，然后单击**确定**。

  您还可以启动会话使用 WinDbg 通过输入以下命令在命令提示符窗口中，其中*n*是频道号：

  **windbg /k 1394:channel=**<em>n</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

- 主计算机上打开命令提示符窗口并输入以下命令，其中*n*是频道号：

  **kd /k 1394:channel=**<em>n</em>

## <a name="span-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>使用环境变量


在主机上，可以使用环境变量指定的 1394年通道。 然后无需指定每次您启动调试会话的通道。 若要使用环境变量指定的 1394年通道，打开命令提示符窗口并输入以下命令，其中*n*是频道号：

- **set \_NT\_DEBUG\_BUS=1394**
- **设置\_NT\_调试\_1394年\_通道 =**<em>n</em>

若要启动调试会话，请打开命令提示符窗口并输入以下命令之一：

-   **kd**
-   **windbg**

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关完整文档**bcdedit**命令，并在 boot.ini 文件中，请参阅驱动程序测试和调试 Windows Driver Kit (WDK) 文档中的启动选项。

## <a name="span-idtroubleshooting-tips-for-debugging-over-a-1394-cablespanspan-idtroubleshooting-tips-for-debugging-over-a-1394-cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting-tips-for-debugging-over-a-1394-cable"></span><span id="TROUBLESHOOTING-TIPS-FOR-DEBUGGING-OVER-A-1394-CABLE"></span>通过 1394年电缆进行调试的故障排除技巧


大多数 1394年调试问题引起的主机或目标计算机中使用多个的 1394 年控制器。 不支持在主计算机使用多个的 1394 年控制器。 1394 调试驱动程序，可以在主机上运行，只能与枚举注册表中的第一次 1394年控制器进行通信。 如果您有内置到主板和单独的 1394年卡的 1394年控制器，请删除卡或禁用计算机的 BIOS 设置中的内置控制器。

目标计算机可以具有多个的 1394 年控制器，尽管不建议这样做。 如果目标计算机具有母板上的 1394年控制器，以进行调试，如有可能使用该控制器。 如果没有附加 1394年卡片，应删除卡，并使用板载控制器。 另一种解决方案是计算机的禁用的 BIOS 设置中载入的 1394年控制器。

如果您决定有多个目标计算机上启用的 1394年控制器，必须指定总线参数，以便调试器知道哪一个控制器来声明以进行调试。 若要指定总线参数，在目标计算机上，打开设备管理器并找到你想要用于调试的 1394年控制器。 打开控制器的属性页并记下的总线数、 设备数量和函数数量。 在提升的命令提示符窗口，输入以下命令，其中*b*， *d*，并*f*是十进制格式的总线、 设备和函数编号：

**bcdedit -set "{dbgsettings}" busparams** <em>b</em>**.**<em>d</em>**.**<em>f</em>.

重新启动目标计算机。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






