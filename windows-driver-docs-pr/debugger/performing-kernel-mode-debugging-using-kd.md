---
title: 实时使用 KD 内核模式调试
description: 实时使用 KD 内核模式调试
ms.assetid: 4C3DB315-CF92-44FC-A54C-0C100A32EB3C
ms.date: 06/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3fa0e69c775859a620f1a7510773e1feda3b7e19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534173"
---
# <a name="span-iddebuggerperformingkernel-modedebuggingusingkdspanlive-kernel-mode-debugging-using-kd"></a><span id="debugger.performing_kernel-mode_debugging_using_kd"></span>实时使用 KD 内核模式调试


在命令提示符窗口中，可以启动时启动 KD 实时内核模式调试会话。 输入以下命令之一。

kd \[-y *SymbolPath*\] -k net:port=*PortNumber*,key=*Key*\[,target=*TargetIPAddress*|*TargetHostName*\] 

kd \[-y *SymbolPath* \] -k 1394:channel =*1394Channel*\[，符号链接 =*1394Protocol*\]

kd \[-y *SymbolPath* \] -k usb:targetname =*USBString*

kd \[-y *SymbolPath*\] -k com:port=*ComPort*,baud=*BaudRate*

kd \[-y *SymbolPath* \] -k com:pipe，端口 =\\\\*VMHost*\\管道\\*PipeName*\[，将重置 = 0\]\[，重新连接\]

kd \[-y *SymbolPath* \] -k com:*调制解调器*

kd \[-y *SymbolPath*\] -kl

kd \[-y *SymbolPath*\] -k

有关详细信息，请参阅[ **KD 命令行选项**](kd-command-line-options.md)。

### <a name="span-idenvironmentvariablesspanspan-idenvironmentvariablesspanspan-idenvironmentvariablesspanenvironment-variables"></a><span id="Environment_Variables"></span><span id="environment_variables"></span><span id="ENVIRONMENT_VARIABLES"></span>环境变量

对于调试通过串行 （COM 端口） 或 1394年连接，可以使用环境变量指定的连接设置。

使用以下变量来指定串行连接。

设置\_NT\_调试\_端口 = *ComPort*

set \_NT\_DEBUG\_BAUD\_RATE = *BaudRate*

使用以下变量来指定 1394年连接。

设置\_NT\_调试\_总线 = 1394年

设置\_NT\_调试\_1394年\_通道 = *1394Channel* 

设置\_NT\_调试\_1394年\_符号链接 = *1394Protocol*

有关详细信息，请参阅[内核模式环境变量](kernel-mode-environment-variables.md)。

### <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数

<span id="_______SymbolPath______"></span><span id="_______symbolpath______"></span><span id="_______SYMBOLPATH______"></span> *SymbolPath*   
符号文件的位置的目录的列表。 由分号分隔列表中的目录。 有关详细信息，请参阅[符号路径](symbol-path.md)。

<span id="_______PortNumber______"></span><span id="_______portnumber______"></span><span id="_______PORTNUMBER______"></span> *PortNumber*   
用于对网络调试使用的端口号。 您可以选择任意数量从 49152 到 65535。 有关详细信息，请参阅[设置了网络连接手动](setting-up-a-network-debugging-connection.md)。

<span id="_______Key______"></span><span id="_______key______"></span><span id="_______KEY______"></span> *密钥*   
要用于网络调试的加密密钥。 我们建议使用 bcdedit 配置目标计算机时提供的自动生成的密钥。 有关详细信息，请参阅[设置了网络连接手动](setting-up-a-network-debugging-connection.md)。


<span id="_______TargetIp______"></span><span id="_______targetip______"></span><span id="_______TARGETIP______"></span> *TargetIPAddress*   
目标计算机的 IPv4 地址。 

当目标 = IP 指定地址，这会导致调试器启动连接到指定的目标计算机中，通过将特定数据包发送到目标，将导致其尝试使用该调试器进行连接。 调试器会将数据包发送到目标重复大约每隔半秒，尝试连接。 如果连接成功，目标将删除任何现有连接，并仅与调试器的此实例进行通信。 这使您能够从现有的调试连接调试会话的控制。 

如果目标配置有主机 IP 地址，且调试器使用配置的主机的 IP 地址在计算机上正在运行，则无需指定目标 = IP 地址参数。 使用主机 IP 地址配置目标后，它将产品/服务向主机发送数据包每三秒。  产品/服务数据包允许将调试器连接到主机时没有目标 = IP 指定地址。

在目标上配置主机的 IP 地址的详细信息，请参阅[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)并[设置向上 KDNET 网络内核调试手动](setting-up-a-network-debugging-connection.md)。


<span id="_______TargetName______"></span><span id="_______targetname______"></span><span id="_______TARGETNAME______"></span> *TargetMachineName*   
计算机的目标 PC 名称。 若要使用的计算机名称，在网络上的 DNS 系统必须具有与目标 PC 的 IP 地址相关联的计算机名称。
 
<span id="_______1394Channel______"></span><span id="_______1394channel______"></span><span id="_______1394CHANNEL______"></span> *1394Channel*   
1394 通道数。 有效的频道号是介于 0 和 62，非独占的任何整数。 *1394Channel*必须与目标计算机使用的数目匹配，但不依赖于选择将在适配器上的物理 1394年端口。 有关详细信息，请参阅[设置 1394年连接手动](setting-up-a-1394-cable-connection.md)。

<span id="_______1394Protocol______"></span><span id="_______1394protocol______"></span><span id="_______1394PROTOCOL______"></span> *1394Protocol*   
要用于 1394年内核连接的连接协议。 这可以几乎始终忽略，因为调试器将自动选择正确的协议。 如果你想要手动将此项设置，并且目标计算机正在运行 Windows XP *1394Protocol*应设置为等于"通道"。 如果目标计算机运行 Windows Server 2003 或更高版本， *1394Protocol*应设置为等于"实例"。 如果省略，则调试器将默认为适用于当前的目标计算机的协议。 这可以通过命令行或环境变量，不能通过 WinDbg 图形界面指定。

<span id="_______USBString______"></span><span id="_______usbstring______"></span><span id="_______USBSTRING______"></span> *USBString*   
USB 连接字符串。 它必须匹配与 /targetname 启动选项指定的字符串。 有关详细信息，请参阅[设置了 USB 3.0 连接手动](setting-up-a-usb-3-0-debug-cable-connection.md)并[设置了 USB 2.0 连接手动](setting-up-a-usb-2-0-debug-cable-connection.md)。

<span id="_______ComPort______"></span><span id="_______comport______"></span><span id="_______COMPORT______"></span> *ComPort*   
COM 端口的名称。 这可以是"com2"格式或采用格式"\\\\。\\com2"，但不是应只需将一个数字。 有关详细信息，请参阅[设置启动串行连接手动](setting-up-a-null-modem-cable-connection.md)。

<span id="_______BaudRate______"></span><span id="_______baudrate______"></span><span id="_______BAUDRATE______"></span> *BaudRate*   
波特率。 这可以是 9600、 19200、 38400、 57600 或 115200。

<span id="_______VMHost______"></span><span id="_______vmhost______"></span><span id="_______VMHOST______"></span> *VMHost*   
虚拟机，在调试时*VMHost*指定在其运行虚拟机的物理计算机的名称。 如果内核调试器本身相同的计算机上运行虚拟机，使用单个句点 （.） 进行*VMHost*。 有关详细信息，请参阅[设置连接到虚拟机](attaching-to-a-virtual-machine--kernel-mode-.md)。

<span id="_______PipeName______"></span><span id="_______pipename______"></span><span id="_______PIPENAME______"></span> *PipeName*   
调试连接的虚拟机创建的管道的名称。

<span id="_______resets_0"></span><span id="_______RESETS_0"></span> 重置 = 0  
指定无限的数量的重置数据包可以发送到目标中，同步主机和目标时。 某些类型的虚拟机在调试时，才需要此参数。

<span id="_______reconnect"></span><span id="_______RECONNECT"></span> 重新连接  
使调试器自动断开连接并在读/写失败时重新连接管道。 此外，如果启动调试器时找不到命名的管道，重新连接参数将导致它等待管道才会显示此名称。 某些类型的虚拟机在调试时，才需要此参数。

<span id="_______-kl"></span><span id="_______-KL"></span> -kl  
使调试器执行本地内核模式调试。 有关详细信息，请参阅[本地内核模式调试](performing-local-kernel-debugging.md)。

### <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的批处理文件可以用于设置和通过 COM 端口连接启动调试会话。

```console
set _NT_SYMBOL_PATH=d:\mysymbols
set _NT_DEBUG_PORT=com1
set _NT_DEBUG_BAUD_RATE=115200
set _NT_DEBUG_LOG_FILE_OPEN=d:\debuggers\logfile1.log
kd
```

下面的批处理文件可以用于设置和通过 1394年连接启动调试会话。

```console
set _NT_SYMBOL_PATH=d:\mysymbols
set _NT_DEBUG_BUS=1394
set _NT_DEBUG_1394_CHANNEL=44
set _NT_DEBUG_LOG_FILE_OPEN=d:\debuggers\logfile1.log
kd
```

无法使用以下命令行启动 WinDbg，而无需任何环境变量。

**kd -y d:\\mysymbols -k com:port=com2,baud=57600**

**kd-y d:\\mysymbols-k com:port =\\\\。\\com2 波特率 = 115200**

**kd-y d:\\mysymbols-k 1394:channel = 20，符号链接 = 实例**

**kd-y d:\\mysymbols-k net: port = 50000，密钥 =**<em>AutoGeneratedKey</em>

 

 





