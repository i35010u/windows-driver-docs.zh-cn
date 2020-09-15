---
title: KSPROPERTY \_ 流 \_ 质量
description: "\"KSPROPERTY \\_ 流 \\_ 质量\" 属性是一个可选属性，如果 Pin 生成质量管理投诉，应实现该属性。"
ms.assetid: ed4d9baa-967a-41b3-b8b9-910b86230254
keywords:
- KSPROPERTY_STREAM_QUALITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_QUALITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e643583a29c6f915f50455918e4740df1aa3199
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105712"
---
# <a name="ksproperty_stream_quality"></a>KSPROPERTY \_ 流 \_ 质量


"KSPROPERTY \_ 流 \_ 质量" 属性是一个可选属性，如果 Pin 生成质量管理投诉，应实现该属性。

## <span id="ddk_ksproperty_stream_quality_ks"></span><span id="DDK_KSPROPERTY_STREAM_QUALITY_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager" data-raw-source="[&lt;strong&gt;KSQUALITY_MANAGER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager)"><strong>KSQUALITY_MANAGER</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

发出此请求时，pin 连接反过来会通过使用给定的上下文参数提供 [**KSQUALITY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality) 结构来通知质量管理器。

如果 pin 不报告质量问题，则不需要支持 KSPROPERTY \_ 流 \_ 质量。

另请参阅 [质量管理](./quality-management.md)。

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

[**KSQUALITY \_ 管理器**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager)

[**KSQUALITY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)

