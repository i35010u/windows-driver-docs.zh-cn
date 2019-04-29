---
title: KSPROPERTY\_EXTDEVICE\_POWER\_STATE
description: KSPROPERTY\_EXTDEVICE\_电源\_STATE 属性设置或获取外部设备的电源状态。
ms.assetid: bfca1f3d-b563-4ddd-b823-85487b4a4093
keywords:
- KSPROPERTY_EXTDEVICE_POWER_STATE 流式处理媒体设备
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
ms.openlocfilehash: b19bb4dbaeb35dd53d085ae465526795b2f4451c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373377"
---
# <a name="kspropertyextdevicepowerstate"></a>KSPROPERTY\_EXTDEVICE\_POWER\_STATE


KSPROPERTY\_EXTDEVICE\_电源\_STATE 属性设置或获取外部设备的电源状态。

## <span id="ddk_ksproperty_extdevice_power_state_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_POWER_STATE_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565156" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565156)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为的 ULONG 的指定外部设备的电源状态。

<a name="remarks"></a>备注
-------

**PowerState** KSPROPERTY 成员\_EXTDEVICE\_S 结构指定外部设备的电源设置。 **PowerState**成员可能会设置为等于上或备用。 例如，可能会关闭电源的电池供电的外部设备，如 DV 摄像机。 AC 电源 DVHS 设备将会放入待机状态。 如果设备处于待机状态，可能会提供支持在更高版本。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTDEVICE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565156)

 

 






