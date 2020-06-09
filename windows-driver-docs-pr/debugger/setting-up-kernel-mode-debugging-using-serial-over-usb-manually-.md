---
title: 为带 cove 开发板手动使用串行 over USB 设置内核模式调试
description: 本主题介绍如何为带 cove 开发面板手动设置内核模式调试。
ms.assetid: E6157263-74E8-4704-9668-B845043737A7
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 43bd8536125ee197b4373a4c53b8d72ac5cccf2e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534758"
---
# <a name="span-iddebuggersetting_up_kernel-mode_debugging_using_serial_over_usb_manually_spansetting-up-kernel-mode-debugging-using-serial-over-usb-manually"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_manually_"></span>手动使用串行 over USB 设置内核模式调试


[带 Cove 硬件开发委员会](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board)支持通过 USB 电缆进行串行调试。

运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。 在本主题中，带 Cove 板是目标计算机。

## <a name="span-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>设置用于调试带 Cove 的主机计算机


1.  在主计算机上，打开设备管理器。 在 "**视图**" 菜单上，选择 "**设备类型**"。

2.  在带 Cove 板上，找到调试连接器。 这是下图所示的微 USB 连接器。

    ![显示带 cove 板上的调试连接器的图片](images/sharkscovedebugconnector.png)

3.  使用 USB 2.0 电缆将主计算机连接到带 cove 板上的调试连接器。

4.  在主计算机上的设备管理器中，将枚举两个 COM 端口。 选择编号最低的 COM 端口。 在 "**视图**" 菜单上，选择 "**按连接设备**"。 验证 COM 端口是否列在某个 USB 主机控制器下。

    ![在设备管理器中显示 com 端口的屏幕显示](images/serialoverusb01.png)

    记下 "COM 端口号"。 这是在 "USB 主机控制器" 节点下显示的最低 COM 端口号。 例如，在上面的屏幕截图中，USB 主机控制器下的最低 COM 端口号为 COM3。 稍后启动调试会话时，将需要此 COM 端口号。 如果尚未安装该 COM 端口的驱动程序，请右键单击 "COM 端口" 节点，然后选择 "**更新驱动程序**"。 然后选择 "**自动搜索更新的驱动程序软件**"。 对于此，你将需要 internet 连接。

## <a name="span-idsetting_up_the_sharks_cove_board_as_the_target_computerspanspan-idsetting_up_the_sharks_cove_board_as_the_target_computerspanspan-idsetting_up_the_sharks_cove_board_as_the_target_computerspansetting-up-the-sharks-cove-board-as-the-target-computer"></a><span id="Setting_Up_the_Sharks_Cove_Board_as_the_Target_Computer"></span><span id="setting_up_the_sharks_cove_board_as_the_target_computer"></span><span id="SETTING_UP_THE_SHARKS_COVE_BOARD_AS_THE_TARGET_COMPUTER"></span>将带 Cove 板设置为目标计算机

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

1.  在目标计算机（带 Cove 板）上，以管理员身份打开命令提示符窗口，然后输入以下命令：

    **bcdedit/debug on**

    **bcdedit/dbgsettings 串行 debugport：1波特率：115200**

2.  重新启动目标计算机。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上，打开 WinDbg。 在 "**文件**" 菜单上，选择 "**内核调试**"。 在 "内核调试" 对话框中，打开 " **COM** " 选项卡。在 "**波特率**" 框中，输入115200。 在 "**端口**" 框中，输入 com*n* ，其中*n*是之前记下的 com 端口号。 单击 **“确定”** 。

还可以通过在命令提示符窗口中输入以下命令来启动与 WinDbg 的会话：*n*是你在主机计算机上记下的 COM 端口的数目：

**windbg-k com： port = com**<em>n</em>**，波特 = 115200**

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

在主计算机上，打开命令提示符窗口，然后输入以下命令，其中*n*是之前记下的 COM 端口号：

**kd-k com： port = com**<em>n</em>**，波特 = 115200**

## <a name="span-idusing_environment_variablesspanspan-idusing_environment_variablesspanspan-idusing_environment_variablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>使用环境变量


在主计算机上，可以使用环境变量指定 COM 端口和波特率。 这样就不必在每次启动调试会话时指定端口和波特率。 若要使用环境变量来指定 COM 端口和波特率，请打开命令提示符窗口并输入以下命令，其中*n*是之前记下的 COM 端口号：

-   **设置 \_ NT \_ 调试 \_ 端口 = COM * * * n*
-   **设置 \_ NT \_ 调试 \_ 波特率 \_ = 115200**

若要启动调试会话，请打开命令提示符窗口，然后输入以下命令之一：

-   **kd**
-   **windbg**

## <a name="span-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>通过 USB 电缆进行串行调试的故障排除提示


### <a name="span-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>指定主机和目标上的正确 COM 端口

在目标计算机（带 Cove 板）上，验证是否正在使用 COM1 进行调试。 以管理员身份打开命令提示符窗口，然后输入**bcdedit/dbgsettings**。 **Bcdedit**的输出应显示 `debugport 1` 。

在主计算机上，启动调试器或设置环境变量时，请指定正确的 COM 端口。 这是在设备管理器中的 USB 主机控制器下枚举的编号最低的 COM 端口。 例如，如果 COM3 为所需的端口，请使用以下方法之一指定 COM 端口。

-   在 WinDbg 的 "内核调试" 对话框中，在 "**端口**" 框中输入 COM3。
-   **windbg-k com： port = COM3，.。。**
-   **kd-k com： port = COM3，.。。**
-   **设置 \_ NT \_ 调试 \_ 端口 = COM3**

### <a name="span-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>主机和目标上的波特率必须相同

主机和目标计算机上的波特率必须为115200。

在目标计算机（带 Cove 板）上，以管理员身份打开命令提示符窗口，然后输入**bcdedit/dbgsettings**。 **Bcdedit**的输出应显示 `baudrate 115200` 。

在主计算机上，当您启动调试器或设置环境变量时，请指定正确的波特率。 使用以下方法之一来指定波特率为115200。

-   在 WinDbg 的 "内核调试" 对话框中，在 "**波特率**" 框中输入115200。
-   **windbg-k ...，波特 = 115200**
-   **kd-k ...，波特 = 115200**
-   **设置 \_ NT \_ 调试 \_ 波特率 \_ = 115200**

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关**bcdedit**命令的完整文档，请参阅 Windows 驱动程序工具包（WDK）文档中的驱动程序测试和调试的启动选项。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






