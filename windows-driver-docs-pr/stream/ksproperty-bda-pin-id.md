---
title: KSPROPERTY \_ BDA \_ PIN \_ ID
description: 客户端使用 KSPROPERTY \_ bda \_ pin \_ id 检索 PIN)  (ID 的 bda 标识符。
ms.assetid: 6f7a4454-1294-4646-8e21-bfec9a14b612
keywords:
- KSPROPERTY_BDA_PIN_ID 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_ID
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 472fdcf4d0cf853ebe6a4b7048fe8bfe9e54314e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188373"
---
# <a name="ksproperty_bda_pin_id"></a>KSPROPERTY \_ BDA \_ PIN \_ ID


客户端使用 KSPROPERTY \_ bda \_ pin \_ id 检索 PIN)  (ID 的 bda 标识符。

## <span id="ddk_ksproperty_bda_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_ID_KS"></span>


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

 

<a name="remarks"></a>注解
-------

返回的值指定 pin ID。

当网络提供商为使用 KSMETHOD BDA 创建 pin 工厂的筛选器创建 pin 时 \_ \_ ，该 \_ \_ 筛选器的 BDA 微型驱动程序将为该筛选器提供 pin ID。 KSPROPERTY \_ BDA \_ PIN \_ ID 返回此 id。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSMETHOD \_ BDA \_ 创建 \_ PIN \_ 工厂**](ksmethod-bda-create-pin-factory.md)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

