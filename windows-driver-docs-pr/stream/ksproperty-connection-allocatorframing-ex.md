---
title: KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX
description: AVStream 客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX 属性来确定 pin 的帧需求。
ms.assetid: 7ff1462f-959b-413e-a888-bcf7d251edee
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
ms.openlocfilehash: ad41468c03ec8b8e1a0ff5b528ea41b191c8e707
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826831"
---
# <a name="ksproperty_connection_allocatorframing_ex"></a>KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX


AVStream 客户端使用 KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX 属性来确定 pin 的帧需求。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING_EX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)"><strong>KSALLOCATOR_FRAMING_EX</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回[**KSALLOCATOR\_组帧\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)，其中描述了 AVStream pin 的组帧要求。

在 stream 类下运行的微型驱动程序应使用[**KSPROPERTY\_连接\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)。

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


[**KSALLOCATOR\_组帧\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)

 

 






