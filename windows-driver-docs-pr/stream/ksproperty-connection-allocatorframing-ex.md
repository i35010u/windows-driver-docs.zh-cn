---
title: KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX
description: AVStream 客户端使用 KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX 属性来确定 pin 的帧需求。
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54a2462a2e9a496fab1214acabc484778ae92ec1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829139"
---
# <a name="ksproperty_connection_allocatorframing_ex"></a>KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX


AVStream 客户端使用 KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX 属性来确定 pin 的帧需求。

## <span id="ddk_ksproperty_connection_allocatorframing_ex_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING_EX&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)"><strong>KSALLOCATOR_FRAMING_EX</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回 [**KSALLOCATOR \_ 组帧， \_ 如**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)描述 AVStream pin 的组帧要求。

在 stream 类下运行的微型驱动程序应使用 [**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)。

请参阅 [KS 分配器](./ks-allocators.md)。 和 [AVStream 分配器](./avstream-allocators.md)。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSALLOCATOR \_ 组帧 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)

