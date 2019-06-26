---
title: KSPROPERTY\_PIN\_DATARANGES
description: 客户端使用 KSPROPERTY\_PIN\_DATARANGES 属性来确定受 pin 的 pin 工厂实例化的数据范围。
ms.assetid: 90dd82c4-36a2-4fd3-b842-bbd9588a2740
keywords:
- KSPROPERTY_PIN_DATARANGES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATARANGES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 885de5eb6d8af481497d4de38873c61fa1019176
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393353"
---
# <a name="kspropertypindataranges"></a>KSPROPERTY\_PIN\_DATARANGES


客户端使用 KSPROPERTY\_PIN\_DATARANGES 属性来确定受 pin 的 pin 工厂实例化的数据范围。

## <span id="ddk_ksproperty_pin_dataranges_ks"></span><span id="DDK_KSPROPERTY_PIN_DATARANGES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>一个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"> <strong>KSMULTIPLE_ITEM</strong> </a>结构后, 跟一系列 64 位对齐<a href="https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))"> <strong>KSDATARANGE</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定此属性使用 KSP\_PIN，其中**PinId**成员指定为其返回可接受的数据范围的 pin 工厂。

KS 筛选器返回所有支持的 pin，pin 工厂实例化的数据范围。 KS 筛选器可能不支持在其当前的内部状态报告的数据范围。 若要确定支持的当前内部状态的数据范围，请使用[ **KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块的详细信息的查询此属性。

有关详细信息，请参阅[KS 数据格式和数据范围](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)。

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


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

 

 






