---
title: KSPROPERTY\_BDA\_PIN\_类型
description: 客户端使用 KSPROPERTY\_BDA\_PIN\_类型来检索指定 PIN 类型的值。
ms.assetid: 3d2a976b-67ff-4469-aa96-7aa8bd5f229e
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
ms.openlocfilehash: a8b2db83db07dc62fc1db06d8a65e653852a8759
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827455"
---
# <a name="ksproperty_bda_pin_type"></a>KSPROPERTY\_BDA\_PIN\_类型


客户端使用 KSPROPERTY\_BDA\_PIN\_类型来检索指定 PIN 类型的值。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定 pin 类型。

当网络提供程序使用 KSMETHOD 创建用于筛选器的 pin\_BDA\_创建\_PIN\_工厂时，它从包含在筛选器的 "BDA" 模板拓扑中的 pin 类型列表中指定 pin 类型。 KSPROPERTY\_BDA\_PIN\_类型返回此 PIN 类型。 在筛选器的 BDA 模板拓扑中，每个 pin 类型只能出现一次，但它可以在实际拓扑中出现多次。 固定类型的值对应于从零开始的固定类型数组中的元素的索引。 此类型的 pin 类型是 KSPIN\_描述符\_EX 结构的数组。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSMETHOD\_BDA\_创建\_PIN\_工厂**](ksmethod-bda-create-pin-factory.md)

[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






