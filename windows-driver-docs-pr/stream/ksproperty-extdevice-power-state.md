---
title: KSPROPERTY \_ EXTDEVICE \_ 电源 \_ 状态
description: KSPROPERTY \_ EXTDEVICE \_ 电源 \_ 状态属性设置或获取外部设备的电源状态。
keywords:
- KSPROPERTY_EXTDEVICE_POWER_STATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_POWER_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8503d94e742d0aadb2b27c9a018e5f4d0a3d02e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795303"
---
# <a name="ksproperty_extdevice_power_state"></a>KSPROPERTY \_ EXTDEVICE \_ 电源 \_ 状态


KSPROPERTY \_ EXTDEVICE \_ 电源 \_ 状态属性设置或获取外部设备的电源状态。

## <span id="ddk_ksproperty_extdevice_power_state_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_POWER_STATE_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个指定外部设备的电源状态的 ULONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **PowerState** \_ EXTDEVICE S 结构的 PowerState 成员 \_ 指定外部设备的电源设置。 **PowerState** 成员可能设置为等于 "开" 或 "待机"。 例如，备有电池的外部设备（如 DV 摄像机）可能会关闭。 接通电源的 DVHS 设备可能会置于备用状态。 如果设备处于备用状态，则可能会在以后对其通电。

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

[**KSPROPERTY \_ EXTDEVICE \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

