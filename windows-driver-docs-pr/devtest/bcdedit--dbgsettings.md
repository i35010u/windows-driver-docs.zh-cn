---
title: BCDEdit /dbgsettings
description: /Dbgsettings 选项设置或显示计算机的当前全局调试器设置。
ms.assetid: df2fe55c-2752-4e0c-a4c0-004235b85e22
ms.date: 04/23/2019
keywords:
- BCDEdit/dbgsettings 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /dbgsettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6a626f6a5f49c46c3dcf3cb96aef6c106193ded6
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778776"
---
# <a name="bcdedit-dbgsettings"></a>BCDEdit /dbgsettings


**/Dbgsettings**选项设置或显示计算机的当前全局调试器设置。 若要启用或禁用内核调试器，请使用 [**BCDEdit/debug**](bcdedit--debug.md) 选项。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。


``` syntax
bcdedit /dbgsettings NET HOSTIP:ip PORT:port [KEY:key] [nodhcp] [newkey] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings LOCAL [/start startpolicy] [/noumex] 

bcdedit /dbgsettings SERIAL [DEBUGPORT:port] [BAUDRATE:baud] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings USB [TARGETNAME:targetname] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings 1394 [CHANNEL:channel] [/start startpolicy] [/noumex] NOTE: The 1394 TRANSPORT IS DEPRECATED
```

<a name="parameters"></a>参数
----------

## <a name="net"></a>NET

指定目标计算机和主机将使用以太网网络连接进行调试。 使用此选项时，还必须包含 **HOSTIP** 和 **PORT** 参数。 目标计算机必须具有 Windows 调试工具支持的网络适配器。 

**HOSTIP：**<em>ip</em>   
对于网络调试，指定主机调试器的 IP 地址。

**键：**<em>键</em>   
对于网络调试，指定用于对连接进行加密的密钥。 只允许 0-9 和 a-z 中的字符\[\]\[\]。 如果已指定 **newkey** 参数，请不要指定此参数。

**端口：**<em>端口</em>  
对于 "网络调试"，指定要在主机调试器上与之通信的端口。 必须是 49152 或以上。

**newkey**   
对于网络调试，指定应为连接生成新的加密密钥。 如果已指定 **密钥** 参数，请不要指定此参数。

**nodhcp**

设置 *nodhcp* 可防止使用 DHCP 获取目标 IP 地址。 很少需要此选项，因为较小的路由器为 DHCP 提供了支持。 仅当你知道网络上没有 DHCP 服务器时，才应使用 *nodhcp* 选项。  在大多数情况下，如果未设置此选项，并且启用了 DHCP，则 KDNET 传输的效果最佳。

**busparams** =*Bus. Function*指定目标控制器。 Bus 指定总线号，Device 指定设备号，Function 指定功能号  。  

若要指定总线参数，请打开设备管理器，然后找到要用于调试的网络适配器。 打开网络适配器的属性页，并记下 "总线号"、"设备号" 和 "功能编号"。 这些值将显示在 "*常规*" 选项卡上的 "*位置*" 下设备管理器。在提升的命令提示符窗口中，输入以下命令，其中 b、d 和 f 是以十进制格式表示的总线、设备和函数编号：

```console
bcdedit /set "{dbgsettings}" busparams b.d.f
```

如果要手动配置调试器连接，则必须指定总线参数。 有关详细信息，请参阅手动 [设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection.md) ，并 [通过 USB 3.0 电缆手动设置内核模式调试](../debugger/setting-up-a-usb-3-0-debug-cable-connection.md)。

## <a name="examples"></a>示例

以下命令将目标计算机配置为使用以太网连接进行调试，并指定主计算机的 IP 地址。 此命令还指定主机可用于连接到目标计算机的端口号。 

``` console
bcdedit /dbgsettings net hostip:10.125.5.10 port:50000
```

以下命令使用 IPv6 将全局调试器设置设置为在2001：48： d8：2f：5e： c0：42：28：4f5b 在端口50000上进行通信的情况下使用 IPv6 进行网络调试：

``` console
bcdedit /dbgsettings NET HOSTIPV6:2001:48:d8:2f:5e:c0:42:28:4f5b PORT:50000
```

 > [!IMPORTANT]
> 手动设置网络调试是一种复杂且容易出错的过程。
> 若要自动设置网络调试，请参阅 [自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。 **强烈**建议所有调试器用户使用 KDNET 实用程序。

有关手动设置的详细信息，请参阅 [通过网络电缆手动设置内核模式调试](../debugger/setting-up-a-network-debugging-connection.md)。


## <a name="local"></a>LOCAL

**Local**选项将全局调试选项设置为本地调试。 这是一台计算机上的内核模式调试。 换句话说，调试器在正在调试的同一台计算机上运行。 利用本地调试，可以检查状态，但不会中断会导致操作系统停止运行的内核模式进程。

### <a name="example"></a>示例

以下命令将全局调试器设置设置为本地调试。

``` console
bcdedit /dbgsettings LOCAL
```

本地选项在 Windows 8.0 和 Windows Server 2012 及更高版本中可用。

有关手动设置本地内核模式调试的信息，请参阅 [手动设置单台计算机的本地内核调试](../debugger/setting-up-local-kernel-debugging-of-a-single-computer-manually.md)。

## <a name="serial"></a>串行

指定目标计算机和主机将使用串行连接进行调试。 使用此选项时，应指定 **DEBUGPORT** 和 **波特率** 参数。

**波特率：**<em>波特</em>   
指定要使用的波特率。 此参数是可选的。 *波特*的有效值为9600、19200、38400、57600和115200。 默认波特速率为 115200 bps。

**DEBUGPORT：**<em>端口</em>   
 指定要用作调试端口的串行端口。 这是一个可选设置。 默认端口为 **1** (COM 1) 。

### <a name="example"></a>示例

以下命令将目标计算机配置为使用串行连接进行调试。 此命令还指定调试连接将使用 COM1，波特率为115200。 

``` console
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```
有关详细信息，请参阅 [通过串行电缆手动设置内核模式调试](../debugger/setting-up-a-null-modem-cable-connection.md)。

## <a name="usb"></a>USB   
指定目标计算机和主机将使用 USB 2.0 或 USB 3.0 连接进行调试。 使用此选项时，还必须包含 **TARGETNAME** 参数。 

**Targetname：** <em>targetname</em>   
指定要用于目标名称的字符串值。 请注意，TargetName 不必是目标计算机的正式名称;它可以是您创建的任何字符串，只要它满足以下限制：

- 字符串不得以大写或小写的任意组合包含在 TargetName 中任意位置的 "debug"。 例如，如果在 targetname 中的任何位置使用 "调试" 或 "调试"，则调试将不会正常工作。
- 字符串中的唯一字符是连字符 (-) 、下划线 (_) 、数字0到9以及字母 A 到 Z (大写或小写。
- 字符串的最大长度为24个字符。


### <a name="example"></a>示例

以下命令将目标计算机配置为使用 USB 连接进行调试。 此命令还指定主机可用于连接到目标计算机的目标名称。 

``` console
bcdedit /dbgsettings usb targetname:myTarget
```

有关详细信息，请参阅：

- [手动设置通过 USB 3.0 线缆进行的内核模式调试](../debugger/setting-up-a-usb-3-0-debug-cable-connection.md)
- [手动设置通过 USB 2.0 线缆进行的内核模式调试](../debugger/setting-up-a-usb-2-0-debug-cable-connection.md)



## <a name="1394"></a>1394   

> [!IMPORTANT]
> 1394 传输可用于 Windows 10 版本 1607 及更低版本。 它在 Windows 的更高版本中不可用。 应将项目转换为其他传输，例如使用以太网的 KDNET。 有关该传输的详细信息，请参阅[自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。
>

指定目标计算机和主机将使用 IEEE 1394 (火线) 连接进行调试。 使用此选项时，还可以包含 **通道** 参数。 

**通道：**<em>通道</em>   
仅当连接类型为 **1394**时才使用 (。 ) 指定要使用的1394通道。 *通道*的值必须是0到62（含）之间的十进制整数，并且必须与主计算机使用的通道号匹配。 此参数中指定的通道不依赖于在适配器上选择的物理1394端口。 *通道*的默认值为0。

有关详细信息，请参阅 [通过1394电缆手动设置内核模式调试](../debugger/setting-up-a-1394-cable-connection.md)。

## <a name="general-debugger-settings"></a>常规调试器设置

**/start** <em>startpolicy</em>   
此选项指定调试器启动策略。 下表显示了 *startpolicy*的选项。

|选项|说明|
|--- |--- |
|ACTIVE|指定内核调试器处于活动状态。|
|AUTOENABLE|指定在发生异常或其他关键事件时自动启用内核调试器。 在此之前，调试程序处于活动状态，但处于禁用状态。|
|DISABLE|指定在键入 kdbgctrl 时启用内核调试器以清除 enable 块。 在此之前，调试程序处于活动状态，但处于禁用状态。|
 

如果未指定启动策略，则默认为 "活动"。

**/noumex**   
指定内核调试器忽略用户模式异常。 默认情况下，内核调试器中断某些用户模式异常，如状态 \_ 断点和 \_ 单 \_ 步执行状态。 仅当没有用户模式调试器附加到进程时， **/noumex** 参数才有效。

### <a name="comments"></a>注释

**/Dbgsettings**选项配置调试设置，但不启用调试。 必须使用 **/debug** 选项启用特定启动项的调试。 如果没有为特定启动项指定调试设置，则使用默认的调试设置。 

下表显示了 dbgsettings 的默认值。

|dbgsetting 参数|默认值|
|--- |--- |
|debugtype|Local|
|debugstart|可用|
|noumex|是|


<a name="see-also"></a>请参阅
--------

有关 Windows 调试工具的信息，请参阅 [Windows 调试](../debugger/index.md)。 

有关设置和配置内核模式调试会话的信息，请参阅 [手动设置内核模式调试](../debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md) 和 [自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。



