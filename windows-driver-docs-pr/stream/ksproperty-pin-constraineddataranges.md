---
title: KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES
description: KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES 属性指定的当前支持的插针上 pin 工厂实例化的数据范围列表。
ms.assetid: 6328a128-c6f8-4de1-a86a-0a7c8a940e18
keywords:
- KSPROPERTY_PIN_CONSTRAINEDDATARANGES 流式处理媒体设备
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
ms.openlocfilehash: e37fc6110a8d7be8f18df53d71c6e28b9caa97d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546822"
---
# <a name="kspropertypinconstraineddataranges"></a>KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES


KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES 属性指定的当前支持的插针上 pin 工厂实例化的数据范围列表。

## <span id="ddk_ksproperty_pin_constraineddataranges_ks"></span><span id="DDK_KSPROPERTY_PIN_CONSTRAINEDDATARANGES_KS"></span>


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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff561658" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561658)"> <strong>KSDATARANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**PinId**的成员[ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)结构指定 pin 工厂为其查询。

此属性返回[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)结构后, 跟一系列 64 位对齐[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构。

KS 筛选器使用此属性，以报告当前受 pin 实例化此 pin 工厂，基于任何约束的数据范围施加的 KS 筛选器的当前内部状态。 使用[ **KSPROPERTY\_PIN\_DATARANGES** ](ksproperty-pin-dataranges.md)属性来报告 KS 筛选器，而不考虑动态约束支持的所有数据范围的完整列表。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块的详细信息的查询此属性。

有关详细信息，请参阅[KS 数据格式和数据范围](https://msdn.microsoft.com/library/windows/hardware/ff567632)。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDATARANGE**](https://msdn.microsoft.com/library/windows/hardware/ff561658)

[**KSPROPERTY\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

 

 






