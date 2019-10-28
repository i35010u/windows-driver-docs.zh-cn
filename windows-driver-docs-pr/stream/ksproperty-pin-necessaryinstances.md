---
title: KSPROPERTY\_PIN\_NECESSARYINSTANCES
description: 此属性返回 pin 工厂在筛选器可执行 i/o 操作之前必须实例化的最小 pin 数。
ms.assetid: d30d7546-3d16-42df-b640-a8ec37bca35c
keywords:
- KSPROPERTY_PIN_NECESSARYINSTANCES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NECESSARYINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df8aaa3d643d9567117102b3dba60ee27c3d4b85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838847"
---
# <a name="ksproperty_pin_necessaryinstances"></a>KSPROPERTY\_PIN\_NECESSARYINSTANCES


此属性返回 pin 工厂在筛选器可执行 i/o 操作之前必须实例化的最小 pin 数。

## <span id="ddk_ksproperty_pin_necessaryinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_NECESSARYINSTANCES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 KSP\_PIN 指定此属性，其中成员指定相关的 PIN 工厂。

KSPROPERTY\_PIN\_NECESSARYINSTANCES 返回类型为 ULONG 的值，指定 pin 工厂必须实例化的最小 pin 数。

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


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






