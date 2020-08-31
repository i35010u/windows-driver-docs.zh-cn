---
title: 名称缓存管理
description: 名称缓存管理
ms.assetid: 3e1b1419-320e-44e0-a6c2-823517cf07c7
keywords:
- RDBSS WDK 文件系统，名称缓存
- 重定向的驱动器缓冲子系统 WDK 文件系统，名称缓存
- NAME_CACHE 结构
- 命名 WDK RDBSS
- 缓存 WDK RDBSS
- "\"找不到文件\" 消息 WDK RDBSS"
- 名称缓存 WDK RDBSS
- NAME_CACHE_CONTROL 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd4e8668632689027e93199ca12549fd7d49be77
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066886"
---
# <a name="name-cache-management"></a>名称缓存管理


## <span id="ddk_name_cache_management_if"></span><span id="DDK_NAME_CACHE_MANAGEMENT_IF"></span>


名称 \_ 缓存结构缓存在服务器上执行的最近操作的名称字符串，以便客户端可以取消冗余请求。 例如，如果一个打开请求最近失败了 "找不到文件" 消息，并且客户端应用程序使用大写的字符串再次尝试打开请求，而网络小型重定向程序不支持区分大小写的名称，则 RDBSS 会立即导致请求失败，而不会命中服务器。

通常，算法是在名称缓存条目上放置时间窗口和操作计数限制 \_ 。 时间窗口通常为两秒。 因此，如果名称 \_ 缓存项大于两秒钟，则匹配将失败，请求将发送到服务器。 如果请求在服务器上再次失败，则 \_ 会用另一个两秒钟的窗口更新名称缓存条目。 如果请求操作计数不匹配，则已将一个或多个请求发送到服务器，这可能会使此名称 \_ 缓存条目无效。 同样，此操作将发送到服务器。

名称 \_ 缓存结构具有公开给网络小型重定向程序、MRX 名称缓存的公共部分， \_ \_ 以及仅供 RDBSS 使用的专用部分。 小型重定向器部分为此名称项上的服务器操作的结果提供了一个上下文字段 NTSTATUS，并为一些其他微型重定向程序特定的存储提供了一个上下文扩展指针，这些存储可以与名称 \_ 缓存结构共同分配。 有关详细信息，请参阅 [**RxNameCacheInitialize**](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize)。

对于 Windows 网络，SMB 操作计数是特定于微型操作程序的状态的一个示例，可将其保存在 MRX 名称缓存的上下文字段 \_ 中 \_ 。 调用 [**RxNameCacheCheckEntry**](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry) 时，它将在上下文字段与提供的参数之间执行相等性检查，作为在名称缓存中查找匹配项的一部分。 当 \_ 创建或更新名称缓存条目时，它是网络小型重定向器的作业，为该字段提供相应的值，并为名称缓存条目提供生存期（以秒为单位） \_ 。

名称缓存结构的 private RDBSS 部分 \_ 包含 Unicode 字符串的名称、要加速查找的名称哈希值、条目的过期时间和指示服务器是否支持区分大小写的名称的标志。

名称 \_ 缓存 \_ 控制结构管理给定的名称缓存。 它有一个可用列表、一个活动列表和一个同步更新的锁。 名称 \_ 缓存 \_ 控制结构还包含用于存储所分配的当前名称缓存条目数的字段。 \_ 要分配的最大条目数的值、用于每个名称缓存条目的任何额外的网络微型重定向程序存储的大小 \_ ，以及用于统计信息的值 (缓存的更新时间、已选中、返回的有效匹配项以及网络小型重定向程序保存网络操作) 。 **MaximumEntries** \_ 当性能不佳的程序生成大量具有使用大量内存的错误文件名的打开请求时，MaximumEntries 字段会限制创建的名称缓存条目数。

当前未找到对象名称的 RDBSS 维护的名称 \_ 缓存 \_ \_ 。 对于此名称缓存，将维护两秒钟的窗口，如果将任何操作发送到服务器，则该窗口将会失效。 当客户端应用程序具有一个 (sample1) 打开的文件时，服务器上的应用程序可以使用该文件来向服务器上的 sample2) 的 (创建发出信号，这可能会发生这种情况。 当客户端读取第一个文件 (sample1) 并了解已在服务器上创建了第二个文件 (sample2) 后，与第二个文件 (sample2) 匹配的名称缓存中的命中将无法返回错误。 此优化仅处理同一个文件中不存在的连续文件打开操作的情况。 使用 Microsoft Word 时，会发生这种情况。

RDBSS 名称缓存管理例程包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>此例程采用名称缓存条目，并更新过期时间和网络小型重定向程序上下文。 然后，它会将该条目置于活动列表中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>此例程检查 NAME_CACHE 项的有效性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>此例程分配并初始化具有给定名称字符串的 NAME_CACHE 结构。 预计调用方将初始化名称缓存上下文的任何其他网络微重定向器元素，然后将该条目放入 "名称缓存活动" 列表中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>此例程为可用列表中的 NAME_CACHE 条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>此例程会使名称前缀与给定短文件名匹配的所有 NAME_CACHE 项过期。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>此例程查找 NAME_CACHE 条目的指定名称字符串匹配项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>此例程将释放与 NAME_CACHE_CONTROL 结构关联的所有 NAME_CACHE 项的存储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>此例程会释放 NAME_CACHE 项的存储并减少与 NAME_CACHE_CONTROL 结构关联的 NAME_CACHE 缓存项的计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>此例程 NAME_CACHE_CONTROL 结构)  (初始化名称缓存。</p></td>
</tr>
</tbody>
</table>

 

 

