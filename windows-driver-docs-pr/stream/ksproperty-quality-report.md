---
title: KSPROPERTY\_质量\_报告
description: KSPROPERTY\_QUALITY\_REPORT 属性是一个可选属性，如果 pin 支持质量管理，则应实现该属性。
ms.assetid: 9879a28d-aa92-4583-be63-03fed67c8416
keywords:
- KSPROPERTY_QUALITY_REPORT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_QUALITY_REPORT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6cda26b7e36845fba333d601a49c5104bc18aac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838834"
---
# <a name="ksproperty_quality_report"></a>KSPROPERTY\_质量\_报告


KSPROPERTY\_QUALITY\_REPORT 属性是一个可选属性，如果 pin 支持质量管理，则应实现该属性。

## <span id="ddk_ksproperty_quality_report_ks"></span><span id="DDK_KSPROPERTY_QUALITY_REPORT_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality" data-raw-source="[&lt;strong&gt;KSQUALITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)"><strong>KSQUALITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_QUALITY\_报表的属性值为类型[**KSQUALITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)结构。 使用此结构可获取或设置当前所用帧的比例和最佳帧接收时间的增量。

类驱动程序不处理此属性;stream 微型驱动程序必须自行提供处理。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSQUALITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)

 

 






