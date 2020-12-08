---
title: 手动设置通过 1394 线缆进行的内核模式调试
description: 适用于 Windows 的调试工具支持通过 1394 (火线) 电缆进行内核调试。 本主题介绍如何手动设置1394调试。
keywords: 建立1394电缆连接、1394连接、IEEE 1394 电缆、火线电缆
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 480c5bd4347f928e6f0334046f61d6219d32c6b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803619"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-manually"></a>手动设置通过 1394 线缆进行的内核模式调试

> [!IMPORTANT]
> 1394 传输可用于 Windows 10 版本 1607 及更低版本。 它在 Windows 的更高版本中不可用。 应将项目转换为其他传输，例如使用以太网的 KDNET。 有关该传输的详细信息，请参阅[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。
>

适用于 Windows 的调试工具支持通过 1394 (火线) 电缆进行内核调试。 本主题介绍如何手动设置1394调试。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。 主机和目标计算机必须都具有1394适配器，并且必须运行 Windows XP 或更高版本。 主机和目标计算机不需要运行相同版本的 Windows。

## <a name="span-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>设置目标计算机

1. 将1394电缆连接到在主机和目标计算机上选择进行调试的1394控制器。

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

2. 在提升的命令提示符窗口中，输入以下命令，其中 *n* 是你选择的通道号，从0到62：

   **bcdedit/debug on**

   **bcdedit/dbgsettings 1394 通道：**<em>n</em>

3. 你必须指定要用于调试的1394控制器的总线、设备和功能号。 有关详细信息，请参阅 [1394 调试的故障排除提示](#troubleshooting-tips-for-debugging-over-a-1394-cable)。

4. 不要重新启动目标计算机。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>首次启动调试会话

1.  确定主机计算机上运行的 Windows 的位数 (32 位或64位) 。
2.  在主计算机上，以与主计算机上运行的 Windows 的位数匹配的 "管理员) 的形式打开某一版本的 WinDbg (。 例如，如果主计算机运行的是64位版本的 Windows，请以管理员身份打开该版本的 WinDbg 的64位版本。
3.  在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **1394** " 选项卡。输入频道号，然后单击 **"确定"**。

    此时，将在主计算机上安装1394调试驱动程序。 这就是将 WinDbg 的位数与 Windows 的位数相匹配的原因。 安装了1394调试驱动程序之后，可以使用 WinDbg 的32位版本或64位版本进行后续调试会话。

4.  重新启动目标计算机。

## <a name="span-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>启动调试会话

### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

- 在主计算机上，打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **1394** " 选项卡。输入频道号，然后单击 **"确定"**。

  还可以通过在命令提示符窗口中输入以下命令（其中 *n* 是你的频道号）来启动与 WinDbg 的会话：

  **windbg/k 1394：通道 =**<em>n</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

- 在主计算机上，打开命令提示符窗口并输入以下命令，其中 *n* 是你的频道号：

  **kd/k 1394：通道 =**<em>n</em>

## <a name="span-idusing_environment_variablesspanspan-idusing_environment_variablesspanspan-idusing_environment_variablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>使用环境变量


在主计算机上，可以使用环境变量来指定1394通道。 这样就不必在每次启动调试会话时都指定通道。 若要使用环境变量来指定1394通道，请打开命令提示符窗口并输入以下命令，其中 *n* 是你的通道号：

- **设置 \_ NT \_ 调试 \_ 总线 = 1394**
- **设置 \_NT \_ DEBUG \_ 1394 \_ 通道 =**<em>n</em>

若要启动调试会话，请打开命令提示符窗口并输入以下命令之一：

-   **kd**
-   **windbg**

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关 **bcdedit** 命令和 boot.ini 文件的完整文档，请参阅 Windows 驱动程序工具包中的驱动程序测试和调试的启动选项 (WDK) 文档。

## <a name="span-idtroubleshooting-tips-for-debugging-over-a-1394-cablespanspan-idtroubleshooting-tips-for-debugging-over-a-1394-cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting-tips-for-debugging-over-a-1394-cable"></span><span id="TROUBLESHOOTING-TIPS-FOR-DEBUGGING-OVER-A-1394-CABLE"></span>通过1394电缆进行调试的故障排除提示


大多数1394调试问题都是在主机或目标计算机中使用多个1394控制器导致的。 不支持在主机计算机中使用多个1394控制器。 在主机上运行的1394调试驱动程序只能与注册表中枚举的第一个1394控制器进行通信。 如果主板内置了1394控制器和一个单独的1394卡，请取出该卡或在计算机的 BIOS 设置中禁用内置控制器。

目标计算机可以有多个1394控制器，尽管不建议这样做。 如果目标计算机在主板上有1394控制器，请尽可能使用该控制器进行调试。 如果有其他1394卡，则应拔下卡并使用板载控制器。 另一种解决方案是在计算机的 BIOS 设置中禁用板载1394控制器。

如果你决定在目标计算机上启用多个1394控制器，则必须指定总线参数，以便调试器知道要对哪个控制器进行调试。 若要指定总线参数，请在目标计算机上打开设备管理器，并找到要用于调试的1394控制器。 打开控制器的 "属性" 页，记下 "总线号码"、"设备编号" 和 "功能编号"。 在提升的命令提示符窗口中，输入以下命令，其中 *b*、 *d* 和 *f* 是以十进制格式表示的总线、设备和函数编号：

**bcdedit-设置 "{dbgsettings}" busparams** <em>b</em>**。**<em>d.</em>**.**<em>f.</em>。

重新启动目标计算机。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)
