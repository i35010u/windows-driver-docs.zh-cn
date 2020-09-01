---
title: KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知
description: KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知属性设置或获取传输模式和状态更改的通知。
ms.assetid: 3ebf3806-bdec-4ea2-8f2a-e75314ee020a
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
ms.openlocfilehash: 2c13c454df0c863eea69225708db90fde5ef7138
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191061"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

