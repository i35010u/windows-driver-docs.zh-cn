---
title: KSPROPERTY\_BDA\_PIN\_TYPES
description: 客户端使用 KSPROPERTY\_BDA\_PIN\_类型来检索固定类型的列表。
ms.assetid: de11ab3c-a787-4831-aad4-e97f46432032
keywords:
- KSPROPERTY_BDA_PIN_TYPES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_TYPES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bad1b911e3a2210cf964163b307fb766e94382a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368121"
---
# <a name="kspropertybdapintypes"></a>KSPROPERTY\_BDA\_PIN\_TYPES


客户端使用 KSPROPERTY\_BDA\_PIN\_类型来检索固定类型的列表。

## <span id="ddk_ksproperty_bda_pin_types_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_TYPES_KS"></span>


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
<td><p>KSPROPERTY</p></td>
<td><p>KSPIN_DESCRIPTOR_EXs 的列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在模板拓扑中每个 pin 类型可仅出现一次，但它可在实际的拓扑结构中出现多次。 此 pin 类型列表是一个数组 KSPIN\_描述符\_EX 结构。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BdaPropertyPinTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertypintypes)

[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






