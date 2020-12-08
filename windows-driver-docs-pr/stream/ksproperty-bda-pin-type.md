---
title: KSPROPERTY \_ BDA \_ PIN \_ 类型
description: 客户端使用 KSPROPERTY \_ BDA \_ pin \_ 类型检索指定 PIN 类型的值。
keywords:
- KSPROPERTY_BDA_PIN_TYPE 流媒体设备
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
ms.openlocfilehash: 0f4e6b6e6d611e54b1c07a5a3e7c51ba52fe5835
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793339"
---
# <a name="ksproperty_bda_pin_type"></a>KSPROPERTY \_ BDA \_ PIN \_ 类型


客户端使用 KSPROPERTY \_ BDA \_ pin \_ 类型检索指定 PIN 类型的值。

## <span id="ddk_ksproperty_bda_pin_type_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_TYPE_KS"></span>


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
<td><p>Pin</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定 pin 类型。

当网络提供商使用 KSMETHOD BDA 创建 pin 工厂为某个筛选器创建 pin 时 \_ \_ \_ \_ ，它将从该筛选器的 "bda 模板" 拓扑中包含的 pin 类型列表中指定 pin 类型。 KSPROPERTY \_ BDA \_ pin \_ 类型返回此 PIN 类型。 在筛选器的 BDA 模板拓扑中，每个 pin 类型只能出现一次，但它可以在实际拓扑中出现多次。 固定类型的值对应于从零开始的固定类型数组中的元素的索引。 此类型的 pin 类型是 KSPIN \_ 描述符 \_ EX 结构的数组。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSMETHOD \_ BDA \_ 创建 \_ PIN \_ 工厂**](ksmethod-bda-create-pin-factory.md)

[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

