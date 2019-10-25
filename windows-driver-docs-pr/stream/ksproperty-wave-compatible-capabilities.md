---
title: KSPROPERTY\_波\_兼容的\_功能
description: "\"KSPROPERTY\\_波形\\_兼容的\\_功能\" 属性用于确定设备的波形兼容功能。"
ms.assetid: 59b24d84-8b98-4928-aaae-46cb14c0d140
keywords:
- KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 298737768a9be6f69c8c2db895a482b17ccdedad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823597"
---
# <a name="ksproperty_wave_compatible_capabilities"></a>KSPROPERTY\_波\_兼容的\_功能


"KSPROPERTY\_波形\_兼容的\_功能" 属性用于确定设备的波形兼容功能。

## <span id="ddk_ksproperty_wave_compatible_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES_KS"></span>


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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_compatcaps" data-raw-source="[&lt;strong&gt;KSWAVE_COMPATCAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_compatcaps)"><strong>KSWAVE_COMPATCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 KSWAVE\_COMPATCAPS 结构，描述波形设备是否接受输入，生成输出，或同时执行这两项操作。

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

[**KSWAVE\_COMPATCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_compatcaps)

 

 






