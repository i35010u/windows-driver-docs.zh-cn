---
title: KSPROPERTY\_VIDEOCOMPRESSION\_质量
description: KSPROPERTY\_VIDECOMPRESSION\_QUALITY 属性控制视频压缩质量设置。 必须实现此属性。
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
ms.openlocfilehash: 79ad71a6dde954232db80118201ce690150d0bfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837879"
---
# <a name="ksproperty_videocompression_quality"></a>KSPROPERTY\_VIDEOCOMPRESSION\_质量


KSPROPERTY\_VIDECOMPRESSION\_QUALITY 属性控制视频压缩质量设置。 必须实现此属性。

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
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定视频压缩质量值的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VIDEOCOMPRESSION\_S 结构的**值**成员指定质量指标。

此属性的值的范围为0到10000。 0表示最高的质量，10000。 微型驱动程序确定其自身的默认值。

支持此属性的微型驱动程序应将**KS\_CompressionCaps\_CanQuality**标志设置为[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的**功能**成员，检索微型驱动程序的视频压缩功能。 如果微型驱动程序将 KS\_CompressionCaps 设置\_CanQuality，则它应同时支持对属性的 get 和 set 请求。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 






