---
title: KSPROPERTY \_ PIN \_ 接口
description: 此属性返回由特定的 pin 工厂实例化的 pin 支持的接口列表。
ms.assetid: 5a49c685-d086-4827-87a3-67d1fa80452a
keywords:
- KSPROPERTY_PIN_INTERFACES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_INTERFACES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23e957e2992522569f255a6f35cfe7e2ca01a7a1
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103548"
---
# <a name="ksproperty_pin_interfaces"></a>KSPROPERTY \_ PIN \_ 接口


此属性返回由特定的 pin 工厂实例化的 pin 支持的接口列表。

## <span id="ddk_ksproperty_pin_interfaces_ks"></span><span id="DDK_KSPROPERTY_PIN_INTERFACES_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列<a href="/previous-versions/ff563537(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_INTERFACE&lt;/strong&gt;](/previous-versions/ff563537(v=vs.85))"><strong>KSPIN_INTERFACE</strong></a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

\_ \_ 使用 KSP PIN 指定 KSPROPERTY pin 接口 \_ ，其中**PinId**成员指定要为其返回可用接口的 pin 工厂。

此属性返回按类驱动程序首选项排序的接口。

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

[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSPIN \_ 接口**](/previous-versions/ff563537(v=vs.85))

