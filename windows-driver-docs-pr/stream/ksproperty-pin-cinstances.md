---
title: KSPROPERTY\_PIN\_CINSTANCES
description: 此插针工厂实例化的当前插针数量，以及此 pin 工厂可根据筛选器实例化的最大 pin 数。
ms.assetid: 0a6c0afa-1bdf-4b80-a8d7-55f13d9da74b
keywords:
- KSPROPERTY_PIN_CINSTANCES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c94923f1b641b5cf9d038c05a580e20622bf6b85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842749"
---
# <a name="ksproperty_pin_cinstances"></a>KSPROPERTY\_PIN\_CINSTANCES


此插针工厂实例化的当前插针数量，以及此 pin 工厂可根据筛选器实例化的最大 pin 数。

## <span id="ddk_ksproperty_pin_cinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_CINSTANCES_KS"></span>


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

此属性返回类型为 KSPIN\_CINSTANCES 的结构：

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

下面是 KSPIN\_CINSTANCES 结构的每个成员的说明。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
指定 pin 工厂在筛选器上可以实例化的最大 pin 数，或者，如果没有最大值，则 KSINTANCE\_不确定。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
指定 pin 工厂在筛选器上实例化的当前针脚数。

此属性为给定的 pin 工厂指定每个筛选器的最大值。 使用[**KSPROPERTY\_引脚\_GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)属性来指定给定 PIN 工厂的总最大值。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性以查询详细信息。

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

 

 





