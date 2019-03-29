---
title: 连接和文件结构锁定
description: 连接和文件结构锁定
ms.assetid: 7286a34f-db8f-4b0a-ab7f-674b9dc641a8
keywords:
- 锁定 WDK RDBSS
- 每个设备对象表 WDK RDBSS
- WDK RDBSS 的排他锁
- 引用计数 WDK RDBSS
- 每个 NET_ROOT 表结构 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49485a815419be3905117e7bcc990bbb5e673902
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575748"
---
# <a name="connections-and-file-structure-locking"></a>连接和文件结构锁定


## <span id="ddk_connections_and_file_structure_locking_if"></span><span id="DDK_CONNECTIONS_AND_FILE_STRUCTURE_LOCKING_IF"></span>


为了进行锁定，有两个级别的查找表使用：

-   每个设备对象表以获取 SRV\_调用和 NET\_根结构 （前缀表）

-   表每个 NET\_FCB 结构 （FCB 表） 的根结构

这些单独的表允许不同的网络上的目录操作\_根结构几乎完全非干涉一旦建立连接。 同一网络上的目录操作\_根结构并影响略有不同，但是。 下表描述了对特定操作需要哪些锁：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">数据类型</th>
<th align="left">所需的锁</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>创建或完成</p></td>
<td align="left"><p></p>
SRV_CALL NET_ROOT V_NET_ROOT</td>
<td align="left"><p>NetName 表的排他锁 (RxContext-TableLock 字段&gt;RxDeviceObject-&gt;pRxNetNameTable)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>引用、 取消引用，或查找</p></td>
<td align="left"><p></p>
SRV_CALL NET_ROOT V_NET_ROOT</td>
<td align="left"><p>NetName 表的共享或排他锁 (RxContext-TableLock 字段&gt;RxDeviceObject-&gt;pRxNetNameTable)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建或完成</p></td>
<td align="left"><p></p>
FCB SRV_OPEN FOBX</td>
<td align="left"><p>FCB 表的排他锁 (NET_ROOT-TableLock 字段&gt;FcbTable)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>引用、 取消引用，或查找</p></td>
<td align="left"><p></p>
FCB SRV_OPEN FOBX</td>
<td align="left"><p>FCB 表的共享或排他锁 (NET_ROOT-TableLock 字段&gt;FcbTable)。</p></td>
</tr>
</tbody>
</table>

 

请注意该操作 SRV\_打开和 FOBX 数据结构目前需要同一个锁所需的操作的 FCB 数据结构。 这是只需保存想法的内存。 Windows 的未来版本可能会在要解除此限制，以便共享资源的一组可用于减少到可接受的低级别冲突的可能性的 FCB 级别添加另一个资源。

如果您需要同时锁 (FinalizeNetFcb，例如)，你必须获取锁，NetName 表第一，然后 FCB 表上的锁。 必须释放的锁以相反的顺序。

SRV\_调用时，NET\_根和 V\_NET\_根创建和终止过程所依据的获取和释放 NetName 表 RDBSS 锁定。

FCB 创建和终止过程所依据的获取和释放的 NET 与关联的网络名表上的锁\_根结构。

FOBX 和 SRVOPEN 创建和终止过程所依据的获取和释放 FCB 表上的锁。

下表总结了锁和锁需要获取用于创建和终止的各种数据结构的模式：

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作类型</th>
<th align="left">SRV_CALL</th>
<th align="left">NET_ROOT</th>
<th align="left">FCB</th>
<th align="left">SRV_OPEN</th>
<th align="left">FOBX</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>创建</p></td>
<td align="left"><p>NetName 表上的排他锁</p></td>
<td align="left"><p>NetName 表上的排他锁</p></td>
<td align="left"><p>FCB 表上的排他锁</p></td>
<td align="left"><p>FCB 表上的排他锁</p></td>
<td align="left"><p>FCB 表上的排他锁</p></td>
</tr>
<tr class="even">
<td align="left"><p>完成</p></td>
<td align="left"><p>NetName 表上的排他锁</p></td>
<td align="left"><p>NetName 表上的排他锁</p></td>
<td align="left"><p>FCB 表上的排他锁</p></td>
<td align="left"><p>FCB 表上的排他锁</p></td>
<td align="left"><p>FCB 表上的排他锁</p></td>
</tr>
</tbody>
</table>

 

必须遵循特定约定也引用并取消对这些数据结构的引用。

引用计数与任何数据结构关联的下降到 1 （正在挂起在大多数情况下的名称表的唯一引用），数据结构时，终止的潜在候选项。 可以立即或者完成的数据结构，否则它可以标记为清理。 这两种方法是在 RDBSS 中实现的。 在取消引用期间满足锁定要求，可以立即最终完成的数据结构。 一个例外是当延迟操作优化实现 （例如取消 FCB 结构）。 否则，数据结构标记为要清理的时间。

网络微型重定向应 NetName 表具有排他锁，才能调用的终止例程。

若要执行这些数据结构之一上创建，网络微型重定向程序驱动程序应执行类似于以下内容：

```cpp
    getshared();lookup();
    if (failed) {
        release(); getexclusive(); lookup();
            if ((failed) { create(); }
        }
    deref();
    release();
```

时已成功获得锁，将节点插入到表、 释放锁，并查看该服务器是否可用。 如果该服务器是否可用，设置的其他信息和取消阻止正在等待在同一服务器上的任何人 (SRV\_调用或 NET\_根结构)。

 

 




