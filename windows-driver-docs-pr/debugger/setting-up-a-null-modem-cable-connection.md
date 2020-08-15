---
title: 手动设置通过串行线缆进行的内核模式调试
description: 适用于 Windows 的调试工具支持通过空调缆线进行内核调试。
ms.assetid: f7311928-bab1-4692-8dd6-5e464dd7127a
keywords:
- 设置，建立调试电缆连接
- 空调制解调器电缆
- 调试电缆
- 电缆连接
- '电缆连接、调试 (空调) 电缆) '
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2ce892c5331aa9131b6da55b296d18fda7a61e8f
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253083"
---
# <a name="setting-up-kernel-mode-debugging-over-a-serial-cable-manually"></a>手动设置通过串行线缆进行的内核模式调试

适用于 Windows 的调试工具支持通过空调缆线进行内核调试。 空调缆线是已配置为在两个串行端口之间发送数据的串行电缆。 不要将空调缆线与标准串行电缆混淆。 标准串行电缆不会将串行端口彼此连接在一起。 有关空调制解调器电缆如何连接的信息，请参阅 [空调制解调器电缆布线](#null-modem-cable-wiring)。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。

## <a name="span-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>设置目标计算机

> [!IMPORTANT]
> 使用 bcdedit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 完成调试并禁用内核调试之后，可以重新启用安全启动。  

1. 在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令，其中 *n* 是目标计算机上用于调试的 COM 端口号， *rate* 是用于调试的波特速率：

   **bcdedit/debug on**

   **bcdedit/dbgsettings serial debugport：**<em>n</em> **波特率：**<em>rate</em>

   **注意**  在主计算机和目标计算机上，波特率必须相同。 建议的速率为115200。

2. 重新启动目标计算机。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话

将空调制解调器电缆连接到在主机和目标计算机上选择进行调试的 COM 端口。

### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上，打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **COM** " 选项卡。在 " **波特率** " 框中，输入为调试选择的费率。 在 " **端口** " 框中，输入 com*n* ，其中 *n* 是你在主机计算机上选择进行调试的 com 端口号。 选择“确定”。

还可以通过在命令提示符窗口中输入以下命令来启动与 WinDbg 的会话： *n* 是在主计算机上用于调试的 COM 端口号， *rate* 是用于调试的波特速率：

**windbg-k com： port = com**<em>n</em>**，波特 =**<em>rate</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

在主计算机上，打开命令提示符窗口，然后输入以下命令，其中 *n* 是在主计算机上用于调试的 COM 端口号， *rate* 是用于调试的波特速率：

**kd-k com： port = com**<em>n</em>**，波特 =**<em>rate</em>

## <a name="span-idusing_environment_variablesspanspan-idusing_environment_variablesspanspan-idusing_environment_variablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>使用环境变量


在主计算机上，可以使用环境变量指定 COM 端口和波特率。 这样就不必在每次启动调试会话时指定端口和波特率。 若要使用环境变量来指定 COM 端口和波特率，请打开命令提示符窗口并输入以下命令，其中 *n* 是在主计算机上用于调试的 COM 端口的编号， *rate* 是用于调试的波特率：

- **设置 \_ NT \_ 调试 \_ 端口 = COM * * * n*
- **设置 \_NT \_ 调试 \_ 波特率 \_ =**<em>速率</em>

若要启动调试会话，请打开命令提示符窗口，然后输入以下命令之一：

-   **kd**
-   **windbg**

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>通过串行电缆进行调试的故障排除提示


### <a name="span-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>指定主机和目标上的正确 COM 端口

确定要用于在主机和目标计算机上进行调试的 COM 端口的数量。 例如，假设您在主计算机上有一个连接到 COM1 的、在目标计算机上连接到 COM1 的空调制解调器电缆。

在目标计算机上，以管理员身份打开命令提示符窗口，然后输入 **bcdedit/dbgsettings**。 如果在目标计算机上使用 COM2，则 **bcdedit** 的输出应显示 `debugport 2` 。

在主计算机上，启动调试器或设置环境变量时，请指定正确的 COM 端口。 如果在主计算机上使用 COM1，请使用下列方法之一指定 COM 端口。

-   在 WinDbg 的 "内核调试" 对话框中，在 " **端口** " 框中输入 COM1。
-   **windbg-k com： port = COM1，.。。**
-   **kd-k com： port = COM1，.。。**
-   **设置 \_ NT \_ 调试 \_ 端口 = COM1**

### <a name="span-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>主机和目标上的波特率必须相同

用于通过串行电缆进行调试的波特率必须设置为主机和目标计算机上的相同值。 例如，假设您选择了波特率为115200。

在目标计算机上，以管理员身份打开命令提示符窗口，然后输入 **bcdedit/dbgsettings**。 **Bcdedit**的输出应显示 `baudrate 115200` 。

在主计算机上，当您启动调试器或设置环境变量时，请指定正确的波特率。 使用以下方法之一来指定波特率为115200。

-   在 WinDbg 的 "内核调试" 对话框中，在 " **波特率** " 框中输入115200。
-   **windbg-k ...，波特 = 115200**
-   **kd-k ...，波特 = 115200**
-   **设置 \_ NT \_ 调试 \_ 波特率 \_ = 115200**

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

 

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 **bcdedit** 命令的完整文档，请参阅 [bcdedit Options Reference](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
