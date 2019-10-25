---
title: KSPROPERTY\_连接\_ALLOCATORFRAMING
description: 在 stream 类模型中，客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING 属性来确定 pin 的帧需求。
ms.assetid: 02cacade-938b-4fab-928f-75f790692324
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
ms.openlocfilehash: 7176f4ea607ecd0f03dbd5ab317a67bb050747b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826804"
---
# <a name="ksproperty_connection_allocatorframing"></a>KSPROPERTY\_连接\_ALLOCATORFRAMING


在 stream 类模型中，客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING 属性来确定 pin 的帧需求。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)"><strong>KSALLOCATOR_FRAMING</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回[**KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)，该框架描述了 pin 的组帧要求。 例如， **FrameSize**成员指定 pin 上数据的帧大小。

AVStream 微型驱动程序应该使用[**KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX**](ksproperty-connection-allocatorframing-ex.md)

请参阅[KS 分配器](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-allocators)。 和[AVStream 分配器](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-allocators)。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)

 

 






