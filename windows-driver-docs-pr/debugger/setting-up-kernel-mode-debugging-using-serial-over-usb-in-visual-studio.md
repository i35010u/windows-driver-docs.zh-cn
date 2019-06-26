---
title: 设置内核模式调试中使用序列通过 Visual Studio 中的 USB Shark Cove 开发板
description: 本主题介绍了如何设置 Visual Studio 中的内核模式调试 USB Shark Cove 开发板。
ms.assetid: D909CA2C-3870-4521-8F23-FBF93738F338
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2c131dd133c42c3ba6f234494a3291dc7da56d03
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366375"
---
# <a name="span-iddebuggersettingupkernel-modedebuggingusingserialoverusbinvisualstudiospansetting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_in_visual_studio"></span>设置内核模式调试使用通过 Visual Studio 中的 USB 串行

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

[Shark Cove 开发板](https://go.microsoft.com/fwlink/p?linkid=403168)支持 USB 电缆通过串行调试。

若要使用内核模式调试的 Microsoft Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p?linkid=301383)。

使用 Visual Studio 设置串行调试通过 USB 电缆的替代方法，您还可以手动执行安装程序。 有关详细信息，请参阅[设置内核模式调试使用通过 USB 手动序列](setting-up-kernel-mode-debugging-using-serial-over-usb-manually-.md)。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 在本主题中，Shark Cove 板是目标计算机。

## <a name="span-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>设置主机计算机用于调试 Shark Cove 板


1.  在主计算机上打开设备管理器。 上**视图**菜单中，选择**依类型排序设备**。

2.  Shark Cove 板上找到调试连接器。 这是在下图中所示的 micro USB 连接器。

    ![显示的图片调试 shark cove 板上的连接器](images/sharkscovedebugconnector.png)

3.  使用 USB 2.0 电缆将主计算机连接到 Shark cove 板上的调试连接器。

4.  主机计算机上，在设备管理器中，将获取枚举两个 COM 端口。 选择最低编号的 COM 端口。 上**视图**菜单中，选择**依连接排序设备**。 验证 COM 端口下列出 USB 主控制器之一。

    ![显示在设备管理器的 com 端口的屏幕显示](images/serialoverusb01.png)

    记下的 COM 端口号。 这是显示在 USB 主控制器节点下面的最低 COM 端口号。 例如，在上面的屏幕截图中，在 USB 主控制器的最低 COM 端口号是 COM3。 启动调试会话时，将更高版本需要此 COM 端口号。 如果 COM 端口尚未安装该驱动程序，右键单击 COM 端口节点，然后选择**更新驱动程序**。 然后选择**自动搜索更新的驱动程序软件**。 为此，将需要 internet 连接。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


在这些步骤中，Shark Cove 板是目标计算机。

1.  开始配置主机和目标计算机中所述[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。
2.  主机计算机上，在 Visual Studio 中，当您转至计算机配置对话框中，选择**预配计算机，并选择调试器设置**。
3.  有关**连接类型**，选择**串行**。

    ![屏幕截图显示调试程序的示例具有以下字段的值的设置： 连接类型、 目标名称和总线参数](images/setupserialoverusbvs.png)

    有关**波特率**，输入 115200。 有关**端口**，以前输入记下的 COM 端口的名称，则会在设备管理器 (例如，com3)。 有关**目标端口**，输入 com1。

4.  配置过程需要几分钟时间，并可能会自动重新启动目标计算机一次或两次。 该过程完成后，单击**完成**。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 内核模式调试程序**。
3.  有关**限定符**，选择以前配置的目标计算机的名称。
4.  单击**附加**。

## <a name="span-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>用于 Serial 调试，通过 USB 电缆的故障排除提示


### <a name="span-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>指定正确的 COM 端口在主机和目标

在目标计算机 （Shark Cove 开发板） 中，验证使用 COM1 进行调试。 打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 输出**bcdedit**应显示`debugport 1`。

在主机上验证使用了记下前面在设备管理器中的 COM 端口。

1.  在主计算机上，在 Visual Studio 的**驱动程序**菜单中，选择**测试 &gt; 配置计算机**。
2.  选择测试计算机的名称，然后单击**下一步**。
3.  选择**预配计算机，并选择调试器设置**。 单击“下一步”  。
4.  验证是否为列出正确的 COM 端口号**端口**。

### <a name="span-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>波特率必须是相同的主机和目标上

波特率必须 115200 主机和目标计算机上。

在目标计算机 （Shark Cove 开发板） 中，打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 输出**bcdedit**应显示`baudrate 115200`。

在主机上验证使用 115200 波特率。

1.  在主计算机上，在 Visual Studio 的**驱动程序**菜单中，选择**测试 &gt; 配置计算机**。
2.  选择测试计算机的名称，然后单击**下一步**。
3.  选择**预配计算机，并选择调试器设置**。 单击“下一步”  。
4.  确认**波特率**是 115200。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






