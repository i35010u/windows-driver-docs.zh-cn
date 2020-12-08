---
title: KSPROPERTY \_ BDA \_ LNB \_ 交换机 \_ 频率
description: 客户端使用 KSPROPERTY \_ BDA \_ LNB \_ SWITCH \_ frequency 来通知 rf 调谐器节点有关的传入 RF 信号的频率，调谐器应通过这些信号通知低干扰块 (LNB) 设备在 LNB 转移 RF 信号的频率时，通过使用带外)  (，反之亦然，反之亦然。
keywords:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68b1a82b149aff660a526b8a4d9a75e452ac6ae4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795317"
---
# <a name="ksproperty_bda_lnb_switch_frequency"></a>KSPROPERTY \_ BDA \_ LNB \_ 交换机 \_ 频率


客户端使用 KSPROPERTY \_ BDA \_ LNB \_ SWITCH \_ frequency 来通知 rf 调谐器节点有关的传入 RF 信号的频率，调谐器应通过这些信号通知低干扰块 (LNB) 设备在 LNB 转移 RF 信号的频率时，通过使用带外)  (，反之亦然，反之亦然。

## <span id="ddk_ksproperty_bda_lnb_switch_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点标识号指定了 RF 调谐器节点的标识符。

属性值指定传入 RF 信号的频率，LNB 应从该频率切换到使用带外的 LOF 来使用带内的 LOF。

如果客户端发送 KSPROPERTY \_ BDA \_ 射频 \_ 调谐器 \_ 频率请求，以将射频调谐器调整到特定的频率，此频率大于或等于使用 KSPROPERTY BDA LNB 切换频率指定的切换频率，则 \_ \_ \_ \_ RF 调谐器应将命令发送到 LNB 以切换到带内的 LOF。 然后，RF 调谐器会预计 LNB 设备会将传入 RF 信号的频率转移到使用 KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层指定的高密度 LOF \_ 。

同样，如果客户端发送 KSPROPERTY \_ BDA \_ 射频 \_ 调谐器 \_ 频率请求以将 RF 调谐器调整到特定的频率，而此频率小于交换机频率，则 RF 调谐器应将命令发送到 LNB 以切换到低区 LOF。 然后，RF 调谐器会预计 LNB 设备会将传入 RF 信号的频率转移到使用 KSPROPERTY \_ BDA \_ LNB \_ LOF \_ low 指定的低带 LOF 量 \_ 。

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

[**KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层 \_**](ksproperty-bda-lnb-lof-high-band.md)

[**KSPROPERTY \_ BDA \_ LNB \_ LOF \_ LOW \_**](ksproperty-bda-lnb-lof-low-band.md)

[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率**](ksproperty-bda-rf-tuner-frequency.md)

 

