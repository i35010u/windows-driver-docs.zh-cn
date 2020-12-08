---
title: 使用 KD 进行实时内核模式调试
description: 使用 KD 进行实时内核模式调试
ms.date: 06/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1d35c54391b40d50ed6c7925ba267d074da289b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803621"
---
# <a name="span-iddebuggerperforming_kernel-mode_debugging_using_kdspanlive-kernel-mode-debugging-using-kd"></a><span id="debugger.performing_kernel-mode_debugging_using_kd"></span>使用 KD 进行实时内核模式调试


在命令提示符窗口中，您可以在启动 KD 时启动实时内核模式调试会话。 输入以下命令之一。

kd \[ -y *SymbolPath* \] -k net： port =*PortNumber*，key =*key* \[ ，target =*TargetIPAddress* | *TargetHostName*\] 

kd \[ -y *SymbolPath* \] -k 1394：通道 =*1394Channel* \[ ，符号 =*1394Protocol*\]

kd \[ -y *SymbolPath* \] -k Usb： targetname =*USBString*

kd \[ -y *SymbolPath* \] -k Com： port =*ComPort*，波特 =*波特率*

kd \[ -y *SymbolPath* \] -k com： pipe，port = \\ \\ *VMHost* \\ pipe \\ *PipeName* \[ ，重置 = 0 \] \[ ，重新连接\]

kd \[ -y *SymbolPath* \] -k com：*调制解调器*

kd \[ -y *SymbolPath* \] -kl

kd \[ -y *SymbolPath* \] -k

有关详细信息，请参阅 [**KD Command-Line 选项**](kd-command-line-options.md)。

### <a name="span-idenvironment_variablesspanspan-idenvironment_variablesspanspan-idenvironment_variablesspanenvironment-variables"></a><span id="Environment_Variables"></span><span id="environment_variables"></span><span id="ENVIRONMENT_VARIABLES"></span>环境变量

若要通过串行 (COM 端口) 或1394连接进行调试，可以使用环境变量来指定连接设置。

使用以下变量指定串行连接。

设置 \_ NT \_ 调试 \_ 端口 = *ComPort*

设置 \_ NT \_ 调试 \_ 波特率 \_ = *波特率*

使用以下变量指定1394连接。

设置 \_ NT \_ 调试 \_ 总线 = 1394

设置 \_ NT \_ DEBUG \_ 1394 \_ 通道 = *1394Channel* 

设置 \_ NT \_ DEBUG \_ 1394 \_ 符号符号 = *1394Protocol*

有关详细信息，请参阅 [内核模式环境变量](kernel-mode-environment-variables.md)。

### <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数

<span id="_______SymbolPath______"></span><span id="_______symbolpath______"></span><span id="_______SYMBOLPATH______"></span>*SymbolPath*   
符号文件所在的目录的列表。 列表中的目录用分号分隔。 有关详细信息，请参阅 [符号路径](symbol-path.md)。

<span id="_______PortNumber______"></span><span id="_______portnumber______"></span><span id="_______PORTNUMBER______"></span>*PortNumber*   
用于网络调试的端口号。 你可以选择从49152到65535的任何数字。 有关详细信息，请参阅 [手动设置网络连接](setting-up-a-network-debugging-connection.md)。

<span id="_______Key______"></span><span id="_______key______"></span><span id="_______KEY______"></span>*键*   
用于网络调试的加密密钥。 建议使用自动生成的密钥，该密钥由 bcdedit 在配置目标计算机时提供。 有关详细信息，请参阅 [手动设置网络连接](setting-up-a-network-debugging-connection.md)。


<span id="_______TargetIp______"></span><span id="_______targetip______"></span><span id="_______TARGETIP______"></span>*TargetIPAddress*   
目标计算机的 IPv4 地址。 

指定 target = IP 地址时，这会使调试器启动到指定目标计算机的连接，方法是向目标发送一个特殊的数据包，这将导致它尝试与该调试器进行连接。 调试器将每半秒重复发送到目标，以尝试连接。 如果连接成功，则目标将删除任何现有连接，并且仅与调试器的此实例通信。 这使你可以从现有的调试连接中控制调试会话。 

当目标配置有主机 IP 地址，并且在具有配置的主机 IP 地址的计算机上运行调试器时，无需指定 target = IP address 参数。 当目标配置有主机 IP 地址时，它会每隔三秒向主机发送一次提供数据包。  当未指定 target = IP 地址时，产品/服务数据包允许调试器连接到主机。

有关在目标上配置主机 IP 地址的详细信息，请参阅 [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md) 和 [手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)。


<span id="_______TargetName______"></span><span id="_______targetname______"></span><span id="_______TARGETNAME______"></span>*TargetMachineName*   
目标 PC 的计算机名称。 若要使用计算机名称，网络上的 DNS 系统必须具有与目标 PC 的 IP 地址相关联的计算机名称。
 
<span id="_______1394Channel______"></span><span id="_______1394channel______"></span><span id="_______1394CHANNEL______"></span>*1394Channel*   
1394信道号。 有效的信道号是0到62（含）之间的任意整数。 *1394Channel* 必须与目标计算机使用的数字匹配，但不依赖于在适配器上选择的物理1394端口。 有关详细信息，请参阅 [手动设置1394连接](setting-up-a-1394-cable-connection.md)。

<span id="_______1394Protocol______"></span><span id="_______1394protocol______"></span><span id="_______1394PROTOCOL______"></span>*1394Protocol*   
要用于1394内核连接的连接协议。 几乎可以忽略这种情况，因为调试器将自动选择正确的协议。 如果希望手动设置此设置，并且目标计算机运行的是 Windows XP，则应将 *1394Protocol* 设置为 "通道"。 如果目标计算机正在运行 Windows Server 2003 或更高版本，则应将 *1394Protocol* 设置为等于 "instance"。 如果省略，则调试器将默认为适用于当前目标计算机的协议。 这只能通过命令行或环境变量指定，而不能通过 WinDbg 图形界面来指定。

<span id="_______USBString______"></span><span id="_______usbstring______"></span><span id="_______USBSTRING______"></span>*USBString*   
USB 连接字符串。 这必须与通过/targetname boot 选项指定的字符串相匹配。 有关详细信息，请参阅 [手动设置 usb 3.0 连接](setting-up-a-usb-3-0-debug-cable-connection.md) 和 [手动设置 usb 2.0 连接](setting-up-a-usb-2-0-debug-cable-connection.md)。

<span id="_______ComPort______"></span><span id="_______comport______"></span><span id="_______COMPORT______"></span>*ComPort*   
COM 端口的名称。 格式可以是 "com2" 或格式 " \\ \\ 。 \\com2 "，但不应只是一个数字。 有关详细信息，请参阅 [手动设置串行连接](setting-up-a-null-modem-cable-connection.md)。

<span id="_______BaudRate______"></span><span id="_______baudrate______"></span><span id="_______BAUDRATE______"></span>*波特率*   
波特率。 这可以是9600、19200、38400、57600或115200。

<span id="_______VMHost______"></span><span id="_______vmhost______"></span><span id="_______VMHOST______"></span>*VMHost*   
当调试虚拟机时， *VMHost* 指定运行虚拟机的物理计算机的名称。 如果虚拟机运行在与内核调试器自身相同的计算机上，请使用单个句点 (. ) 用于 *VMHost*。 有关详细信息，请参阅 [设置与虚拟机的连接](attaching-to-a-virtual-machine--kernel-mode-.md)。

<span id="_______PipeName______"></span><span id="_______pipename______"></span><span id="_______PIPENAME______"></span>*PipeName*   
虚拟机为调试连接创建的管道的名称。

<span id="_______resets_0"></span><span id="_______RESETS_0"></span> 重置 = 0  
指定当主机和目标正在同步时，可以将不限数量的重置数据包发送到目标。 仅在调试某些类型的虚拟机时需要此参数。

<span id="_______reconnect"></span><span id="_______RECONNECT"></span> 重新连接  
如果发生读/写失败，则使调试器自动断开连接并重新连接管道。 此外，如果在启动调试器时找不到命名管道，则 reconnect 参数将导致其等待显示此名称的管道。 仅在调试某些类型的虚拟机时需要此参数。

<span id="_______-kl"></span><span id="_______-KL"></span> -kl  
使调试器执行本地内核模式调试。 有关详细信息，请参阅 [本地 Kernel-Mode 调试](performing-local-kernel-debugging.md)。

### <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例

以下批处理文件可用于通过 COM 端口连接设置和启动调试会话。

```console
set _NT_SYMBOL_PATH=d:\mysymbols
set _NT_DEBUG_PORT=com1
set _NT_DEBUG_BAUD_RATE=115200
set _NT_DEBUG_LOG_FILE_OPEN=d:\debuggers\logfile1.log
kd
```

以下批处理文件可用于通过1394连接设置和启动调试会话。

```console
set _NT_SYMBOL_PATH=d:\mysymbols
set _NT_DEBUG_BUS=1394
set _NT_DEBUG_1394_CHANNEL=44
set _NT_DEBUG_LOG_FILE_OPEN=d:\debuggers\logfile1.log
kd
```

如果没有任何环境变量，可以使用以下命令行来启动 WinDbg。

**kd-y d： \\ mysymbols-k com： port = com2，波特 = 57600**

**kd： \\ mysymbols-k com： port = \\ \\ 。 \\com2，波特 = 115200**

**kd-y d： \\ mysymbols-k 1394：通道 = 20，符号符号 = 实例**

**kd-y d： \\ mysymbols-k net： port = 50000，key =**<em>AutoGeneratedKey</em>

 

 





