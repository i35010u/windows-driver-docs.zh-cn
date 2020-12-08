---
title: KSPROPERTY \_ BDA \_ 传输 \_ 模式
description: 客户端使用 KSPROPERTY \_ BDA \_ 传输 \_ 模式来控制如何传输广播信号的解调器节点上的设置。
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
ms.openlocfilehash: 1a74b2e7102168892a85cd61c7c630c7509ebb7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839197"
---
# <a name="ksproperty_bda_transmission_mode"></a>KSPROPERTY \_ BDA \_ 传输 \_ 模式


客户端使用 KSPROPERTY \_ BDA \_ 传输 \_ 模式来控制如何传输广播信号的解调器节点上的设置。

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
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p>TransmissionMode</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

TransmissionMode 枚举类型返回的值标识了如何传输广播信号的设置。

KSP **NodeId** \_ 节点的节点标识号指定了解调器节点的标识符。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**TransmissionMode**](/previous-versions/windows/desktop/mstv/transmissionmode)

 

