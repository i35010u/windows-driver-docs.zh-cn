---
title: KSPROPERTY \_ 常规 \_ 组件 ID
description: KSPROPERTY \_ 常规组件 \_ id 属性是一个可选属性，它允许客户端访问存储在 KSCOMPONENTID 结构中的常规组件信息。
ms.assetid: fbbdf3f6-c71a-4a6d-ba15-ec7b7bdc1e0e
keywords:
- KSPROPERTY_GENERAL_COMPONENTID 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_GENERAL_COMPONENTID
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d96b5d80fb3f0fb7bd741ad83c6455f0b9384d5a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189993"
---
# <a name="ksproperty_general_componentid"></a>KSPROPERTY \_ 常规 \_ 组件 ID


KSPROPERTY \_ 常规组件 \_ id 属性是一个可选属性，它允许客户端访问存储在 [**KSCOMPONENTID**](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid) 结构中的常规组件信息。

## <span id="ddk_ksproperty_general_componentid_ks"></span><span id="DDK_KSPROPERTY_GENERAL_COMPONENTID_KS"></span>


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
<td><p>筛选器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

[**KSCOMPONENTID**](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)结构包含**制造商**、**产品**、**组件**和**名称**的 GUID 值。 它包含版本和修订**版本**的**Revision**ULONG 值。

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


[**KSCOMPONENTID**](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)

 

