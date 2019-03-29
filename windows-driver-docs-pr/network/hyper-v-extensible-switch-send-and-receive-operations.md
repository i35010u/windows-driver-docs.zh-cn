---
title: Hyper-V 可扩展交换机发送和接收操作
description: Hyper-V 可扩展交换机发送和接收操作
ms.assetid: 3BC59344-CF8E-436F-A1C9-883707990C7D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d470df5e2414a6a20c3a73e6de954f0a4eb49bd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566580"
---
# <a name="hyper-v-extensible-switch-send-and-receive-operations"></a>Hyper-V 可扩展交换机发送和接收操作


本部分介绍了发送和接收的 HYPER-V 可扩展交换机扩展的操作。 下表描述了扩展可以在发送或接收通过可扩展交换机数据路径的数据包执行的操作。

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
<td align="left">原始数据包</td>
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
<td align="left">将数据包转发</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

本部分包括以下主题：

[原始数据包流量](originating-packet-traffic.md)

[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)

[将数据包转发到的 HYPER-V 可扩展交换机端口](forwarding-packets-to-hyper-v-extensible-switch-ports.md)

有关可扩展交换机数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 





