---
title: BCDEdit /dbgsettings
description: /Dbgsettings 选项设置，或显示计算机的当前全局调试器设置。
ms.assetid: df2fe55c-2752-4e0c-a4c0-004235b85e22
ms.date: 04/23/2019
keywords:
- BCDEdit /dbgsettings 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /dbgsettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e5441240e79c050ab937d5e7b581eb991598393
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371670"
---
# <a name="bcdedit-dbgsettings"></a>BCDEdit /dbgsettings


**/Dbgsettings**选项设置，或显示计算机的当前全局调试器设置。 若要启用或禁用内核调试程序，请使用[ **BCDEdit /debug** ](bcdedit--debug.md)选项。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。


``` syntax
bcdedit /dbgsettings NET HOSTIP:ip PORT:port [KEY:key] [nodhcp] [newkey] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings LOCAL [/start startpolicy] [/noumex] 

bcdedit /dbgsettings SERIAL [DEBUGPORT:port] [BAUDRATE:baud] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings USB [TARGETNAME:targetname] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings 1394 [CHANNEL:channel] [/start startpolicy] [/noumex] NOTE: The 1394 TRANSPORT IS DEPRECATED
```

<a name="parameters"></a>Parameters
----------

## <a name="net"></a>NET

指定目标计算机和主机计算机将用于调试使用以太网网络连接。 使用此选项时，**主机**并**端口**参数必须是包含。 目标计算机必须具有有关 Windows 调试工具支持的网络适配器。 

**主机：** <em>ip</em>   
为网络调试，指定主机调试器的 IP 地址。

**密钥：** <em>密钥</em>   
为网络调试，指定用来对连接进行加密密钥。 \[0-9\]并\[a 到 z\]仅允许。 如果已指定未指定此参数**newkey**参数。

**端口：** <em>端口</em>  
为网络调试，指定要与主机调试器上进行通信的端口。 应为 49152 或更高版本。

**newkey**   
为网络调试指定应连接生成新的加密密钥。 如果已指定未指定此参数**密钥**参数。

**nodhcp**

设置*nodhcp*避免使用 DHCP 获取目标 IP 地址。 很少需要此选项，因为甚至小型路由器提供用于 DHCP 的支持。 *Nodhcp*应仅使用选项，如果您知道在网络上没有 DHCP 服务器。  在大多数情况下，KDNET 传输时效果最佳未设置此选项，并且已启用 DHCP。

**busparams**=*Bus.Device.Function*时存在多个控制器指定的目标控制器。 *总线*指定总线数*设备*指定设备数，和*函数*指定的函数数目。  

若要指定总线参数，打开设备管理器，并找到你想要用于调试的网络适配器。 打开的网络适配器，属性页，并记下总线编号、 设备数量和函数编号。 在提升的命令提示符窗口，输入以下命令，其中 b、 d 和 f 的十进制格式的总线、 设备和函数编号：

```console
bcdedit /set "{dbgsettings}" busparams b.d.f
```

如果您在手动配置连接调试器，则必须指定总线参数。 有关详细信息，请参阅[设置向上 KDNET 网络内核调试手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)并[设置内核模式调试通过 USB 3.0 电缆手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)。

### <a name="examples"></a>示例

以下命令来配置目标计算机要用于调试的以太网连接，并指定主计算机的 IP 地址。 该命令还指定主计算机可用于连接到目标计算机的端口号。 

``` console
bcdedit /dbgsettings net hostip:10.125.5.10 port:50000
```

以下命令设置全局调试器设置网络与在 2001:48:d8:2f:5e:c0:42:28:4f5b 端口 50000 上进行通信的调试器主机使用 IPv6 进行调试：

``` console
bcdedit /dbgsettings NET HOSTIPV6:2001:48:d8:2f:5e:c0:42:28:4f5b PORT:50000
```

 > [!IMPORTANT]
> 设置手动调试网络是一个复杂和错误容易过程。
> 若要设置网络自动调试，请参阅[设置向上 KDNET 网络内核调试自动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)。 使用 KDNET 实用工具是**强**建议所有调试器的用户。

有关手动安装的详细信息，请参阅[设置内核模式调试通过网络电缆手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)。


## <a name="local"></a>本地

**本地**选项将全局的调试选项设置为本地调试。 这是一台计算机上的内核模式调试。 换而言之，调试器在正在调试的同一台计算机上运行。 使用本地调试，您可以检查状态，但不是会中断到内核模式进程会导致停止运行的操作系统。

### <a name="example"></a>示例

以下命令设置全局调试器设置为本地调试。

``` console
bcdedit /dbgsettings LOCAL
```

本地选项是可用在 Windows 8.0 和 Windows Server 2012 及更高版本。

有关设置本地内核模式调试手动，请参阅[设置本地内核调试的单个计算机手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-local-kernel-debugging-of-a-single-computer-manually)。

## <a name="serial"></a>串行

指定目标计算机和主机计算机将用于调试使用串行连接。 使用此选项时， **DEBUGPORT**并**BAUDRATE**应指定参数。

**BAUDRATE:** <em>波特率</em>   
指定要使用的波特率。 该参数为可选参数。 有效值*波特率*为 9600、 19200、 38400、 57600 和 115200。 默认的波特率是 115200 bps。

**DEBUGPORT:** <em>端口</em>   
 指定要用作调试端口的串行端口。 这是一个可选设置。 默认端口是**1** (COM 1)。

### <a name="example"></a>示例

以下命令将目标计算机要用于串行连接调试配置。 该命令还指定调试连接将使用 COM2 和 115200 波特率。 

``` console
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```
有关详细信息，请参阅[设置内核模式调试通过串行电缆手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-null-modem-cable-connection)。

## <a name="usb"></a>USB   
指定目标计算机和主机计算机将用于调试使用 USB 2.0 或 USB 3.0 连接。 使用此选项时， **TARGETNAME**参数必须是包含。 

**TARGETNAME:** <em>targetname</em>   
指定要使用的目标名称的字符串值。 请注意，TargetName 不一定要在目标计算机; 的正式名称它可以是任何字符串，只要它满足这些限制创建：

- 字符串不得包含"debug"任意位置中的任何组合的大写或小写 TargetName 中。 例如，如果您使用"调试"或"调试"任意位置在您 targetname，调试将无法正常工作。
- 在字符串中的唯一字符是连字符 （-）、 下划线 （_）、 0 到 9 的数字和字母 A 到 Z （上限或下限的情况下）。
- 字符串的最大长度为 24 个字符。


### <a name="example"></a>示例

以下命令将目标计算机要用于 USB 连接调试配置。 该命令还指定主计算机可用于连接到目标计算机的目标名称。 

``` console
bcdedit /dbgsettings usb targetname:myTarget
```

有关详细信息，请参阅：

- [内核模式调试通过 USB 3.0 电缆手动设置](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)
- [内核模式调试通过 USB 2.0 电缆手动设置](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-2-0-debug-cable-connection)



## <a name="1394"></a>1394   

> [!IMPORTANT]
> 1394 传输协议是可在 Windows 10，版本 1607年及更早版本中使用。 不在更高版本的 Windows 中可用。 应转换到其他传输，如使用以太网 KDNET 项目。 有关该传输的详细信息，请参阅[设置向上 KDNET 网络内核调试自动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)。
>

指定目标计算机和主机计算机将用于调试使用 IEEE 1394 (FireWire) 连接。 使用此选项时，**通道**参数可以是包含。 

**通道：** <em>通道</em>   
(仅在连接类型时，使用**1394年**。)指定要使用的 1394年通道。 值*通道*必须是介于 0 和 62，非独占，十进制整数，并且必须匹配的主机计算机使用的通道数。 此参数中指定的通道不依赖于选择将在适配器上的物理 1394年端口。 默认值为*通道*为 0。

有关详细信息，请参阅[设置内核模式调试通过 1394年电缆手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-1394-cable-connection)。

## <a name="general-debugger-settings"></a>常规调试程序设置

**/start** <em>startpolicy</em>   
此选项指定调试器启动策略。 下表显示的选项*startpolicy*。

|Option|描述|
|--- |--- |
|ACTIVE|指定内核调试程序处于活动状态。|
|AUTOENABLE|指定发生异常或其他关键事件时，会自动启用内核调试程序。 到那时，调试器处于活动状态，但被禁用。|
|禁用|指定当您键入 kdbgctrl 清除启用块时启用了内核调试器。 到那时，调试器处于活动状态，但被禁用。|
 

如果未指定启动策略，活动是默认值。

**/noumex**   
指定内核调试程序忽略用户模式下的异常。 默认情况下内核调试器中断对于某些用户模式异常，如状态\_断点和状态\_单个\_步骤。 **/Noumex**参数仅当没有用户模式调试器附加到进程时才有效。

### <a name="comments"></a>备注

**/Dbgsettings**选项配置的调试设置，但不会启用调试。 必须使用 **/debug**选项以启用特定的启动项的调试。 如果没有指定为特定的启动项目调试设置，将使用默认调试设置。 

Dbgsettings 的默认值是下表中所示。

|dbgsetting 参数|默认值|
|--- |--- |
|Debugtype|本地|
|debugstart|活跃|
|noumex|是|


<a name="see-also"></a>请参阅
--------

有关 Windows 调试工具的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。 

有关设置和配置内核模式调试会话，请参阅[设置了内核模式调试手动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd)并[设置向上 KDNET 网络内核调试自动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)。



 





