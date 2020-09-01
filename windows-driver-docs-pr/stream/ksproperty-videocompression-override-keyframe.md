---
title: KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 关键帧
description: KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 关键帧属性暂时替代关键帧速率。 此属性是可选的。
ms.assetid: 068bd5e6-e283-4c8d-8837-c0e0cef4df65
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e680b3e0feaf81d663bc0f84e0cc2905203a8f3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192829"
---
# <a name="ksproperty_videocompression_override_keyframe"></a>KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 关键帧


KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 关键帧属性暂时替代关键帧速率。 此属性是可选的。

## <span id="ddk_ksproperty_videocompression_override_keyframe_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定新的关键帧图片号的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOCOMPRESSION S 结构的值成员 \_ 指定要成为关键帧的帧号。

视频捕获微型驱动程序不支持此属性。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

 

