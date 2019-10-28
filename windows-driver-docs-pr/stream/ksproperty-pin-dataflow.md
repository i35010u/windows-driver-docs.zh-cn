---
title: KSPROPERTY\_PIN\_数据流
description: KSPROPERTY\_PIN\_数据流属性指定由 pin 工厂实例化的 pin 上数据流的方向。 接收器 pin 是筛选器中的入口点;来自筛选器的源 pin 输出。
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
ms.openlocfilehash: 5b4c64741903a733eb64bdf1fcc6e0c33c7c4d97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838862"
---
# <a name="ksproperty_pin_dataflow"></a>KSPROPERTY\_PIN\_数据流


KSPROPERTY\_PIN\_数据流属性指定由 pin 工厂实例化的 pin 上数据流的方向。 接收器 pin 是筛选器中的入口点;来自筛选器的源 pin 输出。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow" data-raw-source="[&lt;strong&gt;KSPIN_DATAFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)"><strong>KSPIN_DATAFLOW</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在[**KSP\_固定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)结构的**PinId**成员中指定 pin 工厂。

KSPROPERTY\_PIN\_数据流返回[**KSPIN 类型\_数据流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)的枚举，将设置为**KSPIN\_数据流\_** 或 KSPIN\_数据流\_OUT。

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

## <a name="see-also"></a>另请参阅


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSPIN\_数据流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)

 

 






