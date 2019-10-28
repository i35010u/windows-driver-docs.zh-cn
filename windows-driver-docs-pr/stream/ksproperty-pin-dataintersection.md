---
title: KSPROPERTY\_PIN\_DATAINTERSECTION
description: 客户端使用 KSPROPERTY\_PIN\_DATAINTERSECTION 属性来查找 pin 工厂实例化的 pin 支持的数据格式。 客户端提供数据格式列表;KS 筛选器返回支持的列表中的第一个数据格式。
ms.assetid: 447ac37b-1e5e-4812-9e1e-50e9f6f83118
keywords:
- KSPROPERTY_PIN_DATAINTERSECTION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATAINTERSECTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77145aa74df7f51f1d984c924f4cd542d1ee8e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838859"
---
# <a name="ksproperty_pin_dataintersection"></a>KSPROPERTY\_PIN\_DATAINTERSECTION


客户端使用 KSPROPERTY\_PIN\_DATAINTERSECTION 属性来查找 pin 工厂实例化的 pin 支持的数据格式。 客户端提供数据格式列表;KS 筛选器返回支持的列表中的第一个数据格式。

## <span id="ddk_ksproperty_pin_dataintersection_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAINTERSECTION_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要指定此属性，请提供一个[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)结构，后跟[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)结构和64位对齐[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构的序列。 **KSP\_pin**的**PinId**成员指定了 pin 工厂。

此属性从客户端提供的列表中返回第一个匹配的数据格式。

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

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

 

 






