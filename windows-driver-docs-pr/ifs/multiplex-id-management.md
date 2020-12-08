---
title: 多路复用 ID 管理
description: 多路复用 ID 管理
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
ms.openlocfilehash: 6b14a8ef5459935a81a76497a52171c15d75677a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831449"
---
# <a name="multiplex-id-management"></a>多路复用 ID 管理


## <span id="ddk_multiplex_id_management_if"></span><span id="DDK_MULTIPLEX_ID_MANAGEMENT_IF"></span>


RDBSS 定义一个多路复用 ID (中间) （一个16位值），网络客户端可以使用该 ID 来 (最小化重定向程序) 和服务器，以区分任意连接上的并发活动请求。 网络重定向程序可以将中间与任何任意上下文或它使用的内部数据结构相关联。 它完全是网络重定向器的选项，无论是否分配并使用 MIDs。

RDBSS 定义的中端是用于 \_ 满足多个条件的 mid 数据结构的一部分。 与中端数据结构关联的是一 \_ 系列 \_ 用于将 MIDs 映射到关联上下文的中端地图数据结构。

MID \_ 图的数据结构、中 \_ 图结构和 MIDs 应该可以很好地进行缩放，以处理各种远程服务器的不同功能。 例如，Windows 上的典型 LAN 管理器服务器允许在任何连接上进行50未处理的请求。 某些类型的服务器可能仅支持一个未完成的请求，而网关服务器可能希望此数字 (，以) 成千上万个未完成的连接。

需要处理的两个主要操作是：

-   将 MID 映射到与其关联的上下文。 将调用此例程来处理客户端和服务器上的任何连接所接收的每个数据包 (假定服务器使用 MIDs) 。

-   正在生成将请求发送到服务器的新 MID。 将在客户端上使用此例程来强制执行最大连接限制，并使用唯一 ID 标记每个并发请求。

MID 必须能够有效地管理多个 MIDs 的唯一标记和标识， (通常是 50) ，从65536值的可能组合。 在某些情况下，如果需要有效地处理更高的使用情况，可以创建一个小型的中端结构图 \_ 结构来保存中间图结构使用的内核内存 \_ ，并扩展中间的图结构的大小 \_ 。 为了确保适当的时间间隔，查找被组织为三级层次结构。 用于表示 MID 的16位分为三个位域。 最右侧字段 (最小重要 ) 的长度由初始阿特拉斯中允许的最大 MIDs 数决定。 当 [**RxCreateMidAtlas**](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas) \_ 第一次创建 MID 数据结构时，此最大值是传递到 RxCreateMidAtlas 例程的参数。 此最大值决定了所创建的中端 \_ 和地图数据结构的初始大小 \_ 。 剩余的长度平均拆分到接下来的两个字段中，这会确定可能的从属中端阿特拉斯结构的最大大小， \_ 可以定义该结构以将现有的中 \_ 端 \_ 因此，每个中端 \_ 图数据结构都可以包含最大的中 \_ 图结构数，或指向一个从中到的中点 \_ 和中 \_ 图结构的指针。

例如，如果在创建时分配的最大值为 50 MIDs，则第一个字段的长度为 6 (64 ( 2 \* \* 6 ) 大于 50 ) 。 对于第二层和第三级层次结构，剩余长度拆分为5位的两个字段，以便 \_ 可以扩展现有的 \_

RDBSS 提供了以下例程，用于创建和操作 MID \_ 数据结构、关联的中端 \_ 地图数据结构和多路复用 id。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>此例程将提供的不透明上下文与 MID_ATLAS 结构中的可用 MID 关联起来。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>此例程分配 MID_ATLAS 数据结构的新实例，并对其进行初始化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>此例程销毁 MID_ATLAS 数据结构的现有实例，并释放分配给它的内存。 作为副作用，它会调用 MID_ATLAS 结构的每个有效上下文的上下文析构函数中传递的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>此例程在 MID_ATLAS 结构中将 MID 映射到其关联的上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>此例程在 MID_ATLAS 结构中将 MID 映射到其关联的上下文，然后将中间与上下文解除关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>此例程通过备用上下文将了中间。</p></td>
</tr>
</tbody>
</table>

 

