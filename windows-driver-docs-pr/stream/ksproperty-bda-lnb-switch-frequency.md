---
title: KSPROPERTY\_BDA\_LNB\_交换机\_频率
description: 客户端使用 KSPROPERTY\_BDA\_LNB\_交换机\_频率，通知 RF 调谐器节点有关传入 RF 信号的频率，调谐器应使用该频率通知低噪音块（LNB）设备从使用下到下当 LNB 改变 RF 信号的频率时，震荡 frequency （LOF）使用双频 LOF，反之亦然。
ms.assetid: a448bad1-40dc-4596-bc18-9522144e33a7
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
ms.openlocfilehash: b4b409e9248bf0bb63b62bf3adceeb2d34d5eadf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845146"
---
# <a name="ksproperty_bda_lnb_switch_frequency"></a>KSPROPERTY\_BDA\_LNB\_交换机\_频率


客户端使用 KSPROPERTY\_BDA\_LNB\_交换机\_频率，通知 RF 调谐器节点有关传入 RF 信号的频率，调谐器应使用该频率通知低噪音块（LNB）设备从使用下到下当 LNB 改变 RF 信号的频率时，震荡 frequency （LOF）使用双频 LOF，反之亦然。

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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识指定 RF 调谐器节点的标识符。

属性值指定传入 RF 信号的频率，LNB 应从该频率切换到使用带外的 LOF 来使用带内的 LOF。

如果客户端发送 KSPROPERTY\_BDA\_RF\_调谐器\_频率请求，以将 RF 调谐器调整到特定频率，此频率大于或等于使用 KSPROPERTY\_BDA 指定的切换频率\_LNB\_交换机\_频率，则 RF 调谐器应将命令发送到 LNB，以便切换到带内的 LOF。 然后，RF 调谐器会预计 LNB 设备会将传入 RF 信号的频率转移到使用 KSPROPERTY\_BDA\_LNB\_LOF\_高\_波段指定的高带 LOF 量。

同样，如果客户端发送 KSPROPERTY\_BDA\_RF\_调谐器\_频率请求，以将射频调谐器调整到特定的频率，此频率小于交换机频率，则 RF 调谐器应将命令发送到 LNB 以切换到低区 LOF。 然后，RF 调谐器会预计 LNB 设备会将传入 RF 信号的频率转移到使用 KSPROPERTY\_BDA\_LNB\_LOF\_LOW\_波段的低波段 LOF。

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

[**KSPROPERTY\_BDA\_LNB\_LOF\_高\_带区**](ksproperty-bda-lnb-lof-high-band.md)

[**KSPROPERTY\_BDA\_LNB\_LOF\_低\_带**](ksproperty-bda-lnb-lof-low-band.md)

[**KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)

 

 






