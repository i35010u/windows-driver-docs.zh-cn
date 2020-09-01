---
title: KSPROPERTY \_ 质量 \_ 报表
description: KSPROPERTY \_ 质量 \_ 报表属性是一个可选属性，如果 pin 支持质量管理，则应实现该属性。
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
ms.openlocfilehash: e5d6afbfb896a96f25882d86d5c05b90c1ef67cb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190883"
---
# <a name="ksproperty_quality_report"></a>KSPROPERTY \_ 质量 \_ 报表


KSPROPERTY \_ 质量 \_ 报表属性是一个可选属性，如果 pin 支持质量管理，则应实现该属性。

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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality" data-raw-source="[&lt;strong&gt;KSQUALITY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)"><strong>KSQUALITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY \_ 质量 \_ 报告的属性值为 [**KSQUALITY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality) 结构。 使用此结构可获取或设置当前所用帧的比例和最佳帧接收时间的增量。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSQUALITY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)

 

