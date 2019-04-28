---
title: KSPROPERTY\_批\_卷
description: KSPROPERTY\_批\_卷属性指定批设备的卷设置。
ms.assetid: c5725f7d-b965-43f3-9c49-faff82d99580
keywords:
- KSPROPERTY_WAVE_VOLUME 流式处理媒体设备
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
ms.openlocfilehash: cdb34840dea2a5cc4551b379ac8c824f34633735
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331763"
---
# <a name="kspropertywavevolume"></a>KSPROPERTY\_批\_卷


KSPROPERTY\_批\_卷属性指定批设备的卷设置。

## <span id="ddk_ksproperty_wave_volume_ks"></span><span id="DDK_KSPROPERTY_WAVE_VOLUME_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567252" data-raw-source="[&lt;strong&gt;KSWAVE_VOLUME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567252)"><strong>KSWAVE_VOLUME</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSWAVE\_卷结构描述的左侧和右侧衰减量。

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

[**KSWAVE\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff567252)

 

 






