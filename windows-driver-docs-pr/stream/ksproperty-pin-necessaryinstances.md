---
title: KSPROPERTY \_ PIN \_ NECESSARYINSTANCES
description: 此属性返回 pin 工厂在筛选器可执行 i/o 操作之前必须实例化的最小 pin 数。
ms.assetid: d30d7546-3d16-42df-b640-a8ec37bca35c
keywords:
- KSPROPERTY_PIN_NECESSARYINSTANCES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NECESSARYINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3aa1219daadf2594c5be455824fc32f6f3b4cf8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192837"
---
# <a name="ksproperty_pin_necessaryinstances"></a>KSPROPERTY \_ PIN \_ NECESSARYINSTANCES


此属性返回 pin 工厂在筛选器可执行 i/o 操作之前必须实例化的最小 pin 数。

## <span id="ddk_ksproperty_pin_necessaryinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_NECESSARYINSTANCES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

使用 KSP pin 指定此属性 \_ ，其中成员指定相关的 PIN 工厂。

KSPROPERTY \_ pin \_ NECESSARYINSTANCES 返回类型为 ULONG 的值，指定 pin 工厂必须实例化的最小 pin 数。

类驱动程序不处理此属性;stream 微型驱动程序必须自行提供处理。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

