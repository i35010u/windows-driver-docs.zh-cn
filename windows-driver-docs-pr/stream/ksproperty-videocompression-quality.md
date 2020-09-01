---
title: KSPROPERTY \_ VIDEOCOMPRESSION \_ QUALITY
description: KSPROPERTY \_ VIDECOMPRESSION \_ quality 属性控制视频压缩质量设置。 必须实现此属性。
ms.assetid: 7566f60e-fe49-4009-bd61-b29d2adb4e8c
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4c248d90d6dd3b0de24bc1f9d4415dc3ca2ba3d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185863"
---
# <a name="ksproperty_videocompression_quality"></a>KSPROPERTY \_ VIDEOCOMPRESSION \_ QUALITY


KSPROPERTY \_ VIDECOMPRESSION \_ quality 属性控制视频压缩质量设置。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_quality_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_QUALITY_KS"></span>


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

 

) 操作数据 (的属性值是指定视频压缩质量值的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOCOMPRESSION S 结构的 Value 成员 \_ 指定质量指标。

此属性的值的范围为0到10000。 0表示最高的质量，10000。 微型驱动程序确定其自身的默认值。

支持此属性的微型驱动程序应在用于检索 VIDEOCOMPRESSION 视频压缩功能的[**KSPROPERTY \_ GETINFO \_ 微型驱动程序 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的 "**功能**" 成员中设置**KS \_ CompressionCaps \_ CanQuality**标志。 如果微型驱动程序设置了 KS \_ CompressionCaps \_ CanQuality，则它应支持属性的 get 和 set 请求。

此属性的值的范围为0到10000。 0表示最高的质量，10000。 微型驱动程序确定其自身的默认值。

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

 

