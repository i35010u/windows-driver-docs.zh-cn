---
title: KSPROPERTY \_ EXTDEVICE \_ 功能
description: KSPROPERTY \_ EXTDEVICE \_ 功能属性检索外部设备的功能。
ms.assetid: c408b4cf-2fd9-41b2-b182-47baa551fd93
keywords:
- KSPROPERTY_EXTDEVICE_CAPABILITIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b99d34101a69ab4f49462c1d57a501495a5722a2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104558"
---
# <a name="ksproperty_extdevice_capabilities"></a>KSPROPERTY \_ EXTDEVICE \_ 功能


KSPROPERTY \_ EXTDEVICE \_ 功能属性检索外部设备的功能。

## <span id="ddk_ksproperty_extdevice_capabilities_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_CAPABILITIES_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagdevcaps" data-raw-source="[&lt;strong&gt;DEVCAPS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagdevcaps)"><strong>DEVCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是描述外部设备功能的 DEVCAPS 结构。

<a name="remarks"></a>注解
-------

KSPROPERTY **Capabilities** \_ EXTDEVICE S 结构的功能成员 \_ 指定了外部设备的功能。

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

[**KSPROPERTY \_ EXTDEVICE \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

[**DEVCAPS**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagdevcaps)

