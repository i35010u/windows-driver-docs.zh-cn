---
title: KSPROPERTY \_ EXTDEVICE \_ ID
description: KSPROPERTY \_ EXTDEVICE \_ id 属性检索外部设备通用化系统范围内的 id。
keywords:
- KSPROPERTY_EXTDEVICE_ID 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_ID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e631a510f3bd85cbaece8a1e76051c61e976b56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839352"
---
# <a name="ksproperty_extdevice_id"></a>KSPROPERTY \_ EXTDEVICE \_ ID


KSPROPERTY \_ EXTDEVICE \_ id 属性检索外部设备通用化系统范围内的 id。

## <span id="ddk_ksproperty_extdevice_id_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_ID_KS"></span>


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
<td><p>DWORD 数组</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是一个 DWORD 数组，用于指定外部设备的唯一节点 Id

<a name="remarks"></a>备注
-------

KSPROPERTY **NodeUniqueID** \_ EXTDEVICE S 结构的 NodeUniqueID 成员 \_ 指定外部设备的唯一节点 Id。

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

