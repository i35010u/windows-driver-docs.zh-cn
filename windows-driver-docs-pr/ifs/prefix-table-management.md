---
title: 前缀表管理
description: 前缀表管理
ms.assetid: a48ed460-fab9-4a6d-bd2f-454b4932ea61
keywords:
- RDBSS WDK 文件系统，前缀表
- 重定向驱动器缓冲子系统 WDK 文件系统，前缀表
- 前缀表 WDK 网络重定向器
- 命名 WDK RDBSS
- 版本戳记 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42d6a1ea66d365dc6c0d2062cf324125a8b4fbd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841029"
---
# <a name="prefix-table-management"></a>前缀表管理


## <span id="ddk_prefix_table_management_if"></span><span id="DDK_PREFIX_TABLE_MANAGEMENT_IF"></span>


RDBSS 定义数据结构，这些结构允许使用前缀表来目录 SRV\_调用、NET\_ROOT 和 V\_NET\_根名称。

RDBSS 中的名称管理的当前实现使用具有以下组件的表：

-   插入的名称的队列

-   版本标记

-   控制表访问权限的表锁资源

-   一个值，该值指示名称是否匹配不区分大小写

-   此前缀表的哈希值项的存储桶

表锁资源的使用方式如下：用于查找操作的共享，用于进行更改操作。

每次发生更改时，版本标记都会发生变化。 队列的原因是前缀表包允许一次枚举多个调用方。 插入的名称和版本戳记的队列允许同时枚举多个调用方。 队列可用作文件名的更快查找，但前缀表确实是用于 NET\_根结构的正确方法。

这些前缀表管理例程由 RDBSS 在内部使用，以响应 MUP 发出的调用，以声明名称或形成 NET\_根结构的创建路径。 这些 RDBSS 前缀表管理例程还可以由网络小型重定向程序使用，前提是在访问表之前获取适当的锁，并且在工作完成时释放锁。 驱动程序的正常使用情况如下所示：

-   通过调用**RxAcquirePrefixTableLockShared**获取共享锁。

-   通过调用[**RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)查找名称。

-   通过调用**RxReleasePrefixTableLock**释放共享锁。

请注意，某些例程仅在 Windows XP 和早期版本的 Windows 上实现。 [**RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)是在所有版本的 Windows 上实现的唯一前缀表管理例程

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>此例程获取用于对 SRV_CALL 和 NET_ROOT 名称进行分类的前缀表的排他锁。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>此例程获取用于对 SRV_CALL 和 NET_ROOT 名称进行分类的前缀表上的共享锁。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>例程在前缀表中查找用于对 SRV_CALL 和 NET_ROOT 名称进行分类的名称，并将基础指针转换为包含结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>此例程释放用于对 SRV_CALL 和 NET_ROOT 名称进行分类的前缀表上的锁。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
</tbody>
</table>

 

从 Windows Server 2003 开始，上表中提到的例程（ [**RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)除外）会被宏替换。定义了下列宏，用于调用具有较少参数的前缀表例程。

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
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> （<em>表</em>，<em>等待</em>）</p></td>
<td align="left"><p>此宏获取用于更改操作的独占模式下的前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> （<em>表</em>，<em>等待</em>）</p></td>
<td align="left"><p>此宏获取用于查找操作的共享模式下的前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> （<em>表</em>）</p></td>
<td align="left"><p>此宏指示在独占或共享模式下是否获取了前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> （<em>表</em>）</p></td>
<td align="left"><p>此宏指示是否以独占模式获取了前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> （<em>表</em>）</p></td>
<td align="left"><p>此宏释放前缀表锁。</p></td>
</tr>
</tbody>
</table>

 

 

 




