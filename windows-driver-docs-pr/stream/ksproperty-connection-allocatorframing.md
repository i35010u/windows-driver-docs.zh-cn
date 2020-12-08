---
title: KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING
description: 在 stream 类模型中，客户端使用 KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING 属性来确定 pin 的帧需求。
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da2df0eed44adad7e5f9244ca6a48acbee8cb82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837845"
---
# <a name="ksproperty_connection_allocatorframing"></a>KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING


在 stream 类模型中，客户端使用 KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING 属性来确定 pin 的帧需求。

## <span id="ddk_ksproperty_connection_allocatorframing_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)"><strong>KSALLOCATOR_FRAMING</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性将返回 [**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)，其中描述了 pin 的组帧要求。 例如， **FrameSize** 成员指定 pin 上数据的帧大小。

AVStream 微型驱动程序应使用 [**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX**](ksproperty-connection-allocatorframing-ex.md)

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


[**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)

