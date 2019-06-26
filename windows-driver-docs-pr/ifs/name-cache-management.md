---
title: 名称缓存管理
description: 名称缓存管理
ms.assetid: 3e1b1419-320e-44e0-a6c2-823517cf07c7
keywords:
- RDBSS WDK 文件系统中，名称缓存
- 重定向驱动器缓冲子系统 WDK 文件系统中，名称缓存
- NAME_CACHE 结构
- 名称 WDK RDBSS
- 缓存 WDK RDBSS
- 找不到消息 WDK RDBSS 文件
- 命名缓存 WDK RDBSS
- NAME_CACHE_CONTROL 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e5b965feb362a6b3ca611a4e55341b5c1b90aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386072"
---
# <a name="name-cache-management"></a>名称缓存管理


## <span id="ddk_name_cache_management_if"></span><span id="DDK_NAME_CACHE_MANAGEMENT_IF"></span>


名称\_缓存结构缓存在服务器上执行，因此，客户端可以禁止显示冗余请求的最近操作的名称字符串。 例如，如果最近打开的请求失败，"找不到文件"消息客户端应用程序会尝试使用的大写字符串，再次打开请求和网络微型重定向不支持区分大小写的名称，RDBSS 可以失败请求立即而不会达到服务器。

一般情况下，该算法是将时间窗口和操作计数限制放名称\_缓存项。 时间窗口通常为两秒。 因此，如果名称\_缓存项大于两秒，则匹配将失败，请求将转到服务器。 请求再次失败在服务器上，名称\_与另一个两秒窗口更新缓存条目。 如果请求操作计数不匹配，则一个或多个请求已发送到服务器，这可能使此名称\_缓存条目无效。 同样，此操作将发送到服务器。

一个名称\_缓存结构具有网络微型重定向，MRX 向公开的公共部分\_名称\_缓存，并以仅供 RDBSS 私有部分。 最小重定向程序部分具有可以共同分配名称与一些其他微型重定向特定存储此名称项和上下文扩展指针上以前的服务器操作的结果的上下文字段 NTSTATUS，\_缓存结构。 有关详细信息，请参阅[ **RxNameCacheInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheinitialize)。

Windows 网络的 SMB 操作计数是未能 MRX 的上下文字段中保存的最小重定向程序特定状态的一个示例\_名称\_缓存。 当[ **RxNameCacheCheckEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecheckentry)是调用，它将执行上下文字段和名称缓存中查找匹配项的一部分提供的参数之间的相等性检查。 当名称\_创建或更新缓存条目，它是网络微型重定向的作业，以秒为单位的名称中提供适当的值为此字段和生存期，\_缓存项。

名称的专用 RDBSS 部分\_缓存结构包含名称为 Unicode 字符串，哈希值的速度查找名称的项，而一个标志，指示服务器是否支持区分大小写名称的到期时间。

名称\_缓存\_控制结构管理给定名称缓存。 它具有空闲列表、 活动的列表中和使用锁来同步更新。 名称\_缓存\_控制结构还具有字段来存储当前的名称数\_分配的缓存项，并将其分配的任何其他大小的最大项数的值为每个名称使用的网络微型重定向存储\_缓存项和值的统计信息 （已更新的缓存，次数选中时，返回有效的匹配项，并在网络的最小-重定向程序保存网络操作）。 **MaximumEntries**字段限制的名称数\_性能不佳计划的情况下创建的缓存条目已生成大量的打开请求的占用大量内存的错误的文件名称。

当前有名称缓存维护的对象的 RDBSS\_名称\_不\_找到。 为此名称缓存中，两个第二个窗口会保留，这失效的任何操作发送到服务器。 这可能发生客户端应用程序具有一个文件 (sample1) 时，可以使用在服务器上的应用程序发出信号的另一个文件 (sample2) 创建的服务器上打开。 当客户端读取的第一个文件 (sample1)，并了解已在服务器上创建第二个文件 (sample2) 时，第二个文件 (sample2) 匹配的名称缓存中命中不能返回一个错误。 这种优化仅处理对尚不存在的相同文件的连续文件打开操作的情况。 发生这种情况的使用 Microsoft Word。

RDBSS 名称缓存管理例程包括：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheactivateentry" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheactivateentry)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>此例程采用名称缓存项，并更新的到期时间和网络微型重定向程序上下文。 然后将该条目放在活动的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecheckentry" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecheckentry)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>此例程将检查有效性的 NAME_CACHE 条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecreateentry" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecreateentry)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>此例程分配并初始化具有给定名称字符串的 NAME_CACHE 结构。 应调用方将然后初始化的任何其他网络微型重定向程序元素的名称缓存上下文，然后将条目放在名称缓存活动列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentry" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentry)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>此例程将 NAME_CACHE 条目置于空闲列表上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentrywithshortname" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentrywithshortname)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>此例程将过期的所有 NAME_CACHE 条目其名称前缀匹配给定的短文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefetchentry" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefetchentry)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>此例程中查找匹配项替换为 NAME_CACHE 条目指定的名称字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefinalize" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefinalize)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>此例程将释放所有 NAME_CACHE 条目与 NAME_CACHE_CONTROL 结构相关联的存储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefreeentry" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefreeentry)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>此例程释放 NAME_CACHE 项存储并递减的 NAME_CACHE 计数缓存条目与 NAME_CACHE_CONTROL 结构相关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheinitialize" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheinitialize)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>此例程初始化名称缓存 （NAME_CACHE_CONTROL 结构）。</p></td>
</tr>
</tbody>
</table>

 

 

 




