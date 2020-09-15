---
title: KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO
description: KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO 属性检索设备的视频压缩功能。 必须实现此属性。
ms.assetid: 87e19e19-d90e-49c6-a6f0-cf33abf28c01
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_GETINFO 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_GETINFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c49a5710a52254718bc80985f9346963719f52
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104410"
---
# <a name="ksproperty_videocompression_getinfo"></a>KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO


KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO 属性检索设备的视频压缩功能。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_getinfo_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_GETINFO_KS"></span>


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
<td><p>否</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO \_ S 结构，它指定视频压缩设置，如要查询其压缩功能的流、默认的关键帧速率、默认预测帧速率、默认质量设置、质量设置的数量，以及各种压缩功能。

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

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

