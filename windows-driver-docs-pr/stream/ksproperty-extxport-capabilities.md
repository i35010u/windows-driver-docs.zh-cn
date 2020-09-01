---
title: KSPROPERTY \_ EXTXPORT \_ 功能
description: KSPROPERTY \_ EXTXPORT \_ 功能属性检索外部设备的传输特定功能。
ms.assetid: 5394d05c-0c3e-4413-a61e-21445117a350
keywords:
- KSPROPERTY_EXTXPORT_CAPABILITIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7903f1595a33563e29e9594df82db4fdb9af05e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190491"
---
# <a name="ksproperty_extxport_capabilities"></a>KSPROPERTY \_ EXTXPORT \_ 功能


KSPROPERTY \_ EXTXPORT \_ 功能属性检索外部设备的传输特定功能。

## <span id="ddk_ksproperty_extxport_capabilities_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_CAPABILITIES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个指定外部传输功能的 ULONG。

<a name="remarks"></a>注解
-------

KSPROPERTY EXTXPORT 结构的 **功能** 成员 \_ \_ 介绍了传输特定的功能。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

