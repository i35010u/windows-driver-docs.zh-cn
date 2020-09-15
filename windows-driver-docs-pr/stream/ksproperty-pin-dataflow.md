---
title: KSPROPERTY \_ PIN \_ 数据流
description: KSPROPERTY \_ pin \_ 数据流属性指定由 pin 工厂实例化的 pin 上数据流的方向。 接收器 pin 是筛选器中的入口点;来自筛选器的源 pin 输出。
ms.assetid: 3132b344-c4f3-48dc-9829-f4e97d0f18fc
keywords:
- KSPROPERTY_PIN_DATAFLOW 流媒体设备
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
ms.openlocfilehash: 0c99088df7a793be111114586be047b7021e749c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103726"
---
# <a name="ksproperty_pin_dataflow"></a>KSPROPERTY \_ PIN \_ 数据流


KSPROPERTY \_ pin \_ 数据流属性指定由 pin 工厂实例化的 pin 上数据流的方向。 接收器 pin 是筛选器中的入口点;来自筛选器的源 pin 输出。

## <span id="ddk_ksproperty_pin_dataflow_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAFLOW_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow" data-raw-source="[&lt;strong&gt;KSPIN_DATAFLOW&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)"><strong>KSPIN_DATAFLOW</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定[**KSP \_ pin**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)结构的**PinId**成员中的 pin 工厂。

KSPROPERTY \_ PIN \_ 数据流返回 [**KSPIN \_ 数据流**](/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)类型的枚举，并将其设置 **为 \_ KSPIN \_ 数据流** 或 KSPIN \_ 数据流 \_ OUT。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSPIN \_ 数据流**](/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)

