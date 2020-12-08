---
title: Hyper-V 可扩展交换机发送和接收操作
description: Hyper-V 可扩展交换机发送和接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4346ef01e37a19dcd11bc67f8cad74d2dcdaaf90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794508"
---
# <a name="hyper-v-extensible-switch-send-and-receive-operations"></a>Hyper-V 可扩展交换机发送和接收操作


本部分介绍 Hyper-v 可扩展交换机扩展的发送和接收操作。 下表描述了扩展可对通过可扩展交换机数据路径发送或接收的数据包执行的操作。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left"><a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">捕获扩展</a></th>
<th align="left"><a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">筛选扩展</a></th>
<th align="left"><a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">转发扩展</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">发起数据包</td>
<td align="left">X</td>
<td align="left">X</td>
<td align="left">X</td>
</tr>
<tr class="even">
<td align="left">克隆数据包</td>
<td align="left"></td>
<td align="left">X</td>
<td align="left">X</td>
</tr>
<tr class="odd">
<td align="left">转发数据包</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

本节包括下列主题：

[发起数据包流量](originating-packet-traffic.md)

[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)

[将数据包转发到 Hyper-V 可扩展交换机端口](forwarding-packets-to-hyper-v-extensible-switch-ports.md)

有关可扩展交换机数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 





