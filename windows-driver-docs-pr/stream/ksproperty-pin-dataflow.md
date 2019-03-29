---
title: KSPROPERTY\_PIN\_DATAFLOW
description: KSPROPERTY\_PIN\_数据流属性指定的数据流方向 pin 工厂实例化的插针上。 接收器 pin 是入口点筛选器;源插针从筛选器的输出。
ms.assetid: 3132b344-c4f3-48dc-9829-f4e97d0f18fc
keywords:
- KSPROPERTY_PIN_DATAFLOW 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATAFLOW
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15816fbe2f46c844b8185fe23463ea8a718d786e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569523"
---
# <a name="kspropertypindataflow"></a>KSPROPERTY\_PIN\_DATAFLOW


KSPROPERTY\_PIN\_数据流属性指定的数据流方向 pin 工厂实例化的插针上。 接收器 pin 是入口点筛选器;源插针从筛选器的输出。

## <span id="ddk_ksproperty_pin_dataflow_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAFLOW_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563532" data-raw-source="[&lt;strong&gt;KSPIN_DATAFLOW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563532)"><strong>KSPIN_DATAFLOW</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定在 pin 工厂**PinId**的成员[ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)结构。

KSPROPERTY\_PIN\_数据流返回类型的枚举[ **KSPIN\_数据流**](https://msdn.microsoft.com/library/windows/hardware/ff563532)，设置为**KSPIN\_数据流\_IN**或 KSPIN\_数据流\_出。

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

## <a name="see-also"></a>请参阅


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSPIN\_数据流**](https://msdn.microsoft.com/library/windows/hardware/ff563532)

 

 






