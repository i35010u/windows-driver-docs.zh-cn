---
title: 调度例程 IRQL 和线程上下文
description: 调度例程 IRQL 和线程上下文
keywords:
- IRP 调度例程 WDK 文件系统，IRQL
- IRP 调度例程 WDK 文件系统，线程上下文
- nonarbitrary 线程上下文 WDK 文件系统
- 线程上下文 WDK 文件系统
- 任意线程上下文 WDK 文件系统
- IRQLs WDK 文件系统
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 90d836b936190e1a5d9386f9e1fe82e5d9e25c87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823227"
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
<th align="left">调用方的最大 IRQL：</th>
<th align="left">调用方的线程上下文：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>清理</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>关闭</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任一</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>DeviceControl (除分页 i/o) </p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DeviceControl (分页 i/o 路径) </p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任一</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectoryControl</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任一</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FlushBuffers</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>FsControl (除分页 i/o) </p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FsControl (分页 i/o 路径) </p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任一</p></td>
</tr>
<tr class="even">
<td align="left"><p>LockControl</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Pnp-x</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任一</p></td>
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
<td align="left"><p>读取 (除分页 i/o) </p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>读取 (分页 i/o 路径) </p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任一</p></td>
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
<td align="left"><p>任一</p></td>
</tr>
<tr class="odd">
<td align="left"><p>写入 (，分页 i/o) </p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>写入 (分页 i/o 路径) </p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任一</p></td>
</tr>
</tbody>
</table>

 

 

 




