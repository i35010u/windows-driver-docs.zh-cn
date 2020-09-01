---
title: '\_ \_ \_ 每个 \_ 关键帧的 KSPROPERTY VIDEOCOMPRESSION PFRAMES'
description: KSPROPERTY \_ VIDEOCOMPRESSION \_ PFRAMES \_ PER \_ 关键帧属性控制预测帧 (P 帧) 时间间隔。 必须实现此属性。
ms.assetid: feb839b4-32fc-4fe9-b015-019d9d683c66
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51d6c3cf037777a367b4892eba3a3ec26cef7592
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185871"
---
# <a name="ksproperty_videocompression_pframes_per_keyframe"></a>\_ \_ \_ 每个 \_ 关键帧的 KSPROPERTY VIDEOCOMPRESSION PFRAMES


KSPROPERTY \_ VIDEOCOMPRESSION \_ PFRAMES \_ PER \_ 关键帧属性控制预测帧 (P 帧) 时间间隔。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_pframes_per_keyframe_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME_KS"></span>


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

 

 (操作数据) 的属性值是指定每个关键帧的预测帧数的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOCOMPRESSION S 结构的 Value 成员 \_ 指定每个关键帧的 P 帧数。 如果 set 请求提供 **负值，则**微型驱动程序应将 "P 帧速率" 设置为默认值。

支持此属性的微型驱动程序应 \_ \_ 在用于检索 VIDEOCOMPRESSION 视频压缩功能的[**KSPROPERTY \_ GETINFO \_ 微型驱动程序 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的 "**功能**" 成员中设置 KS VideoCompressionCaps CanBFrame 标志。

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

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

