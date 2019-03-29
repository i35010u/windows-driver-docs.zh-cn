---
title: KSPROPERTY\_连接\_ALLOCATORFRAMING
description: 在流类模型中，客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING 属性来确定组帧 pin 的要求。
ms.assetid: 02cacade-938b-4fab-928f-75f790692324
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING 流式处理媒体设备
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
ms.openlocfilehash: 5a6f14e3a8ae50daaacfb47f466fa340789730d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566150"
---
# <a name="kspropertyconnectionallocatorframing"></a>KSPROPERTY\_连接\_ALLOCATORFRAMING


在流类模型中，客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING 属性来确定组帧 pin 的要求。

## <span id="ddk_ksproperty_connection_allocatorframing_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560979" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560979)"><strong>KSALLOCATOR_FRAMING</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回[ **KSALLOCATOR\_组帧**](https://msdn.microsoft.com/library/windows/hardware/ff560979)，其中描述了 pin 的组帧需求。 例如， **FrameSize**成员的插针指定数据的帧大小。

AVStream 微型驱动程序应使用[ **KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX**](ksproperty-connection-allocatorframing-ex.md)。

请参阅[KS 分配器](https://msdn.microsoft.com/library/windows/hardware/ff567257)。 并[AVStream 分配器](https://msdn.microsoft.com/library/windows/hardware/ff554202)。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSALLOCATOR\_FRAMING**](https://msdn.microsoft.com/library/windows/hardware/ff560979)

 

 






