---
title: KSEVENT \_ VIDCAPTOSTI \_ EXT \_ 触发器
description: KSEVENT \_ VIDCAPTOSTI \_ EXT \_ 触发器事件传播一项操作，例如，在视频捕获设备上按下触发器按钮的时间，从内核模式视频捕获微型驱动程序到 DirectShow in user 模式。
keywords:
- KSEVENT_VIDCAPTOSTI_EXT_TRIGGER 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAPTOSTI_EXT_TRIGGER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3afdcac79acf8abf8827ad05359d25b9fb431a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813419"
---
# <a name="ksevent_vidcaptosti_ext_trigger"></a>KSEVENT \_ VIDCAPTOSTI \_ EXT \_ 触发器


KSEVENT \_ VIDCAPTOSTI \_ EXT \_ 触发器事件传播一项操作，例如，在视频捕获设备上按下触发器按钮的时间，从内核模式视频捕获微型驱动程序到 DirectShow in user 模式。

## <span id="ddk_ksevent_vidcaptosti_ext_trigger_ks"></span><span id="DDK_KSEVENT_VIDCAPTOSTI_EXT_TRIGGER_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅 [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index)。

