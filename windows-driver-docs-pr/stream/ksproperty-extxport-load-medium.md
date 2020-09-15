---
title: KSPROPERTY \_ EXTXPORT \_ LOAD \_ MEDIUM
description: KSPROPERTY \_ EXTXPORT \_ load \_ medium 属性设置或获取外部设备的负载介质。 例如，弹出、打开托盘、关闭纸盒等。
ms.assetid: 13ec61ae-4be7-4af6-875f-a6ca178cf6bc
keywords:
- KSPROPERTY_EXTXPORT_LOAD_MEDIUM 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_LOAD_MEDIUM
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3dd10cc7047a3f77fbaedd1a4c920f6628beb10
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101430"
---
# <a name="ksproperty_extxport_load_medium"></a>KSPROPERTY \_ EXTXPORT \_ LOAD \_ MEDIUM


KSPROPERTY \_ EXTXPORT \_ load \_ medium 属性设置或获取外部设备的负载介质。 例如，弹出、打开托盘、关闭纸盒等。

## <span id="ddk_ksproperty_extxport_load_medium_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_LOAD_MEDIUM_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定当前负载介质的 ULONG。 例如，弹出，打开托盘或关闭的纸盒。

<a name="remarks"></a>备注
-------

KSPROPERTY **LoadMedium** \_ EXTXPORT S 结构的 LoadMedium 成员 \_ 指定负载介质。

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

