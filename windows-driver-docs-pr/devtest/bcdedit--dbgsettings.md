---
title: BCDEdit /dbgsettings
description: /Dbgsettings 选项设置，或显示计算机的当前全局调试器设置。
ms.assetid: df2fe55c-2752-4e0c-a4c0-004235b85e22
ms.date: 07/02/2018
keywords:
- BCDEdit /dbgsettings 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /dbgsettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f2bda2c91ab1de08815a61f3ee85080cb625381
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540863"
---
# <a name="bcdedit-dbgsettings"></a>BCDEdit /dbgsettings


**/Dbgsettings**选项设置，或显示计算机的当前全局调试器设置。 若要启用或禁用内核调试程序，请使用[ **BCDEdit /debug** ](bcdedit--debug.md)选项。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

 

``` syntax
bcdedit /dbgsettings SERIAL [DEBUGPORT:port] [BAUDRATE:baud] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings 1394 [CHANNEL:channel] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings USB [TARGETNAME:targetname] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings NET HOSTIP:ip PORT:port [KEY:key] [nodhcp] [newkey] [/start startpolicy] [/noumex] 
```

<a name="parameters"></a>参数
----------

**SERIAL**   
指定目标计算机和主机计算机将用于调试使用串行连接。 使用此选项时， **DEBUGPORT**并**BAUDRATE**参数可以是包含。 有关详细信息，请参阅[设置内核模式调试通过串行电缆手动](https://msdn.microsoft.com/library/windows/hardware/ff556867)。

**1394**   
指定目标计算机和主机计算机将用于调试使用 IEEE 1394 (FireWire) 连接。 使用此选项时，**通道**参数可以是包含。 有关详细信息，请参阅[设置内核模式调试通过 1394年电缆手动](https://msdn.microsoft.com/library/windows/hardware/ff556866)。

**USB**   
指定目标计算机和主机计算机将用于调试使用 USB 2.0 或 USB 3.0 连接。 使用此选项时， **TARGETNAME**参数必须是包含。 有关详细信息，请参阅：

-   [内核模式调试通过 USB 3.0 电缆手动设置](https://msdn.microsoft.com/library/windows/hardware/hh439372)
-   [内核模式调试通过 USB 2.0 电缆手动设置](https://msdn.microsoft.com/library/windows/hardware/ff556869)

**NET**   
指定目标计算机和主机计算机将用于调试使用以太网网络连接。 使用此选项时，**主机**并**端口**参数必须是包含。 目标计算机必须具有有关 Windows 调试工具支持的网络适配器。 有关详细信息，请参阅：

-   [内核模式下通过网络电缆手动调试设置](https://msdn.microsoft.com/library/windows/hardware/hh439346)

**本地**   
**本地**选项将全局的调试选项设置为本地调试。 这是一台计算机上的内核模式调试。 换而言之，调试器在正在调试的同一台计算机上运行。 使用本地调试，您可以检查状态，但不是会中断到内核模式进程会导致停止运行的操作系统。

有关设置本地内核模式调试手动，请参阅[设置本地内核调试的单个计算机手动](https://msdn.microsoft.com/library/windows/hardware/dn553412)。

本地选项是可用在 Windows 8.0 和 Windows Server 2012 及更高版本。

**BAUDRATE:**<em>波特率</em>   
(仅在连接类型时，使用**串行**。)指定要使用的波特率。 该参数为可选参数。 有效值*波特率*为 9600、 19200、 38400、 57600 和 115200。 默认的波特率是 115200 bps。

> [!NOTE]
> 如果通过串行端口的内核模式调试配置的目标计算机上正在运行 Windows 的特殊管理控制台 (SAC) 应用程序，SAC 应用程序可能会导致调试器连接中断。 因为 COM 端口的波特率值更改调试器连接建立后，将发生此事件。 关闭之前运行调试器在 SAC 应用程序或将调试器 COM 端口的波特率值更改为 9600。

 
**通道：**<em>通道</em>   
(仅在连接类型时，使用**1394年**。)指定要使用的 1394年通道。 值*通道*必须是介于 0 和 62，非独占，十进制整数，并且必须匹配的主机计算机使用的通道数。 此参数中指定的通道不依赖于选择将在适配器上的物理 1394年端口。 默认值为*通道*为 0。

**DEBUGPORT:**<em>端口</em>   
(仅在连接类型时，使用**串行**。)指定要用作调试端口的串行端口。 这是一个可选设置。 默认端口是**1** (COM 1)。

**主机：**<em>ip</em>   
(仅在连接类型时，使用**NET**。)为网络调试，指定主机调试器的 IPv4 地址。

**密钥：**<em>密钥</em>   
为网络调试，指定用来对连接进行加密密钥。 \[0-9\]并\[a 到 z\]仅允许。 如果已指定未指定此参数**newkey**参数。

**newkey**   
为网络调试指定应连接生成新的加密密钥。 如果已指定未指定此参数**密钥**参数。

**nodhcp**   
为网络调试会阻止使用 DHCP 获取目标 IP 地址。

<strong>端口：</strong>*端口*   
为网络调试，指定要与主机调试器上进行通信的端口。 应为 49152 或更高版本。

<strong>TARGETNAME:</strong>*targetname*   
(仅在连接类型时，使用**USB**。)指定要使用的目标名称的字符串值。 此字符串可以是任何值。

<strong>\start</strong> *startpolicy*   
此选项指定调试器启动策略。 下表显示的选项*startpolicy*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ACTIVE</strong></p></td>
<td align="left"><p>指定内核调试程序处于活动状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AUTOENABLE</strong></p></td>
<td align="left"><p>指定发生异常或其他关键事件时，会自动启用内核调试程序。 到那时，调试器处于活动状态，但被禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>禁用</strong></p></td>
<td align="left"><p>指定当您键入时启用了内核调试器<strong>kdbgctrl</strong>清除启用块。 到那时，调试器处于活动状态，但被禁用。</p></td>
</tr>
</tbody>
</table>

 

如果未指定启动策略，活动是默认值。

</strong>/noumex</strong>   
指定内核调试程序忽略用户模式下的异常。 默认情况下内核调试器中断对于某些用户模式异常，如状态\_断点和状态\_单个\_步骤。 **/Noumex**参数仅当没有用户模式调试器附加到进程时才有效。

### <a name="comments"></a>备注

**/Dbgsettings**选项配置的全局的调试设置，但不会启用调试。 必须使用 **/debug**选项以启用特定的启动项的调试。 如果没有指定为特定的启动项目调试设置，将使用全局调试设置。 若要重写全局设置，必须使用[ **BCDEdit /set** ](bcdedit--set.md)命令并指定调试参数和值对以及的启动项目的 ID。

全局设置的默认值是使用 115200 波特率在 COM1 串行通信。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">/dbgsetting 参数</th>
<th align="left">默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>连接类型</p></td>
<td align="left"><p>序列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DEBUGPORT:</strong><em>端口</em></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>BAUDRATE:</strong><em>速率</em></p></td>
<td align="left"><p>115200</p></td>
</tr>
</tbody>
</table>

 

有关 Windows 调试工具的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。 有关设置和配置内核模式调试会话，请参阅[设置了内核模式调试手动](https://msdn.microsoft.com/library/windows/hardware/hh439378)。

<a name="examples"></a>示例
--------

以下命令来配置目标计算机要用于调试的以太网连接，并指定主计算机的 IP 地址。 该命令还指定主计算机可用于连接到目标计算机的端口号。 有关详细信息，请参阅[设置内核模式调试通过网络电缆手动](https://msdn.microsoft.com/library/windows/hardware/hh439346)。

``` syntax
bcdedit /dbgsettings net hostip:10.125.5.10 port:50000
```

以下命令将配置目标计算机要用于调试的 1394年连接。 该命令还指定主计算机可用于连接到目标计算机频道号。 有关详细信息，请参阅[设置内核模式调试通过 1394年电缆手动](https://msdn.microsoft.com/library/windows/hardware/ff556866)。

``` syntax
bcdedit /dbgsettings 1394 channel:1
```

以下命令将目标计算机要用于 USB 连接调试配置。 该命令还指定主计算机可用于连接到目标计算机的目标名称。 有关详细信息，请参阅[设置内核模式调试通过 USB 3.0 电缆手动](https://msdn.microsoft.com/library/windows/hardware/hh439372)并[设置内核模式调试通过 USB 2.0 电缆手动](https://msdn.microsoft.com/library/windows/hardware/ff556869)。

``` syntax
bcdedit /dbgsettings usb targetname:myTarget
```

以下命令将目标计算机要用于串行连接调试配置。 该命令还指定调试连接将使用 COM2 和 115200 波特率。 有关详细信息，请参阅[设置内核模式调试通过串行电缆手动](https://msdn.microsoft.com/library/windows/hardware/ff556867)。

``` syntax
bcdedit /dbgsettings serial debugport:2 baudrate:115200
```

<a name="see-also"></a>另请参阅
--------

[内核模式调试手动设置](https://msdn.microsoft.com/library/windows/hardware/hh439378)


 





