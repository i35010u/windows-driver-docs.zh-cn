---
title: AV/C 子单元驱动程序调试
description: AV/C 子单元驱动程序调试
ms.assetid: d669157c-60fa-4b7a-8f33-58923a3f2230
keywords:
- Avc.sys 功能驱动程序 WDK，调试
- 跟踪消息 WDK AV/C
- 消息 WDK AV/C
- 调试驱动程序 WDK AV/C
- 一般消息 WDK AV/C
- Plug and Play WDK AV/C
- 即插即用 WDK AV/C
- 电源管理 WDK AV/C
- I/O WDK AV/C
- 连接消息 WDK AV/C
- AV/C WDK 调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35ef78fbb475fc80fff515b32170c17ae84535d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323510"
---
# <a name="avc-subunit-driver-debugging"></a>AV/C 子单元驱动程序调试





在 Windows Vista 的调试版本之前*Avc.sys*允许跟踪消息输出到调试窗口。 Windows Vista 版本的*Avc.sys*使用事件跟踪 Windows (ETW)。

*AvcDebugLevel* ULONG 类型是可能的跟踪级别的位图。 每个半字节表示的跟踪输出的类别。 默认值为 0x00CCCCCC，它将所有消息类别都设置为错误和警告输出级别。 监视 AV/C 命令活动的最佳设置是的 0x000ECCCC （将消息的 TRACE 类添加到输出的 AV/C 类别）。 若要关闭所有调试输出，请将所有位都设置为 0。 下面描述了每个类别的位图。

**一般消息类别**

泛型类别会应用于所有的泛型输出。 输出的最有趣类流，当启用时，记录每个函数的入口和出口点的一条消息。 在运行 Windows Millennium Edition (Windows Me)、 Windows 98 或 Windows 95 中，所有 TL\_流 (和大多数 TL\_跟踪消息) 转到.ntkern 循环缓冲区池。 若要查看这些日志条目，请使用类型 **.ntkern**调试器，然后选择 D 选项。 按 D 继续转储的缓冲区，一次一页后按空格键。 按任意键取消转储。 若要启用关闭.ntkern 日志记录并将消息发送到标准调试输出，请使用**e ulind**调试器命令，以设置**ulind**变量为 1 （默认设置为 0）。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>ReplTest1</th>
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

 

**Plug and Play 消息类别**

插即用 (PnP) 类别会应用于与即插即用相关的所有输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>ReplTest1</th>
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

电源管理类别会应用到与电源管理，包括休眠状态相关的所有输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>ReplTest1</th>
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

 

**I/O 消息类别**

I/O 类别会应用于与 interdriver 通信，包括 IRP 处理相关的所有输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>值</th>
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

AV/C 类别会应用于与 AV/C 命令相关的所有输出以及潜在的相关性对象列表和旋转锁某些内部驱动程序消息 (TL\_IO\_干扰 I/O 消息类别)。 包含在 TL\_IO\_跟踪类别的消息是命令执行时间。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>值</th>
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

连接类别处理的所有即插即用连接相关的输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>含义</th>
<th>ReplTest1</th>
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

 

 

 




