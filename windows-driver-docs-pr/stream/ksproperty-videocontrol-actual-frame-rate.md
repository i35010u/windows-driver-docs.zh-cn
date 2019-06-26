---
title: KSPROPERTY\_VIDEOCONTROL\_ACTUAL\_FRAME\_RATE
description: KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率属性检索的设备指定 pin 的流式处理的帧速率。 此属性为可选项。
ms.assetid: 1681bb54-bdd8-499d-b544-c0e8b14deaa5
keywords:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f532dffb1fe49e53575459f2a19c71bfc0d3a07e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355920"
---
# <a name="kspropertyvideocontrolactualframerate"></a>KSPROPERTY\_VIDEOCONTROL\_ACTUAL\_FRAME\_RATE


KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率属性检索的设备指定 pin 的流式处理的帧速率。 此属性为可选项。

## <span id="ddk_ksproperty_videocontrol_actual_frame_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S</strong></a></p></td>
<td><p>KSPROPERTY_VIDEOCONTROL</p>
<p>_ACTUAL_FRAME_RATE_S</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率\_S 结构，它指定实际帧速率信息时的查询，例如图像、 当前的实际帧速率和当前的最大可用帧速率的维度 （宽度和高度）。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)

 

 






