---
title: 连接和名称解析
description: 连接和名称解析
ms.assetid: e61d09f1-7951-4291-93ce-e5ccbe0be576
keywords:
- 小型重定向程序 WDK，连接
- 小型重定向程序 WDK，名称解析
- 命名 WDK 文件系统
- 连接 WDK 微型重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00755c7c89b763faa837c27fde5b6928ef454f91
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841461"
---
# <a name="connection-and-name-resolution"></a>连接和名称解析


网络小型重定向器与远程服务器建立连接，并使用多个例程处理名称解析。 RDBSS 将此过程抽象化为多个结构，其中包括 SRV\_调用、NET\_ROOT 和 V\_NET\_引用计数的根结构。 在网络小型重定向器术语中，建立连接通常称为 "树连接"。 此连接建立需要创建 SRV\_调用、NET\_ROOT 和 V\_NET\_根结构。 因此，正常过程将是对网络微重定向程序[**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)例程的调用，接下来是对[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)和[**MRxCreateVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)例程的调用。 通常，这些调用用于响应来自用户模式应用程序或服务的请求，以装载驱动器（例如**net use x： \\\\服务器\\public**）。 这些调用也可能由对 UNC 文件对象（例如，**记事本 \\\\server\\公共\\readme.txt**）请求导致。 RDBSS 在内部处理网络微型重定向程序的这两种情况并启动**MRxCreateSrvCall**序列。

删除连接时，将发出类似的 finalize 调用来细分 SRV\_调用，NET\_根结构并释放使用的任何内存。 这些对网络小型重定向程序的调用包括[**MRxFinalizeVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)、 [**MRxFinalizeNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown)和[**MRxFinalizeSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)。

RDBSS 的原始设计是各种网络微重定向器都将共享 RDBSS 的单个副本，但这不是实现的。 此初始设计的一个 holdover 是，各种网络微型重定向器都在满足网络连接请求（例如\\\\服务器\\共享）的情况下进行争用。 RDBSS 使用[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)例程通知网络小型重定向程序，这是多个重定向程序可能满足请求时的入选方。 预期的网络微型重定向程序应创建 SRV\_调用，并建立与服务器的连接。

在 Windows Server 2003、Windows XP 和 Windows 2000 中的 RDBSS 实现下，每个网络小型重定向程序都有其自己的 RDBSS 副本，因此在 RDBSS 层没有争用的网络重定向程序。 每个网络小型重定向程序（网络提供程序）及其本地 RDBSS 的本地副本都是基于注册表设置中的顺序依次调用的：查询提供程序的顺序由以下注册表值控制：

```cpp
ProviderOrder
```

此注册表值位于以下注册表项下：

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)例程将在每次请求创建 SRV\_调用结构后调用。

下表列出了可由网络微型重定向程序为连接和名称解析操作实现的例程。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序创建 SRV_CALL 结构并建立与服务器的连接。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序创建 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extract_netroot_name" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extract_netroot_name)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序从给定路径名的 NET_ROOT 结构中提取名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序完成 NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器完成用于与服务器建立连接的 SRV_CALL 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序完成 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_preparse_name" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_preparse_name)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，为网络微重定向程序指定 preparse 名称的机会。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>此例程最初设计为由 RDBSS 调用，以便在多个重定向程序可能满足请求时通知网络小型重定向程序。 预期的网络微重定向器应创建 SRV_CALL 结构并建立与服务器的连接。</p>
<p>在 RDBSS 的当前实现下，每个网络微型重定向程序都有其自己的 RDBSS 副本，因此在 RDBSS 层没有争用的网络重定向器。 在每次请求创建 SRV_CALL 结构之前，将调用此例程。</p>
<p>如果安装了多个重定向程序来处理同一 UNC 命名空间，则 MUP 会根据注册表中指定的重定向程序的顺序来选择用于处理请求的重定向程序。</p></td>
</tr>
</tbody>
</table>

 

 

 




