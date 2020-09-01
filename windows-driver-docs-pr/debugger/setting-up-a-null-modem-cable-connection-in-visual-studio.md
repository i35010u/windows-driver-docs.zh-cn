---
title: 在 Visual Studio 中设置通过串行线缆进行的内核模式调试
description: 可以使用 Microsoft Visual Studio 通过空调缆线设置和执行内核模式调试。
ms.assetid: 9E50AA5F-92A2-4360-BB21-A9D4F3E9CA83
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0f8dd367cef544c92a8daaf90ab719075516107d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210841"
---
# <a name="span-iddebuggersetting_up_a_null-modem_cable_connection_in_visual_studiospansetting-up-kernel-mode-debugging-over-a-serial-cable-in-visual-studio"></a><span id="debugger.setting_up_a_null-modem_cable_connection_in_visual_studio"></span>在 Visual Studio 中设置通过串行线缆进行的内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

可以使用 Microsoft Visual Studio 通过空调缆线设置和执行内核模式调试。 空调缆线是已配置为在两个串行端口之间发送数据的串行电缆。 它们可在大多数计算机存储中使用。 不要将空调缆线与标准串行电缆混淆。 标准串行电缆不会将串行端口彼此连接在一起。 有关空调制解调器电缆如何连接的信息，请参阅 [空调制解调器电缆布线](#null-modem-cable-wiring)。

若要将 Visual Studio 用于内核模式调试，你必须将 Windows 驱动程序工具包 (WDK) 与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅 [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

作为使用 Visual Studio 设置串行调试的替代方法，你可以手动执行设置。 有关详细信息，请参阅 [通过串行电缆手动设置内核模式调试](setting-up-a-null-modem-cable-connection.md)。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  按照为 [驱动程序部署设置计算机和测试 (WDK 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)中所述，开始配置主机和目标计算机。
2.  在主计算机上，在 Visual Studio 的 "计算机配置" 对话框中，选择 " **设置计算机"，然后选择 "调试器设置**"。
3.  对于 " **连接类型**"，请选择 " **串行**"。

    ![屏幕截图显示了具有以下字段的值的调试器设置示例：连接类型、目标名称和总线参数](images/setupserialvs.png)

    对于 **波特率**，接受默认值或输入要使用的波特率。 对于 " **端口**"，请输入要用于在主计算机上进行调试的 COM 端口的名称。 对于 " **目标端口**"，请输入要用于在目标计算机上进行调试的 COM 端口的名称。

4.  配置过程需要几分钟的时间，并且可能会自动重启目标计算机一次或两次。 完成此过程后，单击 " **完成**"。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  将空调制解调器电缆连接到在主机和目标计算机上选择进行调试的 COM 端口。
2.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
3.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
4.  对于 " **限定符**"，选择以前配置的目标计算机的名称。
5.  单击 **“附加”** 。

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>通过串行电缆进行调试的故障排除提示


### <a name="span-idspecify_correct_com_ports_and_baud_ratespanspan-idspecify_correct_com_ports_and_baud_ratespanspan-idspecify_correct_com_ports_and_baud_ratespanspecify-correct-com-ports-and-baud-rate"></a><span id="Specify_correct_COM_ports_and_baud_rate"></span><span id="specify_correct_com_ports_and_baud_rate"></span><span id="SPECIFY_CORRECT_COM_PORTS_AND_BAUD_RATE"></span>指定正确的 COM 端口和波特率

确定要用于在主机和目标计算机上进行调试的 COM 端口的数量。 例如，假设您在主计算机上有一个连接到 COM1 的、在目标计算机上连接到 COM1 的空调制解调器电缆。 同时假设您选择了波特率为115200。

1.  在主计算机上，在 Visual Studio 的“驱动程序”  菜单中，选择“测试”&gt;“配置计算机”  。
2.  选择测试计算机的名称，然后单击 " **下一步**"。
3.  选择 " **设置计算机" 并选择 "调试器设置**"。 单击“配置目录分区”  。
4.  如果在主计算机上使用 COM1，请在 " **端口**" 中输入 COM1。 如果要在目标计算机上使用 COM2，请在 " **目标端口**" 中输入 COM2。
5.  如果已选择使用波特率115200，对于 **波特率**，请输入115200。

通过以管理员身份打开命令提示符窗口，然后输入 **bcdedit/dbgsettings**，可以在目标计算机上仔细检查 COM 端口和波特率设置。 如果在目标计算机上使用 COM2 并且波特率为115200，则 **bcdedit** 的输出应显示 `debugport 2` 和 `baudrate 115200` 。

## <a name="span-idnull-modem-cable-wiringspanspan-idnull-modem-cable-wiringspannull-modem-cable-wiring"></a><span id="null-modem-cable-wiring"></span><span id="NULL-MODEM-CABLE-WIRING"></span>空调制解调器电缆布线


下表显示空调制解调器电缆如何连接。

### <a name="span-id9-pin_connectorspanspan-id9-pin_connectorspan9-pin-connector"></a><span id="9-pin_connector"></span><span id="9-PIN_CONNECTOR"></span>9针连接器

| 连接器1 | 连接器2 | 引发        |
|-------------|-------------|----------------|
| 2           | 3           | Tx-Rx        |
| 3           | 2           | Rx-Tx        |
| 7           | 8           | RTS-CTS      |
| 8           | 7           | CTS-RTS      |
| 4           | 1 + 6         | DTR- (CD + DSR)  |
| 1 + 6         | 4           |  (CD + DSR) -DTR |
| 5           | 5           | 信号接地  |

 

### <a name="span-id25-pin_connectorspanspan-id25-pin_connectorspan25-pin-connector"></a><span id="25-pin_connector"></span><span id="25-PIN_CONNECTOR"></span>25针连接器

| 连接器1 | 连接器2 | 引发       |
|-------------|-------------|---------------|
| 2           | 3           | Tx-Rx       |
| 3           | 2           | Rx-Tx       |
| 4           | 5           | RTS-CTS     |
| 5           | 4           | CTS-RTS     |
| 6           | 20          | DSR-DTR     |
| 20          | 6           | DTR-DSR     |
| 7           | 7           | 信号接地 |

 

### <a name="span-idsignal_abbreviationsspanspan-idsignal_abbreviationsspanspan-idsignal_abbreviationsspansignal-abbreviations"></a><span id="Signal_Abbreviations"></span><span id="signal_abbreviations"></span><span id="SIGNAL_ABBREVIATIONS"></span>信号缩写

| 缩写 | Signal              |
|--------------|---------------------|
| Tx           | 传输数据       |
| Rx           | 接收数据        |
| RTS          | 请求发送     |
| 限          | 清除以发送       |
| DTR          | 数据终端就绪 |
| 看到          | 数据集就绪      |
| CD           | 载体检测      |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

