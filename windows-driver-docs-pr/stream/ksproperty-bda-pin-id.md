---
title: KSPROPERTY\_BDA\_PIN\_ID
description: 客户端使用 KSPROPERTY\_BDA\_PIN\_ID 检索 pin 的 BDA 标识符（ID）。
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
ms.openlocfilehash: 8b7484e2541624da3e5677bb00a9c3e4f99791a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837609"
---
# <a name="ksproperty_bda_pin_id"></a>KSPROPERTY\_BDA\_PIN\_ID


客户端使用 KSPROPERTY\_BDA\_PIN\_ID 检索 pin 的 BDA 标识符（ID）。

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

返回的值指定 pin ID。

当网络提供程序使用 KSMETHOD 创建用于筛选器的 pin 时\_BDA\_创建\_PIN\_工厂，则该筛选器的 BDA 微型驱动程序将提供 pin ID。 KSPROPERTY\_BDA\_PIN\_ID 返回此 ID。

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

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






