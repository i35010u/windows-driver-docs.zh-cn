---
title: AV/C 子单元驱动程序调试
description: AV/C 子单元驱动程序调试
keywords:
- Avc.sys 函数驱动程序 WDK，调试
- 跟踪消息 WDK AV/C
- 消息 WDK AV/C
- 调试驱动程序 WDK AV/C
- 一般消息 WDK AV/C
- 即插即用 WDK AV/C
- PnP WDK AV/C
- 电源管理 WDK AV/C
- I/O WDK AV/C
- 连接消息 WDK AV/C
- AV/C WDK，调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 887bbe6730887409f42d24898ca4152b41b1369b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805995"
---
# <a name="avc-subunit-driver-debugging"></a>AV/C 子单元驱动程序调试





在 Windows Vista 之前， *Avc.sys* 的调试版本允许将跟踪消息输出到调试窗口。 *Avc.sys* 的 windows Vista 版本使用 WINDOWS (ETW) 的事件跟踪。

*AvcDebugLevel* ULONG 类型是可能的跟踪级别的位图。 每个半字节表示一个跟踪输出类别。 默认值为0x00CCCCCC，它将所有消息类别设置为 "错误" 和 "警告" 输出级别。 监视 AV/C 命令活动的最佳设置是 0x000ECCCC (将消息的跟踪类添加到输出) 的 AV/C 类别。 若要关闭所有调试输出，请将所有位设置为0。 下面描述了每个类别的位图。

**一般消息类别**

泛型类别适用于所有泛型输出。 最感兴趣的输出类是 FLOW，启用后，会在每个函数的入口和出口点记录一条消息。 在运行 Windows Millennium Edition 的计算机上 (Windows Me) 、Windows 98 或 Windows 95，所有 TL \_ FLOW (和大多数 tl \_ 跟踪消息) 转到 ntkern 循环缓冲池。 若要查看这些日志条目，请在调试器中使用 **ntkern** ，然后选择 D 选项。 按 D 后按空格键继续转储缓冲区，一次一页。 按任意键以取消转储。 若要关闭 ntkern 日志记录并将消息发送到标准调试输出，请使用 **e ulind** 调试器命令将 **ulind** 变量设置为 1 (默认设置为 0) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_MASK</p></td>
<td><p>0x0000000F</p></td>
</tr>
<tr class="even">
<td><p>TL_FLOW</p></td>
<td><p>0x00000001</p></td>
</tr>
<tr class="odd">
<td><p>TL_TRACE</p></td>
<td><p>0x00000002</p></td>
</tr>
<tr class="even">
<td><p>TL_WARNING</p></td>
<td><p>0x00000004</p></td>
</tr>
<tr class="odd">
<td><p>TL_ERROR</p></td>
<td><p>0x00000008</p></td>
</tr>
</tbody>
</table>

 

**即插即用消息类别**

即插即用 (PnP) 类别适用于与 PnP 相关的所有输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_PNP_MASK</p></td>
<td><p>0x000000F0</p></td>
</tr>
<tr class="even">
<td><p>TL_PNP_TRACE</p></td>
<td><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td><p>TL_PNP_WARNING</p></td>
<td><p>0x00000040</p></td>
</tr>
<tr class="even">
<td><p>TL_PNP_ERROR</p></td>
<td><p>0x00000080</p></td>
</tr>
</tbody>
</table>

 

**电源管理消息类别**

"电源管理" 类别适用于所有与电源管理相关的输出，包括休眠。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_POWER_MASK</p></td>
<td><p>0x00000F00</p></td>
</tr>
<tr class="even">
<td><p>TL_POWER_TRACE</p></td>
<td><p>0x00000200</p></td>
</tr>
<tr class="odd">
<td><p>TL_POWER_WARNING</p></td>
<td><p>0x00000400</p></td>
</tr>
<tr class="even">
<td><p>TL_POWER_ERROR</p></td>
<td><p>0x00000800</p></td>
</tr>
</tbody>
</table>

 

**I/o 消息类别**

I/o 类别适用于与 interdriver 通信相关的所有输出，包括 IRP 处理。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_IO_MASK</p></td>
<td><p>0x0000F000</p></td>
</tr>
<tr class="even">
<td><p>TL_IO_NOISE</p></td>
<td><p>0x00001000</p></td>
</tr>
<tr class="odd">
<td><p>TL_IO_TRACE</p></td>
<td><p>0x00002000</p></td>
</tr>
<tr class="even">
<td><p>TL_IO_WARNING</p></td>
<td><p>0x00004000</p></td>
</tr>
<tr class="odd">
<td><p>TL_IO_ERROR</p></td>
<td><p>0x00008000</p></td>
</tr>
</tbody>
</table>

 

**AV/C 消息类别**

AV/C 类别适用于与 AV/C 命令相关的所有输出，以及一些可能与对象列表和旋转锁 (TL \_ IO \_ 干扰 I/o 消息类别) 相关的内部驱动程序消息。 在消息的 TL \_ IO \_ 跟踪类别中包含的是命令执行时间。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_AVC_MASK</p></td>
<td><p>0x000F0000</p></td>
</tr>
<tr class="even">
<td><p>TL_AVC_NOISE</p></td>
<td><p>0x00010000</p></td>
</tr>
<tr class="odd">
<td><p>TL_AVC_TRACE</p></td>
<td><p>0x00020000</p></td>
</tr>
<tr class="even">
<td><p>TL_AVC_WARNING</p></td>
<td><p>0x00040000</p></td>
</tr>
<tr class="odd">
<td><p>TL_AVC_ERROR</p></td>
<td><p>0x00080000</p></td>
</tr>
</tbody>
</table>

 

**连接消息类别**

连接类别处理与连接相关的所有输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_CXN_MASK</p></td>
<td><p>0x00F00000</p></td>
</tr>
<tr class="even">
<td><p>TL_CXN_NOISE</p></td>
<td><p>0x00100000</p></td>
</tr>
<tr class="odd">
<td><p>TL_CXN_TRACE</p></td>
<td><p>0x00200000</p></td>
</tr>
<tr class="even">
<td><p>TL_CXN_WARNING</p></td>
<td><p>0x00400000</p></td>
</tr>
<tr class="odd">
<td><p>TL_CXN_ERROR</p></td>
<td><p>0x00800000</p></td>
</tr>
</tbody>
</table>

 

 

 




