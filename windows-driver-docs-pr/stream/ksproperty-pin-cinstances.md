---
title: KSPROPERTY\_PIN\_CINSTANCES
description: 当前的 pin 已实例化此 pin 工厂，数，以及此 pin 工厂可以实例化，每个筛选器的 pin 的最大数目。
ms.assetid: 0a6c0afa-1bdf-4b80-a8d7-55f13d9da74b
keywords:
- KSPROPERTY_PIN_CINSTANCES 流式处理媒体设备
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
ms.openlocfilehash: 8de2f8a114283deaae9f92581c91c3dae13c5a1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346467"
---
# <a name="kspropertypincinstances"></a>KSPROPERTY\_PIN\_CINSTANCES


当前的 pin 已实例化此 pin 工厂，数，以及此 pin 工厂可以实例化，每个筛选器的 pin 的最大数目。

## <span id="ddk_ksproperty_pin_cinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_CINSTANCES_KS"></span>


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
<td><p>KSPIN_CINSTANCES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回的结构类型 KSPIN\_CINSTANCES:

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

下面是描述每个成员的 KSPIN\_CINSTANCES 结构。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
指定的 pin 的 pin 工厂可以实例化的最大数目上的筛选器或 KSINTANCE\_不确定是否存在无最大值。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
指定的筛选器上的 pin 的 pin 工厂已实例化的当前数目。

此属性指定给定的 pin 工厂的每个筛选器最大值。 使用[ **KSPROPERTY\_PIN\_GLOBALCINSTANCES** ](ksproperty-pin-globalcinstances.md)属性来指定给定的 pin 工厂的整体最大值。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块的详细信息的查询此属性。

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

 

 





