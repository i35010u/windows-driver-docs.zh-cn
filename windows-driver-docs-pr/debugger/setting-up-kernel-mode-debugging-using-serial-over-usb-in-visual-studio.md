---
title: 在 Visual Studio 中使用带 Cove 开发板设置内核模式调试
description: 本主题介绍如何在 Visual Studio 中使用带 Cove 开发板设置内核模式调试 USB。
ms.assetid: D909CA2C-3870-4521-8F23-FBF93738F338
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6f95605abfb3317b33417e7fa77c5e74668a1d94
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528959"
---
# <a name="span-iddebuggersetting_up_kernel-mode_debugging_using_serial_over_usb_in_visual_studiospansetting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_in_visual_studio"></span>在 Visual Studio 中使用串连 over USB 设置内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

[带 Cove 开发板](https://go.microsoft.com/fwlink/p?linkid=403168)支持通过 USB 电缆进行串行调试。

若要将 Microsoft Visual Studio 用于内核模式调试，必须将 Windows 驱动程序工具包（WDK）与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅[Windows 驱动程序工具包（WDK）](https://go.microsoft.com/fwlink/p?linkid=301383)。

运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。 在本主题中，带 Cove 板是目标计算机。

## <a name="span-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>设置用于调试带 Cove 的主机计算机


1.  在主计算机上，打开设备管理器。 在 "**视图**" 菜单上，选择 "**设备类型**"。

2.  在带 Cove 板上，找到调试连接器。 这是下图所示的微 USB 连接器。

    ![显示带 cove 板上的调试连接器的图片](images/sharkscovedebugconnector.png)

3.  使用 USB 2.0 电缆将主计算机连接到带 cove 板上的调试连接器。

4.  在主计算机上的设备管理器中，将枚举两个 COM 端口。 选择编号最低的 COM 端口。 在 "**视图**" 菜单上，选择 "**按连接设备**"。 验证 COM 端口是否列在某个 USB 主机控制器下。

    ![在设备管理器中显示 com 端口的屏幕显示](images/serialoverusb01.png)

    记下 "COM 端口号"。 这是在 "USB 主机控制器" 节点下显示的最低 COM 端口号。 例如，在上面的屏幕截图中，USB 主机控制器下的最低 COM 端口号为 COM3。 稍后启动调试会话时，将需要此 COM 端口号。 如果尚未安装该 COM 端口的驱动程序，请右键单击 "COM 端口" 节点，然后选择 "**更新驱动程序**"。 然后选择 "**自动搜索更新的驱动程序软件**"。 对于此，你将需要 internet 连接。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


在这些步骤中，带 Cove 板是目标计算机。

1.  按照[为驱动程序部署和测试设置计算机（WDK 8.1）](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)中所述，开始配置主机和目标计算机。
2.  在主计算机上，在 Visual Studio 的 "计算机配置" 对话框中，选择 "**设置计算机"，然后选择 "调试器设置**"。
3.  对于 "**连接类型**"，请选择 "**串行**"。

    ![屏幕截图显示了具有以下字段的值的调试器设置示例：连接类型、目标名称和总线参数](images/setupserialoverusbvs.png)

    对于**波特率**，请输入115200。 对于 "**端口**"，请输入前面在设备管理器中记下的 COM 端口的名称（例如 com3）。 对于**目标端口**，请输入 com1。

4.  配置过程需要几分钟的时间，并且可能会自动重启目标计算机一次或两次。 完成此过程后，单击 "**完成**"。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  在主计算机上，在 Visual Studio 的 "**工具**" 菜单中，选择 "**附加到进程**"。
2.  对于 "**传输**"，请选择 " **Windows 内核模式调试程序**"。
3.  对于 "**限定符**"，选择以前配置的目标计算机的名称。
4.  单击 "**附加**"。

## <a name="span-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>通过 USB 电缆进行串行调试的故障排除提示


### <a name="span-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>指定主机和目标上的正确 COM 端口

在目标计算机（带 Cove 板）上，验证是否正在使用 COM1 进行调试。 以管理员身份打开命令提示符窗口，然后输入**bcdedit/dbgsettings**。 **Bcdedit**的输出应显示 `debugport 1`。

在主计算机上，验证你是否正在使用之前在设备管理器中记下的 COM 端口。

1.  在主计算机上，在 Visual Studio 的“驱动程序”菜单中，选择“测试” **“配置计算机”&gt;** 。
2.  选择测试计算机的名称，然后单击 "**下一步**"。
3.  选择 "**设置计算机" 并选择 "调试器设置**"。 单击 **“下一步”** 。
4.  验证是否为 "**端口**" 列出了正确的 COM 端口号。

### <a name="span-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>主机和目标上的波特率必须相同

主机和目标计算机上的波特率必须为115200。

在目标计算机（带 Cove 板）上，以管理员身份打开命令提示符窗口，然后输入**bcdedit/dbgsettings**。 **Bcdedit**的输出应显示 `baudrate 115200`。

在主计算机上，验证是否使用的波特率为115200。

1.  在主计算机上，在 Visual Studio 的“驱动程序”菜单中，选择“测试” **“配置计算机”&gt;** 。
2.  选择测试计算机的名称，然后单击 "**下一步**"。
3.  选择 "**设置计算机" 并选择 "调试器设置**"。 单击 **“下一步”** 。
4.  验证**波特率**是否为115200。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题



