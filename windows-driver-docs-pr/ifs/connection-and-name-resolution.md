---
title: 连接和名称解析
description: 连接和名称解析
ms.assetid: e61d09f1-7951-4291-93ce-e5ccbe0be576
keywords:
- 最小重定向程序 WDK，连接
- 最小重定向程序 WDK、 名称解析
- 名称 WDK 文件系统
- 连接 WDK 微型-重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08a0ef58bcf2b978e8e4444187c33cba4db00768
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378985"
---
# <a name="connection-and-name-resolution"></a>连接和名称解析


网络微型-重定向程序建立与远程服务器连接和处理使用多个例程的名称解析。 RDBSS 将此进程抽象化为多个结构包括 SRV\_调用时，NET\_根和 V\_NET\_根结构的引用计数。 在网络微型重定向术语中，建立连接通常称为"树连接。" 建立此连接需要创建 SRV\_调用、 NET\_根和 V\_NET\_根结构。 正常的过程不会对网络微型重定向的调用以便[ **MRxCreateSrvCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall)例程通过调用后接[ **MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)并[ **MRxCreateVNetRoot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root)例程。 这些调用通常来自要装载驱动器的用户模式应用程序或服务的请求响应中发出 (**使用 x:，net \\\\服务器\\公共**，例如)。 这些调用也可能来自 UNC 文件对象的请求 (**记事本\\\\服务器\\公共\\readme.txt**，例如)。 RDBSS 处理这两种情况在内部的网络微型重定向，并启动**MRxCreateSrvCall**序列。

连接时已删除，类似完成调用都是关闭 SRV\_调用时，并 NET\_根结构并释放任何内存使用。 网络微型重定向到这些调用包括[ **MRxFinalizeVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)， [ **MRxFinalizeNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown)，和[**MRxFinalizeSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)。

RDBSS 的原始设计是各种网络微型重定向将共享的 RDBSS，单个副本，但没有实施此功能。 从该原始设计遗留是各种网络微型重定向争用来满足网络连接的请求 (\\\\server\\共享，例如)。 [ **MRxSrvCallWinnerNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify) RDBSS 使用例程，它是获胜者，当多个重定向程序无法完成请求时通知网络微型重定向。 入选网络的微型重定向需要创建 SRV\_调用并建立与服务器的连接。

下 RDBSS 在 Windows Server 2003、 Windows XP 和 Windows 2000 中实现时，每个网络微型重定向有其自己的 RDBSS 副本，因此在 RDBSS 层包含任何竞争的网络重定向程序。 每个网络微型重定向 （网络提供商） 以及其 RDBSS 的本地副本被称为反过来基于注册表设置中的顺序：在其中查询提供程序的顺序由以下注册表值控制：

```cpp
ProviderOrder
```

此注册表值位于以下注册表项下：

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

[ **MRxSrvCallWinnerNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)例程将在调用完每个请求创建 SRV\_调用结构。

下表列出了可以由网络微型重定向的连接和名称解析操作的例程。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建 SRV_CALL 结构并与服务器建立连接。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extract_netroot_name" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extract_netroot_name)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向从给定的路径名称 NET_ROOT 结构提取的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成 NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成用于建立与服务器连接的 SRV_CALL 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_preparse_name" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_preparse_name)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以使网络微型重定向有机会 preparse 一个名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>此例程最初设计用于由 RDBSS 以通知网络微型重定向，它是获胜者，当多个重定向程序无法完成请求时调用。 入选网络的微型重定向需要创建 SRV_CALL 结构并建立与服务器的连接。</p>
<p>下 RDBSS 的当前实现每个网络微型重定向有其自己的 RDBSS，副本，因此在 RDBSS 层包含任何竞争的网络重定向程序。 此例程将在创建 SRV_CALL 结构的每个请求之前调用。</p>
<p>如果多个重定向程序安装为处理同一个 UNC 命名空间中，MUP 基于重定向程序在注册表中指定的顺序选择重定向程序若要为请求提供服务。</p></td>
</tr>
</tbody>
</table>

 

 

 




