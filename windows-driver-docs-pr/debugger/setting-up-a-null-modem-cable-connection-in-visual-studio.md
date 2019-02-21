---
title: 设置通过在 Visual Studio 中的串行电缆内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行通过调制解调器电缆内核模式调试。
ms.assetid: 9E50AA5F-92A2-4360-BB21-A9D4F3E9CA83
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 368ebc2681fce48dc5ef26a11538515be7fda63f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521516"
---
# <a name="span-iddebuggersettingupanull-modemcableconnectioninvisualstudiospansetting-up-kernel-mode-debugging-over-a-serial-cable-in-visual-studio"></a><span id="debugger.setting_up_a_null-modem_cable_connection_in_visual_studio"></span>设置通过在 Visual Studio 中的串行电缆内核模式调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

可以使用 Microsoft Visual Studio 设置和执行通过调制解调器电缆内核模式调试。 调制解调器电缆有已配置为两个串行端口之间发送数据的串行电缆。 它们在大多数计算机存储均可用。 不要混淆使用标准串行电缆调制解调器电缆。 标准串行电缆不相互连接的串行端口。 了解如何将有线调制解调器电缆，请参阅[调制解调器电缆连接](#null-modem-cable-wiring)。

若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。

使用 Visual Studio 设置串行调试的替代方法，您还可以手动执行安装程序。 有关详细信息，请参阅[设置内核模式调试通过串行电缆手动](setting-up-a-null-modem-cable-connection.md)。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  开始配置主机和目标计算机中所述[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)。
2.  主机计算机上，在 Visual Studio 中，当您转至计算机配置对话框中，选择**预配计算机，并选择调试器设置**。
3.  有关**连接类型**，选择**串行**。

    ![屏幕截图显示调试程序的示例具有以下字段的值的设置： 连接类型、 目标名称和总线参数](images/setupserialvs.png)

    有关**波特率**，接受默认值或输入你想要使用的波特率。 有关**端口**，输入你想要用于调试在主计算机上的 COM 端口的名称。 有关**目标端口**，输入你想要用于调试的目标计算机上的 COM 端口的名称。

4.  配置过程需要几分钟时间，并可能会自动重新启动目标计算机一次或两次。 该过程完成后，单击**完成**。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  连接到已选择在主机和目标计算机上进行调试的 COM 端口的调制解调器电缆。
2.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
3.  有关**传输**，选择**Windows 内核模式调试程序**。
4.  有关**限定符**，选择以前配置的目标计算机的名称。
5.  单击**附加**。

## <a name="span-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>通过串行电缆进行调试的故障排除提示


### <a name="span-idspecifycorrectcomportsandbaudratespanspan-idspecifycorrectcomportsandbaudratespanspan-idspecifycorrectcomportsandbaudratespanspecify-correct-com-ports-and-baud-rate"></a><span id="Specify_correct_COM_ports_and_baud_rate"></span><span id="specify_correct_com_ports_and_baud_rate"></span><span id="SPECIFY_CORRECT_COM_PORTS_AND_BAUD_RATE"></span>指定正确的 COM 端口和波特率

确定将用于在主机和目标计算机上进行调试的 COM 端口号。 例如，假设已在目标计算机上的主机计算机和 COM2 上连接到 COM1 将调制解调器电缆连接。 此外假设您已选择 115200 波特率。

1.  在主计算机上，在 Visual Studio 的**驱动程序**菜单中，选择**测试 &gt; 配置计算机**。
2.  选择测试计算机的名称，然后单击**下一步**。
3.  选择**预配计算机，并选择调试器设置**。 单击“下一步” 。
4.  如果您的主计算机上使用 COM1**端口**，输入 com1。 如果您的在目标计算机上使用 COM2**目标端口**，输入 com2。
5.  如果您要用于 115200，波特率**波特率**，输入 115200。

可以在目标计算机上的仔细检查 COM 端口和波特率速率的设置，通过打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 如果您使用的 COM2 在目标计算机和 115200，输出的波特率**bcdedit**应显示`debugport 2`和`baudrate 115200`。

## <a name="span-idnull-modem-cable-wiringspanspan-idnull-modem-cable-wiringspannull-modem-cable-wiring"></a><span id="null-modem-cable-wiring"></span><span id="NULL-MODEM-CABLE-WIRING"></span>空调制解调器电缆连接


下表显示如何调制解调器电缆连线。

### <a name="span-id9-pinconnectorspanspan-id9-pinconnectorspan9-pin-connector"></a><span id="9-pin_connector"></span><span id="9-PIN_CONNECTOR"></span>9 针连接器

| 连接器 1 | 连接器 2 | 信号        |
|-------------|-------------|----------------|
| 2           | 3           | Tx - Rx        |
| 3           | 2           | Rx - Tx        |
| 7           | 8           | RTS - CTS      |
| 8           | 7           | CTS - RTS      |
| 4           | 1+6         | DTR-(CD + DSR) |
| 1+6         | 4           | (CD + DSR)-DTR |
| 5           | 5           | 信号基础  |

 

### <a name="span-id25-pinconnectorspanspan-id25-pinconnectorspan25-pin-connector"></a><span id="25-pin_connector"></span><span id="25-PIN_CONNECTOR"></span>25 针连接器

| 连接器 1 | 连接器 2 | 信号       |
|-------------|-------------|---------------|
| 2           | 3           | Tx - Rx       |
| 3           | 2           | Rx - Tx       |
| 4           | 5           | RTS - CTS     |
| 5           | 4           | CTS - RTS     |
| 6           | 20          | DSR - DTR     |
| 20          | 6           | DTR - DSR     |
| 7           | 7           | 信号基础 |

 

### <a name="span-idsignalabbreviationsspanspan-idsignalabbreviationsspanspan-idsignalabbreviationsspansignal-abbreviations"></a><span id="Signal_Abbreviations"></span><span id="signal_abbreviations"></span><span id="SIGNAL_ABBREVIATIONS"></span>信号缩写

| 缩写 | 信号              |
|--------------|---------------------|
| Tx           | 将数据传输       |
| Rx           | 接收数据        |
| RTS          | 要发送请求     |
| CTS          | 明文形式发送       |
| DTR          | 数据终端就绪 |
| DSR          | 数据集准备就绪      |
| CD           | 载波检测      |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[设置 Visual Studio 中的内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






