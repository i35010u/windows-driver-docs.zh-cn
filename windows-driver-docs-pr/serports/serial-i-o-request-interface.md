---
title: 串行 I/O 请求接口
description: 若要控制外围设备连接到串行控制器，客户端上的端口的应用程序或外围设备驱动程序将发送到端口的输入/输出请求。
ms.assetid: D536A0EC-2B8B-491B-8A14-656F4B5A3843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6e2ce72e1b26843a1714b6483aaf68b7417793d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327419"
---
# <a name="serial-io-request-interface"></a>串行 I/O 请求接口


若要控制外围设备连接到串行控制器，客户端上的端口的应用程序或外围设备驱动程序将发送到端口的输入/输出请求。 客户端用[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)并[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff546883)若要将数据传输到和从串行端口接收数据的请求。 此外，Windows 还定义一系列[串行 I/O 控制](https://msdn.microsoft.com/library/windows/hardware/ff547466)客户端可以使用配置的串行端口的请求 (Ioctl)。

Serial **IRP\_MJ\_* XXX*** 请求和串行 Ioctl 共同构成支持在系列串行控制器设备的串行 I/O 请求接口。 由 Serial.sys 驱动程序和 SerCx2 或 SerCx 和扩展基于串行控制器驱动程序的组合来支持此接口。

SerCx2、 SerCx 和 Serial.sys 支持许多相同的串行 Ioctl。 但是，SerCx2、 SerCx 和 Serial.sys 支持 Ioctl 中指定的不同子集[串行设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff547466)。 下表汇总了支持的 SerCx2、 SerCx 和 Serial.sys Ioctl 的子集。 一个**是**表中的条目指示串行 framework 扩展插件或驱动程序支持相应 IOCTL，和一个**否**条目指示它没有。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>串行 IOCTL</th>
<th>SerCx2</th>
<th>SerCx</th>
<th>Serial.sys</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406621" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406621)"><strong>IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546538" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLEAR_STATS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546538)"><strong>IOCTL_SERIAL_CLEAR_STATS</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546541" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_DTR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546541)"><strong>IOCTL_SERIAL_CLR_DTR</strong></a></p></td>
<td><p>请参阅备注 1。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546545" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_RTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546545)"><strong>IOCTL_SERIAL_CLR_RTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546548" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CONFIG_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546548)"><strong>IOCTL_SERIAL_CONFIG_SIZE</strong></a></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546554" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_BAUD_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546554)"><strong>IOCTL_SERIAL_GET_BAUD_RATE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546558" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_CHARS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546558)"><strong>IOCTL_SERIAL_GET_CHARS</strong></a></p></td>
<td><p>请参阅备注 2。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546562" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_COMMSTATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546562)"><strong>IOCTL_SERIAL_GET_COMMSTATUS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546566" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_DTRRTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546566)"><strong>IOCTL_SERIAL_GET_DTRRTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546574" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_HANDFLOW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546574)"><strong>IOCTL_SERIAL_GET_HANDFLOW</strong></a></p></td>
<td><p>请参阅备注 1。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546582" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_LINE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546582)"><strong>IOCTL_SERIAL_GET_LINE_CONTROL</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546591" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546591)"><strong>IOCTL_SERIAL_GET_MODEM_CONTROL</strong> </a> （请参阅备注 4）。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546587" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEMSTATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546587)"><strong>IOCTL_SERIAL_GET_MODEMSTATUS</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546597" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_PROPERTIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546597)"><strong>IOCTL_SERIAL_GET_PROPERTIES</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546600" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_STATS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546600)"><strong>IOCTL_SERIAL_GET_STATS</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546604" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_TIMEOUTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546604)"><strong>IOCTL_SERIAL_GET_TIMEOUTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546610" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_WAIT_MASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546610)"><strong>IOCTL_SERIAL_GET_WAIT_MASK</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546620" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_IMMEDIATE_CHAR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546620)"><strong>IOCTL_SERIAL_IMMEDIATE_CHAR</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546649" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_LSRMST_INSERT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546649)"><strong>IOCTL_SERIAL_LSRMST_INSERT</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546655" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_PURGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546655)"><strong>IOCTL_SERIAL_PURGE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546671" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_RESET_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546671)"><strong>IOCTL_SERIAL_RESET_DEVICE</strong> </a> （请参阅备注 5）。</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546672" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BAUD_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546672)"><strong>IOCTL_SERIAL_SET_BAUD_RATE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546680" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_OFF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546680)"><strong>IOCTL_SERIAL_SET_BREAK_OFF</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546685" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_ON&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546685)"><strong>IOCTL_SERIAL_SET_BREAK_ON</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546688" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_CHARS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546688)"><strong>IOCTL_SERIAL_SET_CHARS</strong></a></p></td>
<td><p>请参阅备注 2。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546696" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_DTR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546696)"><strong>IOCTL_SERIAL_SET_DTR</strong></a></p></td>
<td><p>请参阅备注 1。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546720" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_FIFO_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546720)"><strong>IOCTL_SERIAL_SET_FIFO_CONTROL</strong></a></p></td>
<td><p>请参阅备注 1。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546736" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_HANDFLOW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546736)"><strong>IOCTL_SERIAL_SET_HANDFLOW</strong> </a> （请参阅备注 3）。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546740" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_LINE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546740)"><strong>IOCTL_SERIAL_SET_LINE_CONTROL</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546748" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_MODEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546748)"><strong>IOCTL_SERIAL_SET_MODEM_CONTROL</strong> </a> （请参阅备注 4）。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546754" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_QUEUE_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546754)"><strong>IOCTL_SERIAL_SET_QUEUE_SIZE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546760" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_RTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546760)"><strong>IOCTL_SERIAL_SET_RTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546772" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_TIMEOUTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546772)"><strong>IOCTL_SERIAL_SET_TIMEOUTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546780" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_WAIT_MASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546780)"><strong>IOCTL_SERIAL_SET_WAIT_MASK</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546784" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XOFF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546784)"><strong>IOCTL_SERIAL_SET_XOFF</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546793" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XON&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546793)"><strong>IOCTL_SERIAL_SET_XON</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546805" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_WAIT_ON_MASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546805)"><strong>IOCTL_SERIAL_WAIT_ON_MASK</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546812" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_XOFF_COUNTER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546812)"><strong>IOCTL_SERIAL_XOFF_COUNTER</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  SerCx2 可能或可能不支持此 IOCTL，具体取决于实现串行控制器驱动程序和串行控制器硬件的功能。

2.  SerCx2 不支持特殊字符。 总是完成 SerCx2 **IOCTL\_串行\_设置\_CHARS**状态请求\_成功状态代码，但不设置任何特殊字符或执行其他操作此请求的响应。 有关**IOCTL\_串行\_获取\_CHARS**请求，SerCx2 设置中的所有字符值[**串行\_CHARS** ](https://msdn.microsoft.com/library/windows/hardware/jj673020)结构为 null，且完成状态请求\_成功状态代码。

3.  SerCx2 和 SerCx 支持仅为定义的标志的子集**FlowReplace**并**ControlHandShake**的成员**串行\_HANDFLOW**结构。 Serial.sys 支持所有这些标志。 有关详细信息，请参阅[**串行\_HANDFLOW**](https://msdn.microsoft.com/library/windows/hardware/jj680685)。

4.  **IOCTL\_串行\_获取\_调制解调器\_控制**并**IOCTL\_串行\_设置\_调制解调器\_控制**请求主要用于硬件测试。 没有标准注册布局定义的调制解调器控制操作。 使用调制解调器控制 Ioctl 风险使自己依赖于特定的串行控制器的硬件功能的外围设备驱动程序。

5.  Serial.sys 驱动程序始终完成**IOCTL\_串行\_重置\_设备**状态请求\_成功，但不执行任何操作以响应此请求。 不支持 SerCx2 和 SerCx **IOCTL\_串行\_重置\_设备**请求，并始终完成这些请求的状态\_不\_实现。

有关详细信息**IOCTL\_串行\_* XXX*** 的请求，请参阅[串行设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff547466)。 详细信息大约读取和写入请求为串行控制器，请参阅[序列主要 I/O 请求](https://msdn.microsoft.com/library/windows/hardware/ff547484)。

 

 




