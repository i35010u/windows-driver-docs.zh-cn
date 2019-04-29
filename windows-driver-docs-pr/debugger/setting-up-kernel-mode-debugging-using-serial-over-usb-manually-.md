---
title: 设置内核模式调试使用通过 USB 手动为 Shark cove 开发板的序列
description: 本主题介绍了如何手动为 Shark cove 开发板内核模式调试的设置。
ms.assetid: E6157263-74E8-4704-9668-B845043737A7
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 72c31d23bcd9ffa5d91eabb75a2d61a179b8db14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368135"
---
# <a name="span-iddebuggersettingupkernel-modedebuggingusingserialoverusbmanuallyspansetting-up-kernel-mode-debugging-using-serial-over-usb-manually"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_manually_"></span>设置内核模式调试使用通过 USB 手动序列


[Shark Cove 开发板](https://go.microsoft.com/fwlink/p?linkid=403168)支持 USB 电缆通过串行调试。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 在本主题中，Shark Cove 板是目标计算机。

## <a name="span-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>设置主机计算机用于调试 Shark Cove 板


1.  在主计算机上打开设备管理器。 上**视图**菜单中，选择**依类型排序设备**。

2.  Shark Cove 板上找到调试连接器。 这是在下图中所示的 micro USB 连接器。

    ![显示的图片调试 shark cove 板上的连接器](images/sharkscovedebugconnector.png)

3.  使用 USB 2.0 电缆将主计算机连接到 Shark cove 板上的调试连接器。

4.  主机计算机上，在设备管理器中，将获取枚举两个 COM 端口。 选择最低编号的 COM 端口。 上**视图**菜单中，选择**依连接排序设备**。 验证 COM 端口下列出 USB 主控制器之一。

    ![显示在设备管理器的 com 端口的屏幕显示](images/serialoverusb01.png)

    记下的 COM 端口号。 这是显示在 USB 主控制器节点下面的最低 COM 端口号。 例如，在上面的屏幕截图中，在 USB 主控制器的最低 COM 端口号是 COM3。 启动调试会话时，将更高版本需要此 COM 端口号。 如果 COM 端口尚未安装该驱动程序，右键单击 COM 端口节点，然后选择**更新驱动程序**。 然后选择**自动搜索更新的驱动程序软件**。 为此，将需要 internet 连接。

## <a name="span-idsettingupthesharkscoveboardasthetargetcomputerspanspan-idsettingupthesharkscoveboardasthetargetcomputerspanspan-idsettingupthesharkscoveboardasthetargetcomputerspansetting-up-the-sharks-cove-board-as-the-target-computer"></a><span id="Setting_Up_the_Sharks_Cove_Board_as_the_Target_Computer"></span><span id="setting_up_the_sharks_cove_board_as_the_target_computer"></span><span id="SETTING_UP_THE_SHARKS_COVE_BOARD_AS_THE_TARGET_COMPUTER"></span>作为目标计算机设置 Shark Cove 板

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

1.  在目标计算机 （Shark Cove 开发板） 中，打开命令提示符窗口，以管理员身份，并输入以下命令：

    **bcdedit /debug 上**

    **bcdedit /dbgsettings serial debugport:1 baudrate:115200**

2.  重新启动目标计算机。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**COM**选项卡。在中**波特率**框中，输入 115200。 在中**端口**框中，输入 COM*n*其中*n*是前面所述的 COM 端口号。 单击 **“确定”**。

您还可以启动会话使用 WinDbg 通过输入以下命令在命令提示符窗口中;*n*是主计算机所述的 COM 端口数：

**windbg -k com:port=COM**<em>n</em>**,baud=115200**

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

主计算机上打开命令提示符窗口，并输入以下命令，其中*n*是前面所述的 COM 端口号：

**kd -k com:port=COM**<em>n</em>**,baud=115200**

## <a name="span-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>使用环境变量


在主机上，可以使用环境变量指定的 COM 端口和波特率。 然后无需每次启动调试会话指定的端口和波特率速率。 若要使用环境变量指定的 COM 端口和波特率速率，打开命令提示符窗口并输入以下命令，其中*n*是前面所述的数字的 COM 端口号：

-   **设置\_NT\_调试\_端口 = COM * * * n*
-   **set \_NT\_DEBUG\_BAUD\_RATE=115200**

若要启动调试会话，请打开命令提示符窗口，并输入以下命令之一：

-   **kd**
-   **windbg**

## <a name="span-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>用于 Serial 调试，通过 USB 电缆的故障排除提示


### <a name="span-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>指定正确的 COM 端口在主机和目标

在目标计算机 （Shark Cove 开发板） 中，验证使用 COM1 进行调试。 打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 输出**bcdedit**应显示`debugport 1`。

在主机上启动调试器，或当设置环境变量时指定正确的 COM 端口。 这是已枚举 USB 主控制器在设备管理器下带编号最低的 COM 端口。 例如，如果 COM3 是所需的端口，使用以下方法之一来指定 COM 端口。

-   在 WinDbg 中，在内核调试对话框中，输入在 COM3**端口**框。
-   **windbg -k com:port=COM3, ...**
-   **kd -k com:port=COM3, ...**
-   **设置\_NT\_调试\_端口 = COM3**

### <a name="span-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>波特率必须是相同的主机和目标上

波特率必须 115200 主机和目标计算机上。

在目标计算机 （Shark Cove 开发板） 中，打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 输出**bcdedit**应显示`baudrate 115200`。

在主机上启动调试器，或当设置环境变量时指定正确的波特率。 使用以下方法之一指定 115200 波特率。

-   在 WinDbg 中，在内核调试对话框中，输入在 115200**波特率**框。
-   **windbg -k ..., baud=115200**
-   **kd -k ..., baud=115200**
-   **set \_NT\_DEBUG\_BAUD\_RATE=115200**

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关完整文档**bcdedit**命令，请参阅驱动程序测试和调试 Windows Driver Kit (WDK) 文档中的启动选项。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






