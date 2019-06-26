---
title: 多路复用 ID 管理
description: 多路复用 ID 管理
ms.assetid: feffc421-bd51-4174-80a4-1f9a36355667
keywords:
- RDBSS WDK 的文件系统进行多路复用 ID
- 重定向驱动器缓冲子系统 WDK 的文件系统进行多路复用 ID
- 多路复用 ID WDK 网络重定向程序
- MID WDK 网络重定向程序
- 映射 MID
- MID_ATLAS 结构
- MID_MAP 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcad2321ab6254231361170c0dbc54c74bd92a84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383864"
---
# <a name="multiplex-id-management"></a>多路复用 ID 管理


## <span id="ddk_multiplex_id_management_if"></span><span id="DDK_MULTIPLEX_ID_MANAGEMENT_IF"></span>


RDBSS 定义 multiplex ID (MID)，一个 16 位值，它可用于通过网络客户端 （最小-重定向程序） 和服务器之间的任何连接上的并发活动请求区分开来。 网络重定向程序可以将 MID 与任何任意上下文或它使用的内部数据结构相关联。 它位于完全的网络重定向程序选项 MIDs 是否分配和使用。

MID、 规定的 RDBSS，属于 MID\_ATLAS 数据结构，旨在满足多个条件。 与 MID\_ATLAS 数据结构是一系列一个或多个 MID\_映射用来将 MIDs 映射到关联的上下文数据结构。

MID\_ATLAS 数据结构，MID\_映射结构和 MIDs 应缩放以处理多个远程服务器的不同功能。 例如，在 Windows 上的典型 LAN 管理器服务器上的任何连接允许 50 个未完成请求。 网关服务器可能需要此编号，以很高 （大约成千上万的未完成的连接） 时，某些类型的服务器可能支持只一个未处理的请求。

需要进行还处理的两个主要操作包括：

-   将 MID 映射到与它关联的上下文。 将调用此例程来处理任何连接在客户端和服务器 （假设，服务器使用 MIDs） 沿接收到的每个数据包。

-   生成新 MID 将请求发送到服务器。 此例程将在客户端使用的强制的最大连接限制也与标记具有一个唯一 id。 每个并发请求

MID 必须能够有效地从 65,536 值的可能组合管理唯一标记和 MIDs (通常为 50) 的数字标识。 在某些情况下，它可能会有用来创建小型 MID\_ATLAS 结构保存 MID 所使用的内核内存\_映射结构并将扩展大小 MID\_ATLAS 结构根据需要来有效地处理更高版本的使用情况。 若要确保正确的时间空间权衡，查找被组织成三层层次结构。 用于表示 MID 16 位分为三位域。 （最不重要） 的最右侧的字段的长度由 MIDs 初始 atlas 中允许的最大数目决定。 此最大值是一个参数传递给[ **RxCreateMidAtlas** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas)例程时 MID\_首次创建 ATLAS 数据结构。 此最大值确定的初始大小 MID\_ATLAS 创建的数据结构和多少 MID\_可以容纳映射数据结构。 剩下的长度拆分同样在接下来两个字段，确定可能的从属 MID 的最大大小间\_ATLAS 结构可以定义可展开和扩展现有 MID\_ATLAS 成一个三级层次结构的 MID\_映射数据结构。 因此，每个 MID\_ATLAS 数据结构可以包含最大数量的 MID\_映射结构或指向一个从属 MID\_ATLAS 和 MID\_映射结构。

例如，如果创建时分配最多为 50 MIDs，第一个字段的长度为 6 (64 (2 \* \* 6) 大于 50)。 剩下的长度被分为 5 位的每个第二个和第三个层次结构级别的两个字段因此的现有 MID\_ATLAS 数据结构可以扩展以容纳更多 MID\_映射条目。

RDBSS 提供了用于创建和操作 MID 下面的例程\_ATLAS 数据结构，关联 MID\_映射数据结构和多路复用 Id。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>此例程将提供的不透明上下文与从 MID_ATLAS 结构可用 MID 相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>此例程分配 MID_ATLAS 数据结构的新实例并初始化它。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>此例程销毁 MID_ATLAS 数据结构的现有实例，并释放分配给它的内存。 副作用是它会调用传递上下文析构函数上 MID_ATLAS 结构中每个有效的上下文中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>此例程会映射到在 MID_ATLAS 结构及其关联的上下文 MID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>此例程将 MID 映射到 MID_ATLAS 结构中其关联的上下文，并取消从上下文 MID 然后关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>此例程重新 MID 关联与备用的上下文。</p></td>
</tr>
</tbody>
</table>

 

 

 




