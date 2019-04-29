---
title: KSPROPERTY\_CONNECTION\_ALLOCATORFRAMING\_EX
description: AVStream 客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX 属性来确定组帧 pin 的要求。
ms.assetid: 7ff1462f-959b-413e-a888-bcf7d251edee
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX 流式处理媒体设备
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
ms.openlocfilehash: 373605c1fded851941d3049f1e487c2e690efd87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376091"
---
# <a name="kspropertyconnectionallocatorframingex"></a>KSPROPERTY\_CONNECTION\_ALLOCATORFRAMING\_EX


AVStream 客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX 属性来确定组帧 pin 的要求。

## <span id="ddk_ksproperty_connection_allocatorframing_ex_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560982" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560982)"><strong>KSALLOCATOR_FRAMING_EX</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回[ **KSALLOCATOR\_组帧\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff560982)，其中描述了 AVStream pin 的组帧需求。

流类下运行的微型驱动程序应使用[ **KSPROPERTY\_连接\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)。

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


[**KSALLOCATOR\_FRAMING\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff560982)

 

 






