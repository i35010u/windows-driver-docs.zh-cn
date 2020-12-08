---
title: KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知
description: KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知属性设置或获取传输模式和状态更改的通知。
keywords:
- KSPROPERTY_EXTXPORT_STATE_NOTIFY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE_NOTIFY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00247a5da2a7bef4ad529a8e1a2ca3700b6e4a16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782024"
---
# <a name="ksproperty_extxport_state_notify"></a>KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知


KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知属性设置或获取传输模式和状态更改的通知。

## <span id="ddk_ksproperty_extxport_state_notify_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_NOTIFY_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是在 \_ \_ 传输状态发生更改时描述当前外部传输的 KSPROPERTY EXTXPORT S 结构。

<a name="remarks"></a>备注
-------

\_ \_ 当传输状态发生更改时，KSPROPERTY EXTXPORT S 结构将收到通知。

此调用是一个同步操作，将不会返回，直到传输状态发生更改。 不建议使用此方法，因为并非所有 DV 摄像机都可以支持此操作。

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

