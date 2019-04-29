---
title: KSPROPERTY\_质量\_报表
description: KSPROPERTY\_质量\_报表属性是可选属性，如果 pin 支持质量管理应实现。
ms.assetid: 9879a28d-aa92-4583-be63-03fed67c8416
keywords:
- KSPROPERTY_QUALITY_REPORT 流式处理媒体设备
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
ms.openlocfilehash: 6567bf3b9bc5a737f68f64dca0f348b73204f40f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380799"
---
# <a name="kspropertyqualityreport"></a>KSPROPERTY\_质量\_报表


KSPROPERTY\_质量\_报表属性是可选属性，如果 pin 支持质量管理应实现。

## <span id="ddk_ksproperty_quality_report_ks"></span><span id="DDK_KSPROPERTY_QUALITY_REPORT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566728" data-raw-source="[&lt;strong&gt;KSQUALITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566728)"><strong>KSQUALITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_质量\_报表的属性值为类型[ **KSQUALITY** ](https://msdn.microsoft.com/library/windows/hardware/ff566728)结构。 使用此结构来获取或设置当前正在使用的帧的比例和从最佳帧回执时间差异。

在类驱动程序不处理此属性;流微型驱动程序必须提供自己的处理。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSQUALITY**](https://msdn.microsoft.com/library/windows/hardware/ff566728)

 

 






