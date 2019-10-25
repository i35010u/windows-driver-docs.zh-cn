---
title: KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率
description: KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率属性检索指定 pin 的设备流式传输的帧速率。 此属性为可选项。
ms.assetid: 1681bb54-bdd8-499d-b544-c0e8b14deaa5
keywords:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE 流媒体设备
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
ms.openlocfilehash: 7abae78a5c39046d8a5c6146528c5b4689cf07f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837876"
---
# <a name="ksproperty_videocontrol_actual_frame_rate"></a>KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率


KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率属性检索指定 pin 的设备流式传输的帧速率。 此属性为可选项。

## <span id="ddk_ksproperty_videocontrol_actual_frame_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S</strong></a></p></td>
<td><p>KSPROPERTY_VIDEOCONTROL</p>
<p>_ACTUAL_FRAME_RATE_S</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率\_S 结构，它指定查询时的实际帧速率信息，如图像、当前实际帧速率和当前最大可用帧速率。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)

 

 






