---
title: KSPROPERTY\_BDA\_传输\_模式
description: 客户端使用 KSPROPERTY\_BDA\_传输\_模式来控制如何传输广播信号的解调器节点上的设置。
ms.assetid: 8d49a45f-031f-445f-ae2e-d98223a7d524
keywords:
- KSPROPERTY_BDA_TRANSMISSION_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TRANSMISSION_MODE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20e742d0c4dc53e66df89e238b19cadff0623f28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843594"
---
# <a name="ksproperty_bda_transmission_mode"></a>KSPROPERTY\_BDA\_传输\_模式


客户端使用 KSPROPERTY\_BDA\_传输\_模式来控制如何传输广播信号的解调器节点上的设置。

## <span id="ddk_ksproperty_bda_transmission_mode_ks"></span><span id="DDK_KSPROPERTY_BDA_TRANSMISSION_MODE_KS"></span>


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
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>TransmissionMode</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

TransmissionMode 枚举类型返回的值标识了如何传输广播信号的设置。

KSP\_**节点的节点**标识号指定了解调器节点的标识符。

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


[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**TransmissionMode**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/transmissionmode)

 

 






