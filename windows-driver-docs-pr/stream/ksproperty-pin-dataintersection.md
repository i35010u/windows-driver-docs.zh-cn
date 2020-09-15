---
title: KSPROPERTY \_ PIN \_ DATAINTERSECTION
description: 客户端使用 KSPROPERTY \_ 引脚 \_ DATAINTERSECTION 属性查找 pin 工厂实例化的 pin 支持的数据格式。 客户端提供数据格式列表;KS 筛选器返回支持的列表中的第一个数据格式。
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
ms.openlocfilehash: 33e9dec8535c3d4be6a834a2a1256136da0a4833
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103722"
---
# <a name="ksproperty_pin_dataintersection"></a>KSPROPERTY \_ PIN \_ DATAINTERSECTION


客户端使用 KSPROPERTY \_ 引脚 \_ DATAINTERSECTION 属性查找 pin 工厂实例化的 pin 支持的数据格式。 客户端提供数据格式列表;KS 筛选器返回支持的列表中的第一个数据格式。

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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要指定此属性，请提供 [**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) 结构，后跟 [**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item) 结构和64位对齐的 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构的序列。 **KSP \_ Pin**的**PinId**成员指定了 PIN 工厂。

此属性从客户端提供的列表中返回第一个匹配的数据格式。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性以查询详细信息。

有关详细信息，请参阅 [KS 数据格式和数据区域](./ks-data-formats-and-data-ranges.md)。

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

[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))

[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

