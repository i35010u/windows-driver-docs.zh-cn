---
title: KSPROPERTY\_BDA\_PIN\_TYPE
description: 客户端使用 KSPROPERTY\_BDA\_PIN\_类型来检索用于指定 pin 的类型的值。
ms.assetid: 3d2a976b-67ff-4469-aa96-7aa8bd5f229e
keywords:
- KSPROPERTY_BDA_PIN_TYPE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b776208930c94c6873138fd9928035c635fc7cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525563"
---
# <a name="kspropertybdapintype"></a>KSPROPERTY\_BDA\_PIN\_TYPE


客户端使用 KSPROPERTY\_BDA\_PIN\_类型来检索用于指定 pin 的类型的值。

## <span id="ddk_ksproperty_bda_pin_type_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_TYPE_KS"></span>


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
<td><p>Pin</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定 pin 类型。

当网络提供商创建筛选器使用 KSMETHOD pin\_BDA\_创建\_PIN\_工厂，它指定筛选器的 BDA 模板拓扑中包含的 pin 类型列表中 pin 类型。 KSPROPERTY\_BDA\_PIN\_类型返回此 pin 类型。 在筛选器的 BDA 模板拓扑中每个 pin 类型可仅出现一次，但它可在实际的拓扑结构中出现多次。 Pin 类型的值对应于 pin 类型的从零开始的数组中元素的索引。 此 pin 类型的数组是一个数组 KSPIN\_描述符\_EX 结构。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSMETHOD\_BDA\_创建\_PIN\_工厂**](ksmethod-bda-create-pin-factory.md)

[**KSPIN\_描述符\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






