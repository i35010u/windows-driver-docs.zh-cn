---
title: 多路复用 ID 管理
description: 多路复用 ID 管理
ms.assetid: feffc421-bd51-4174-80a4-1f9a36355667
keywords:
- RDBSS WDK 文件系统，多路复用 ID
- 重定向驱动器缓冲子系统 WDK 文件系统，多路复用 ID
- 多路复用 ID WDK 网络重定向器
- 中间的 WDK 网络重定向器
- 中间映射
- MID_ATLAS 结构
- MID_MAP 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc73f78a61b1058d87f65020ff4b3eb8195f46e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841061"
---
# <a name="multiplex-id-management"></a>多路复用 ID 管理


## <span id="ddk_multiplex_id_management_if"></span><span id="DDK_MULTIPLEX_ID_MANAGEMENT_IF"></span>


RDBSS 定义了一个多路复用 ID （MID），这是一个16位值，网络客户端（最小化重定向程序）和服务器可以使用该 ID 来区分对任何连接的并发活动请求。 网络重定向程序可以将中间与任何任意上下文或它使用的内部数据结构相关联。 它完全是网络重定向器的选项，无论是否分配并使用 MIDs。

RDBSS 定义的中端是设计为满足若干标准的 MID\_阿特拉斯数据结构的一部分。 与中型\_阿特拉斯数据结构相关联的是一个或多个 MID\_映射数据结构，用于将 MIDs 映射到关联的上下文。

MID\_阿特拉斯数据结构、中\_地图结构和 MIDs 应该可以很好地进行缩放，以处理各种远程服务器的不同功能。 例如，Windows 上的典型 LAN 管理器服务器允许在任何连接上进行50未处理的请求。 某些类型的服务器可能仅支持一个未完成的请求，而网关服务器可能希望此数字非常高（按上千个未完成连接的顺序）。

需要处理的两个主要操作是：

-   将 MID 映射到与其关联的上下文。 将调用此例程来处理客户端和服务器上的任何连接所接收的每个数据包（假设服务器使用 MIDs）。

-   正在生成将请求发送到服务器的新 MID。 将在客户端上使用此例程来强制执行最大连接限制，并使用唯一 ID 标记每个并发请求。

MID 必须能够有效地管理多个 MIDs （通常为50）的唯一标记和标识，这可能是65536值的组合。 在某些情况下，如果需要有效地处理更大的使用量，可以创建一个小型的中\_阿特拉斯结构来保存中型\_地图结构使用的内核内存，并扩展中间\_阿特拉斯结构的大小。 为了确保适当的时间间隔，查找被组织为三级层次结构。 用于表示 MID 的16位分为三个位域。 最右侧字段的长度（最不重要）由初始阿特拉斯中允许的最大 MIDs 数决定。 当首次创建\_阿特拉斯数据结构时，此最大值是传递到[**RxCreateMidAtlas**](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)例程的参数。 此最大值决定了开始\_阿特拉斯数据结构的初始大小，以及可以容纳多少个 MID\_地图数据结构。 剩余的长度平均拆分到接下来的两个字段中，这确定了可能的下级中间\_阿特拉斯结构的最大大小，可以定义该结构以将现有的中端\_\_映射数据结构。 因此，每个 MID\_阿特拉斯数据结构都可以包含\_地图结构的最大数目，或指向一个下属\_\_

例如，如果在创建时分配的最大值为 50 MIDs，则第一个字段的长度为6（64（2 \*\* 6）大于50）。 对于第二层和第三级层次结构，剩余长度分为5位的两个字段，以便可以\_扩展现有的中\_

RDBSS 提供以下例程用于创建和操作 MID\_阿特拉斯数据结构、关联的中端\_地图数据结构和多路复用 Id。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>此例程将提供的不透明上下文与 MID_ATLAS 结构中的可用 MID 关联起来。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>此例程分配 MID_ATLAS 数据结构的新实例，并对其进行初始化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>此例程销毁 MID_ATLAS 数据结构的现有实例，并释放分配给它的内存。 作为副作用，它会调用 MID_ATLAS 结构中的每个有效上下文的上下文析构函数中传递的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>此例程将 MID 映射到 MID_ATLAS 结构中与其关联的上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>此例程将 MID 映射到 MID_ATLAS 结构中与其关联的上下文，然后将中间与上下文解除关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>此例程通过备用上下文将了中间。</p></td>
</tr>
</tbody>
</table>

 

 

 




