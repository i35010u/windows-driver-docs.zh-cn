---
title: KSPROPERTY \_ EXTXPORT \_ 状态
description: KSPROPERTY \_ EXTXPORT \_ 状态属性设置或获取外部设备的传输模式和状态。
keywords:
- KSPROPERTY_EXTXPORT_STATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37f08fbf9e53a8811de0ea10fff8f2f2cce347ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782021"
---
# <a name="ksproperty_extxport_state"></a>KSPROPERTY \_ EXTXPORT \_ 状态


KSPROPERTY \_ EXTXPORT \_ 状态属性设置或获取外部设备的传输模式和状态。

## <span id="ddk_ksproperty_extxport_state_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_KS"></span>


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
<td><p>是</p></td>
<td><p>设备</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state" data-raw-source="[&lt;strong&gt;TRANSPORT_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state)"><strong>TRANSPORT_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个传输 \_ 状态结构，用于描述外部传输的当前模式和状态。 例如，当模式设置为 "播放" 时，状态可能设置为 "冻结" (暂停) 。

<a name="remarks"></a>备注
-------

KSPROPERTY **XPrtState** \_ EXTXPORT S 结构的 XPrtState 成员 \_ 指定模式和状态。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

[**传输 \_ 状态**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state)

