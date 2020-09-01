---
title: KSPROPERTY \_ PIN \_ GLOBALCINSTANCES
description: 客户端使用 KSPROPERTY \_ pin \_ GLOBALCINSTANCES 来确定由 pin 工厂实例化的当前 pin 数量，以及此 PIN 工厂可以实例化的最大 pin 数。 此属性是可选的。
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
ms.openlocfilehash: 731cec328c050ae557bdcbb684481a999ea90f8f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192511"
---
# <a name="ksproperty_pin_globalcinstances"></a>KSPROPERTY \_ PIN \_ GLOBALCINSTANCES


客户端使用 KSPROPERTY \_ pin \_ GLOBALCINSTANCES 来确定由 pin 工厂实例化的当前 pin 数量，以及此 PIN 工厂可以实例化的最大 pin 数。 此属性是可选的。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_CINSTANCES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

使用 KSP pin 指定此属性 \_ ，其中 **PinId** 成员指定 PIN 工厂。

KSPIN \_ CINSTANCES 是一种格式的数据结构：

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

下面是 KSPIN CINSTANCES 结构的每个成员的说明 \_ 。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
指定 pin 工厂在驱动程序上可以实例化的最大 pin 数，或者，如果没有最大值，则 KSINTANCE 不 \_ 确定。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
指定 pin 工厂在驱动程序上实例化的当前 pin 数。

类驱动程序不处理此属性;stream 微型驱动程序必须自行提供处理。

KSPROPERTY \_ 引脚 \_ GLOBALCINSTANCES 指定筛选器的所有实例上的最新和最大实例数。 若要确定每个筛选器的值，请使用 [**KSPROPERTY \_ PIN \_ CINSTANCES**](ksproperty-pin-cinstances.md)。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSPROPERTY \_ PIN \_ CINSTANCES**](ksproperty-pin-cinstances.md)

 

