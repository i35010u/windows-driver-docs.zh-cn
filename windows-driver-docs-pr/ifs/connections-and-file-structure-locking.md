---
title: 连接和文件结构锁定
description: 连接和文件结构锁定
keywords:
- 锁定 WDK RDBSS
- 每设备对象表 WDK RDBSS
- 排他锁 WDK RDBSS
- 引用计数 WDK RDBSS
- 每 NET_ROOT 表的结构 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9d631850ee1111cce631f9116fa8d753ad711f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789925"
---
# <a name="connections-and-file-structure-locking"></a>连接和文件结构锁定


## <span id="ddk_connections_and_file_structure_locking_if"></span><span id="DDK_CONNECTIONS_AND_FILE_STRUCTURE_LOCKING_IF"></span>


出于锁定目的，使用了两个级别的查找表：

-   用于 SRV 调用的每个设备对象表 \_ 和 \_ (前缀表的网络根结构) 

-   \_ (FCB 表的 FCB 结构的每网络根结构表) 

这些单独的表允许在建立连接后，对不同网络根结构的目录操作 \_ 几乎完全不会干扰。 但是，同一网络根结构上的目录操作会 \_ 略微干扰。 下表描述了特定操作所需的锁：

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
<th align="left">需要锁</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>创建或完成</p></td>
<td align="left"><p></p>
SRV_CALL NET_ROOT V_NET_ROOT</td>
<td align="left"><p>网络名称表的排他锁 (RxContext- &gt; RxDeviceObject-pRxNetNameTable) 的 TableLock 字段 &gt; 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>引用、取消引用或查找</p></td>
<td align="left"><p></p>
SRV_CALL NET_ROOT V_NET_ROOT</td>
<td align="left"><p>网络名称表上的共享锁或排他锁 (RxContext- &gt; RxDeviceObject-pRxNetNameTable) 的 TableLock 字段 &gt; 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建或完成</p></td>
<td align="left"><p></p>
FCB SRV_OPEN FOBX</td>
<td align="left"><p>FCB 表中的排他锁 (NET_ROOT-FcbTable) 的 TableLock 字段 &gt; 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>引用、取消引用或查找</p></td>
<td align="left"><p></p>
FCB SRV_OPEN FOBX</td>
<td align="left"><p>FCB 表上的共享锁或排他锁 (NET_ROOT-FcbTable) 的 TableLock 字段 &gt; 。</p></td>
</tr>
</tbody>
</table>

 

请注意，SRV \_ OPEN 和 FOBX 数据结构的操作当前要求 FCB 数据结构的操作所需的锁。 这只是一种节省内存的方法。 将来版本的 Windows 可以在 FCB 级别添加另一个资源以消除此限制，因此，可以使用一组共享资源将冲突的可能性降低到可接受的低级别。

如果需要两个锁 (FinalizeNetFcb，例如) ，必须首先对网络名称表执行锁定，然后对 FCB 表执行锁定。 您必须以相反顺序释放锁。

SRV \_ 调用、net \_ root 和 \_ net \_ root 创建和终止进程由对网络名称表上的 RDBSS 锁的获取和释放进行控制。

FCB 创建和终止过程由与 NET 根结构关联的网络名称表上的锁的获取和释放进行控制 \_ 。

FOBX 和 SRVOPEN 创建和终止过程由 FCB 表上的锁的获取和释放进行控制。

下表总结了在创建和终止各种数据结构时需要获取锁的锁和模式：

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
<th align="left">运算类型</th>
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
<td align="left"><p>网络名称表中的排他锁</p></td>
<td align="left"><p>网络名称表中的排他锁</p></td>
<td align="left"><p>FCB 表中的排他锁</p></td>
<td align="left"><p>FCB 表中的排他锁</p></td>
<td align="left"><p>FCB 表中的排他锁</p></td>
</tr>
<tr class="even">
<td align="left"><p>完成</p></td>
<td align="left"><p>网络名称表中的排他锁</p></td>
<td align="left"><p>网络名称表中的排他锁</p></td>
<td align="left"><p>FCB 表中的排他锁</p></td>
<td align="left"><p>FCB 表中的排他锁</p></td>
<td align="left"><p>FCB 表中的排他锁</p></td>
</tr>
</tbody>
</table>

 

引用和取消引用这些数据结构还必须遵守某些约定。

在大多数情况) 下，如果与任何数据结构相关联的引用计数降为1，则在大多数情况下， (由名称表保存的引用计数。 数据结构可以立即完成，也可以标记为要清理。 这两种方法都是在 RDBSS 中实现的。 如果在取消引用时满足锁定要求，数据结构将立即终止。 但这种情况的一个例外是，当实现了延迟操作优化时 (取消 FCB 结构的引用，例如) 。 否则，将数据结构标记为进行清理。

网络小型重定向程序应该对网络名称表具有排他锁，以便调用终止例程。

若要对其中一个数据结构执行创建操作，网络小型重定向程序驱动程序应执行类似于以下内容的操作：

```cpp
    getshared();lookup();
    if (failed) {
        release(); getexclusive(); lookup();
            if ((failed) { create(); }
        }
    deref();
    release();
```

成功获取锁定后，将节点插入到表中，释放锁定，然后查看服务器是否可用。 如果服务器可用，请设置其余信息并取消阻止正在等待同一服务器 (SRV \_ 调用或 NET \_ ROOT 结构) 的任何人。

 

 




