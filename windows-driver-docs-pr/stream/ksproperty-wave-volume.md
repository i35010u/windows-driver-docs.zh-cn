---
title: KSPROPERTY\_波形\_音量
description: KSPROPERTY\_WAVE\_VOLUME 属性指定波形设备的音量设置。
ms.assetid: c5725f7d-b965-43f3-9c49-faff82d99580
keywords:
- KSPROPERTY_WAVE_VOLUME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0081da607e0195d901198d8d2a332033100624fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845548"
---
# <a name="ksproperty_wave_volume"></a>KSPROPERTY\_波形\_音量


KSPROPERTY\_WAVE\_VOLUME 属性指定波形设备的音量设置。

## <span id="ddk_ksproperty_wave_volume_ks"></span><span id="DDK_KSPROPERTY_WAVE_VOLUME_KS"></span>


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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume" data-raw-source="[&lt;strong&gt;KSWAVE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume)"><strong>KSWAVE_VOLUME</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 KSWAVE\_卷结构，用于描述左右衰减量。

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

[**KSWAVE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume)

 

 






