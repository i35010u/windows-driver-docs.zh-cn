---
title: KSPROPERTY\_BDA\_PIN\_ID
description: 客户端使用 KSPROPERTY\_BDA\_PIN\_ID 来检索 pin 的 BDA 标识符 (ID)。
ms.assetid: 6f7a4454-1294-4646-8e21-bfec9a14b612
keywords:
- KSPROPERTY_BDA_PIN_ID 流式处理媒体设备
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
ms.openlocfilehash: 14ee22245d287a47508005fdfed2353e8e078b7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390550"
---
# <a name="kspropertybdapinid"></a>KSPROPERTY\_BDA\_PIN\_ID


客户端使用 KSPROPERTY\_BDA\_PIN\_ID 来检索 pin 的 BDA 标识符 (ID)。

## <span id="ddk_ksproperty_bda_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_ID_KS"></span>


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

返回的值指定 pin id。

当网络提供商创建筛选器使用 KSMETHOD pin\_BDA\_创建\_PIN\_工厂，BDA 微型驱动程序的筛选器，使该 pin id。 KSPROPERTY\_BDA\_PIN\_ID 返回此 id。

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


[**KSMETHOD\_BDA\_创建\_PIN\_工厂**](ksmethod-bda-create-pin-factory.md)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






