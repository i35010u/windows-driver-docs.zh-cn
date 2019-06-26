---
title: KSPROPERTY\_常规\_COMPONENTID
description: KSPROPERTY\_常规\_COMPONENTID 属性是可选属性，允许客户端以访问 KSCOMPONENTID 结构中存储的常规组件信息。
ms.assetid: fbbdf3f6-c71a-4a6d-ba15-ec7b7bdc1e0e
keywords:
- KSPROPERTY_GENERAL_COMPONENTID 流式处理媒体设备
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
ms.openlocfilehash: 866414c5c0ded0200ac59971e9425a57af2134c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354820"
---
# <a name="kspropertygeneralcomponentid"></a>KSPROPERTY\_常规\_COMPONENTID


KSPROPERTY\_常规\_COMPONENTID 属性是可选属性，允许访问常规组件信息存储在客户端[ **KSCOMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)结构。

## <span id="ddk_ksproperty_general_componentid_ks"></span><span id="DDK_KSPROPERTY_GENERAL_COMPONENTID_KS"></span>


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
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[ **KSCOMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)结构包含的 GUID 值**制造商**，**产品**，**组件**，并**名称**。 它包含 ULONG 值**版本**并**修订**。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSCOMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)

 

 






