---
title: KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES
description: KSPROPERTY \_ 引脚 \_ CONSTRAINEDDATARANGES 属性指定在 pin 工厂实例化的 pin 当前支持的数据范围列表。
ms.assetid: 6328a128-c6f8-4de1-a86a-0a7c8a940e18
keywords:
- KSPROPERTY_PIN_CONSTRAINEDDATARANGES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CONSTRAINEDDATARANGES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd9645f35549fad8fd086a2ca2dfe808cca61676
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103736"
---
# <a name="ksproperty_pin_constraineddataranges"></a>KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES


KSPROPERTY \_ 引脚 \_ CONSTRAINEDDATARANGES 属性指定在 pin 工厂实例化的 pin 当前支持的数据范围列表。

## <span id="ddk_ksproperty_pin_constraineddataranges_ks"></span><span id="DDK_KSPROPERTY_PIN_CONSTRAINEDDATARANGES_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>和<a href="/previous-versions/ff561658(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](/previous-versions/ff561658(v=vs.85))"> <strong>KSDATARANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[**KSP \_ pin**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)结构的**PinId**成员指定要查询的 PIN 工厂。

此属性返回 [**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item) 结构，后跟一系列64位对齐的 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构。

KS 筛选器使用此属性，根据 KS 筛选器的当前内部状态所强加的任何约束，来报告此 pin 工厂中实例化的当前支持的数据区域。 无论动态约束如何，都可以使用 [**KSPROPERTY \_ 引脚 \_ DATARANGES**](ksproperty-pin-dataranges.md) 属性报告 KS 筛选器支持的所有数据范围的完整列表。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性以查询详细信息。

有关详细信息，请参阅 [KS 数据格式和数据区域](./ks-data-formats-and-data-ranges.md)。

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


[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))

[**KSPROPERTY \_ PIN \_ DATARANGES**](ksproperty-pin-dataranges.md)

