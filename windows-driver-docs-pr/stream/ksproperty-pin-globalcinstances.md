---
title: KSPROPERTY\_PIN\_GLOBALCINSTANCES
description: 客户端使用 KSPROPERTY\_PIN\_GLOBALCINSTANCES 来确定 pin 工厂实例化的当前 pin 数量，以及此 PIN 工厂可以实例化的最大 pin 数量。 此属性为可选项。
ms.assetid: 888b8ddf-aa36-4e2f-a74c-ab4ee693bb36
keywords:
- KSPROPERTY_PIN_GLOBALCINSTANCES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_GLOBALCINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1c95334a1a667caf9c089a028c7d98c96d3a65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838856"
---
# <a name="ksproperty_pin_globalcinstances"></a>KSPROPERTY\_PIN\_GLOBALCINSTANCES


客户端使用 KSPROPERTY\_PIN\_GLOBALCINSTANCES 来确定 pin 工厂实例化的当前 pin 数量，以及此 PIN 工厂可以实例化的最大 pin 数量。 此属性为可选项。

## <span id="ddk_ksproperty_pin_globalcinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_GLOBALCINSTANCES_KS"></span>


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
<td><p>KSPIN_CINSTANCES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 KSP\_PIN 指定此属性，其中**PinId**成员指定 pin 工厂。

KSPIN\_CINSTANCES 是一种格式的数据结构：

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

下面是 KSPIN\_CINSTANCES 结构的每个成员的说明。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
指定 pin 工厂在驱动程序上可以实例化的最大 pin 数，或者，如果没有最大值，则 KSINTANCE\_不确定。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
指定 pin 工厂在驱动程序上实例化的当前 pin 数。

类驱动程序不处理此属性;stream 微型驱动程序必须自行提供处理。

KSPROPERTY\_引脚\_GLOBALCINSTANCES 指定所有实例的当前最大和最大实例数，超过筛选器的所有实例。 若要确定每个筛选器的值，请使用[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)。

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

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

 

 






