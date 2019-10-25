---
title: KSPROPERTY\_BDA\_信号\_强度
description: 客户端使用 KSPROPERTY\_BDA\_信号\_强度来确定 mDb 中信号的载波强度（分贝（DB）的1/1000）。
ms.assetid: b8b71135-cc0b-4a59-940a-dd766cab3305
keywords:
- KSPROPERTY_BDA_SIGNAL_STRENGTH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_STRENGTH
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d9957d05a5d9b83b52a6a9732b3897d3013c26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843603"
---
# <a name="ksproperty_bda_signal_strength"></a>KSPROPERTY\_BDA\_信号\_强度


客户端使用 KSPROPERTY\_BDA\_信号\_强度来确定 mDb 中信号的载波强度（分贝（DB）的1/1000）。

## <span id="ddk_ksproperty_bda_signal_strength_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_STRENGTH_KS"></span>


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
<td><p>固定或筛选</p></td>
<td><p>KSP_NODE</p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**1 指定了控制节点的标识符，或设置为−1以指定 pin。

返回的值指定 mDb 中信号的载波强度。

对于给定类型的广播网络，"强度" 的长度为 "预期"。 Subnominal 强项报告为正面 mDb。 超级标称强度报告为否定 mDb。

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

 

 






