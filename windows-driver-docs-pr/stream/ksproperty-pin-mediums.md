---
title: KSPROPERTY \_ PIN \_ 媒体
description: 此属性返回由特定的 pin 工厂实例化的 pin 支持的媒体列表。
keywords:
- KSPROPERTY_PIN_MEDIUMS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_MEDIUMS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18db051e44343ed5b531b6fb2e3624825ceeebfb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823697"
---
# <a name="ksproperty_pin_mediums"></a>KSPROPERTY \_ PIN \_ 媒体


此属性返回由特定的 pin 工厂实例化的 pin 支持的媒体列表。

## <span id="ddk_ksproperty_pin_mediums_ks"></span><span id="DDK_KSPROPERTY_PIN_MEDIUMS_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列<a href="/previous-versions/ff563538(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](/previous-versions/ff563538(v=vs.85))"><strong>KSPIN_MEDIUM</strong></a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

客户端使用此属性来请求由 pin 工厂实例化的 pin 支持的所有媒体的列表。 然后，客户端指定要在连接到 pin 时使用的实际媒介。

使用 KSP PIN 指定此属性 \_ ，其中成员指定要为其返回媒体列表的 PIN 工厂。

KSPROPERTY \_ PIN \_ 媒体返回按类驱动程序首选项排序的媒体。

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

## <a name="see-also"></a>请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSPIN \_ 中型**](/previous-versions/ff563538(v=vs.85))

