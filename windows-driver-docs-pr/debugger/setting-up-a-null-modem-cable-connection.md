---
title: 手动设置通过串行线缆进行的内核模式调试
description: 调试工具的 Windows 支持通过调制解调器电缆内核调试。
ms.assetid: f7311928-bab1-4692-8dd6-5e464dd7127a
keywords:
- 安装程序，使调试电缆连接
- null 调制解调器电缆
- 调试电缆
- 电缆连接
- 电缆连接，调试 （调制解调器） 电缆）
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d46ae155ae7a2b8ec69b8f79ee0f0232776b074
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562589"
---
# <a name="setting-up-kernel-mode-debugging-over-a-serial-cable-manually"></a>手动设置通过串行线缆进行的内核模式调试


调试工具的 Windows 支持通过调制解调器电缆内核调试。 调制解调器电缆有已配置为两个串行端口之间发送数据的串行电缆。 它们在大多数计算机存储均可用。 不要混淆使用标准串行电缆调制解调器电缆。 标准串行电缆不相互连接的串行端口。 了解如何将有线调制解调器电缆，请参阅[调制解调器电缆连接](#null-modem-cable-wiring)。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>在目标计算机上安装的设置


> [!IMPORTANT]
> 使用 bcdedit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。 您可以重新启用安全启动完成后，调试和您禁用了内核调试。  


1. 目标计算机上打开命令提示符窗口，以管理员身份，并输入以下命令，其中*n*是用于在目标计算机上进行调试的 COM 端口数并*速率*是用于调试的波特率：

   **bcdedit /debug 上**

   **bcdedit /dbgsettings 串行 debugport:**<em>n</em> **baudrate:**<em>速率</em>

   **请注意**波特率必须是主计算机和目标计算机上相同。 建议的速率为 115200。

     

2. 重新启动目标计算机。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


连接到已选择在主机和目标计算机上进行调试的 COM 端口的调制解调器电缆。

### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**COM**选项卡。在中**波特率**框中，输入您选择用于调试的速率。 在中**端口**框中，输入 COM*n*其中*n*是在主计算机上进行调试您的 COM 端口号。 单击 **“确定”**。

您还可以启动会话使用 WinDbg 通过输入以下命令在命令提示符窗口中;*n*是用于在主计算机上进行调试的 COM 端口数并*速率*是用于调试的波特率：

**windbg -k com:port=COM**<em>n</em>**,baud=**<em>rate</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

主计算机上打开命令提示符窗口，并输入以下命令，其中*n*是用于在主计算机上进行调试的 COM 端口数并*速率*波特率用于调试：

**kd -k com:port=COM**<em>n</em>**,baud=**<em>rate</em>

## <a name="span-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>使用环境变量


在主机上，可以使用环境变量指定的 COM 端口和波特率。 然后无需每次启动调试会话指定的端口和波特率速率。 若要使用环境变量指定的 COM 端口和波特率速率，打开命令提示符窗口并输入以下命令，其中*n*是用于在主计算机上进行调试的 COM 端口的数目和*速率*是用于调试的波特率：

- **设置\_NT\_调试\_端口 = COM * * * n*
- **set \_NT\_DEBUG\_BAUD\_RATE=**<em>rate</em>

若要启动调试会话，请打开命令提示符窗口，并输入以下命令之一：

-   **kd**
-   **windbg**

## <a name="span-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>通过串行电缆进行调试的故障排除提示


### <a name="span-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>指定正确的 COM 端口在主机和目标

确定将用于在主机和目标计算机上进行调试的 COM 端口号。 例如，假设已在目标计算机上的主机计算机和 COM2 上连接到 COM1 将调制解调器电缆连接。

在目标计算机上，打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 如果在目标计算机的输出上使用 COM2 **bcdedit**应显示`debugport 2`。

在主机上启动调试器，或当设置环境变量时指定正确的 COM 端口。 如果主机计算机上使用 COM1，使用以下方法之一来指定 COM 端口。

-   在 WinDbg 中，在内核调试对话框中，输入在 COM1**端口**框。
-   **windbg -k com:port=COM1, ...**
-   **kd -k com:port=COM1, ...**
-   **设置\_NT\_调试\_端口 = COM1**

### <a name="span-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>波特率必须是相同的主机和目标上

使用通过串行电缆进行调试的波特率必须设置为在主机和目标计算机上的相同值。 例如，假设您已选择 115200 波特率。

在目标计算机上，打开命令提示符窗口，以管理员身份，并输入**bcdedit /dbgsettings**。 输出**bcdedit**应显示`baudrate 115200`。

在主机上启动调试器，或当设置环境变量时指定正确的波特率。 使用以下方法之一指定 115200 波特率。

-   在 WinDbg 中，在内核调试对话框中，输入在 115200**波特率**框。
-   **windbg -k ..., baud=115200**
-   **kd -k ..., baud=115200**
-   **set \_NT\_DEBUG\_BAUD\_RATE=115200**

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

 

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关完整文档**bcdedit**命令，请参阅驱动程序测试和调试 Windows Driver Kit (WDK) 文档中的启动选项。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






