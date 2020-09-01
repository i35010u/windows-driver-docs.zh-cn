---
title: KSEVENT \_ TVAUDIO \_ 已更改
description: KSEVENT \_ TVAUDIO \_ CHANGED 事件传播一项操作，例如，在用户模式下，新优化到的通道支持立体声音频，从内核模式视频捕获微型驱动程序到 DirectShow。
ms.assetid: 98d77001-9844-4893-9a23-9c06f7d75841
keywords:
- KSEVENT_TVAUDIO_CHANGED 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_TVAUDIO_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51670778f243f56e31cf718f05e20bafc83e9fcd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188419"
---
# <a name="ksevent_tvaudio_changed"></a>KSEVENT \_ TVAUDIO \_ 已更改


KSEVENT \_ TVAUDIO \_ CHANGED 事件传播一项操作，例如，在用户模式下，新优化到的通道支持立体声音频，从内核模式视频捕获微型驱动程序到 DirectShow。

## <span id="ddk_ksevent_tvaudio_changed_ks"></span><span id="DDK_KSEVENT_TVAUDIO_CHANGED_KS"></span>


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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅 [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index)。

 

