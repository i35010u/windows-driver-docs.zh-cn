---
title: KSPROPERTY \_ VIDEOCOMPRESSION \_ 关键帧 \_ 速率
description: KSPROPERTY \_ VIDEOCOMPRESSION \_ 关键帧 \_ 速率属性控制关键帧速率。 必须实现此属性。
ms.assetid: 2b39dbe4-5010-4454-92ca-699b3b2c21ac
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 064fa1d4015308c69e119363f7053f903c02e535
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191403"
---
# <a name="ksproperty_videocompression_keyframe_rate"></a>KSPROPERTY \_ VIDEOCOMPRESSION \_ 关键帧 \_ 速率


KSPROPERTY \_ VIDEOCOMPRESSION \_ 关键帧 \_ 速率属性控制关键帧速率。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_keyframe_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE_KS"></span>


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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定关键帧速率的 LONG。

<a name="remarks"></a>注解
-------

KSPROPERTY **Value** \_ VIDEOCOMPRESSION S 结构的 Value 成员 \_ 指定属性设置。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

 

