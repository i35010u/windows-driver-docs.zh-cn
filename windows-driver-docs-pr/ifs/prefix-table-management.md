---
title: 前缀表管理
description: 前缀表管理
ms.assetid: a48ed460-fab9-4a6d-bd2f-454b4932ea61
keywords:
- RDBSS WDK 的文件系统，前缀表
- 重定向驱动器缓冲子系统 WDK 的文件系统，前缀表
- 前缀表 WDK 网络重定向程序
- 名称 WDK RDBSS
- 版本戳 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3ed821f8a96c0d0f1c674f6990d722084fd6d76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385163"
---
# <a name="prefix-table-management"></a>前缀表管理


## <span id="ddk_prefix_table_management_if"></span><span id="DDK_PREFIX_TABLE_MANAGEMENT_IF"></span>


RDBSS 定义数据结构，使用的前缀表到编录 SRV\_调用时，NET\_根和 V\_NET\_根名称。

名称中的管理的 RDBSS 的当前实现将表具有以下组件：

-   插入名称的一个队列

-   版本标记

-   表锁资源，用于控制表的访问

-   一个值，指示是否不区分大小写名称的匹配项

-   为此前缀表的哈希值项的存储桶

以正常方式使用表锁资源： 共享的查找操作时，独有的更改操作。

版本戳更改，并每次更改。 队列的原因是前缀表包允许多个调用方枚举一次。 插入的名称和版本戳记的队列允许多个调用方同时枚举。 队列可用于为速度更快查找文件的名称，但前缀表肯定是 NET 的正确方法\_根结构。

这些前缀表管理例程中的使用在内部 RDBSS MUP 从响应的调用来声明一个名称，或以形成网络的创建路径\_根结构。 这些 RDBSS 前缀表管理例程可也由网络微型-重定向程序，只要访问表之前获取适当的锁和锁被释放时已完成工作。 由驱动程序正常使用将按如下所示：

-   通过调用获取共享的锁**RxAcquirePrefixTableLockShared**。

-   查找名称通过调用[ **RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname)。

-   通过调用释放共享的锁**RxReleasePrefixTableLock**。

请注意，仅在 Windows XP 和早期版本的 Windows 上实现某些例程。 [**RxPrefixTableLookupName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname)是所有版本的 Windows 上实现的唯一前缀表管理例程

RDBSS 前缀表管理例程包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockexclusive" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockexclusive)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>此例程将获取对目录 SRV_CALL 和 NET_ROOT 名称所用的前缀表的排他锁。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockshared" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockshared)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>此例程将获取对目录 SRV_CALL 和 NET_ROOT 名称所用的前缀表上的共享的锁。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>例程查找到目录 SRV_CALL 所用的前缀表中的名称和 NET_ROOT 名称，并将从基础指针转换为包含结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpreleaseprefixtablelock" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpreleaseprefixtablelock)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>此例程释放对目录 SRV_CALL 和 NET_ROOT 名称所用的前缀表上的锁。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
</tbody>
</table>

 

从 Windows Server 2003 开始上, 表中所述例程除外[ **RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname)，替换为宏。以下宏的定义，调用表例程参数较少的前缀。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>TABLE</em>, <em>WAIT</em>)</p></td>
<td align="left"><p>此宏获取独占模式下更改操作为该前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>表</em>，<em>等待</em>)</p></td>
<td align="left"><p>此宏获取前缀表锁在共享模式下的查找操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>此宏指示是否在独占或共享模式下获取前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>此宏指示是否以独占方式获取前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>此宏可释放前缀表锁。</p></td>
</tr>
</tbody>
</table>

 

 

 




