---
title: KSEVENT\_横线\_更改
description: KSEVENT\_纵横比\_CHANGED 事件会在用户模式下传播从内核模式视频捕获微型驱动程序到 DirectShow 的操作，例如新的路由配置。
ms.assetid: b67d95a3-7c30-49ae-a2df-eb88491c2e97
keywords:
- KSEVENT_CROSSBAR_CHANGED 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CROSSBAR_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca50923808fb474583f36cb78093f8ea3a8baaa2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837956"
---
# <a name="ksevent_crossbar_changed"></a>KSEVENT\_横线\_更改


KSEVENT\_纵横比\_CHANGED 事件会在用户模式下传播从内核模式视频捕获微型驱动程序到 DirectShow 的操作，例如新的路由配置。

## <span id="ddk_ksevent_crossbar_changed_ks"></span><span id="DDK_KSEVENT_CROSSBAR_CHANGED_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)。

 

 





