---
title: KSPROPERTY\_VIDEOCOMPRESSION\_KEYFRAME\_RATE
description: KSPROPERTY\_VIDEOCOMPRESSION\_关键帧\_速率属性控制的关键帧速率。 必须实现此属性。
ms.assetid: 2b39dbe4-5010-4454-92ca-699b3b2c21ac
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE 流式处理媒体设备
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
ms.openlocfilehash: c8a19326704e618cc5911545d3b2092d7ddb7f61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355938"
---
# <a name="kspropertyvideocompressionkeyframerate"></a>KSPROPERTY\_VIDEOCOMPRESSION\_KEYFRAME\_RATE


KSPROPERTY\_VIDEOCOMPRESSION\_关键帧\_速率属性控制的关键帧速率。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_keyframe_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE_KS"></span>


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
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 long 类型的值，指定关键帧速率。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOCOMPRESSION\_S 结构指定的属性设置。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

 

 






