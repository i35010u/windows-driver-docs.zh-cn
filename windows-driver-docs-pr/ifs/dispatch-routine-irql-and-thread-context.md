---
title: 调度例程 IRQL 和线程上下文
description: 调度例程 IRQL 和线程上下文
ms.assetid: 95f3a976-c97a-4c8a-979b-14a0ddd823a2
keywords:
- IRP 调度例程 WDK 文件系统，IRQL
- IRP 调度例程 WDK 文件系统，线程上下文
- nonarbitrary 线程上下文 WDK 文件系统
- 线程上下文 WDK 文件系统
- 任意线程上下文 WDK 文件系统
- 于 Irql WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d9bcc852b2ee0921f2985c02f3778f91aeaaf21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522453"
---
# <a name="dispatch-routine-irql-and-thread-context"></a>调度例程 IRQL 和线程上下文


## <span id="ddk_dispatch_routine_irql_and_thread_context_if"></span><span id="DDK_DISPATCH_ROUTINE_IRQL_AND_THREAD_CONTEXT_IF"></span>


下表总结了文件系统筛选器驱动程序调度例程的 IRQL 和线程上下文要求。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">调度例程</th>
<th align="left">调用方&#39;s IRQL:</th>
<th align="left">调用方&#39;s 线程上下文：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Cleanup</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>关闭</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>DeviceControl （除分页 I/O）</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DeviceControl （分页 I/O 路径）</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectoryControl</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FlushBuffers</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>FsControl （除分页 I/O）</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FsControl （分页 I/O 路径）</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>LockControl</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PnP</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryEa</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>QueryInformation</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryQuota</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>QuerySecurity</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryVolumeInfo</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>读取 （除分页 I/O）</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>读取 （分页 I/O 路径）</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetEa</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>SetInformation</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetQuota</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>SetSecurity</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetVolumeInfo</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>关机</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>写入 （除分页 I/O）</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>写入 （分页 I/O 路径）</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
</tbody>
</table>

 

 

 




