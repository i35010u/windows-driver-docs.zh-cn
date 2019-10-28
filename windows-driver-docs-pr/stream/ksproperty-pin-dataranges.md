---
title: KSPROPERTY\_PIN\_DATARANGES
description: 客户端使用 KSPROPERTY\_PIN\_DATARANGES 属性来确定 pin 工厂实例化的 pin 支持的数据范围。
ms.assetid: 90dd82c4-36a2-4fd3-b842-bbd9588a2740
keywords:
- KSPROPERTY_PIN_DATARANGES 流媒体设备
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
ms.openlocfilehash: 755fd0864fd23d9d22bb0d73049e7f6e02b28b4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838858"
---
# <a name="ksproperty_pin_dataranges"></a>KSPROPERTY\_PIN\_DATARANGES


客户端使用 KSPROPERTY\_PIN\_DATARANGES 属性来确定 pin 工厂实例化的 pin 支持的数据范围。

## <span id="ddk_ksproperty_pin_dataranges_ks"></span><span id="DDK_KSPROPERTY_PIN_DATARANGES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列64位对齐的<a href="https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))"><strong>KSDATARANGE</strong></a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 KSP\_PIN 指定此属性，其中**PinId**成员指定要为其返回可接受数据范围的 PIN 工厂。

KS 筛选器返回由 pin 工厂实例化的 pin 支持的所有数据范围。 KS 筛选器可能不支持在其当前内部状态中报告的数据区域。 若要确定当前内部状态支持的数据范围，请使用[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性以查询详细信息。

有关详细信息，请参阅[KS 数据格式和数据区域](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)。

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

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

 

 






