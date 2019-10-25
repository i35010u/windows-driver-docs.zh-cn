---
title: KSPROPERTY\_BDA\_信号\_锁定
description: 客户端使用 KSPROPERTY\_BDA\_信号\_锁定，以确定是否可以锁定信号。
ms.assetid: 98023f83-2e90-4649-8e85-3e7b7f26b01d
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCKED 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCKED
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7364834dfb4bff30719f77da94509c33f459e417
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838065"
---
# <a name="ksproperty_bda_signal_locked"></a>KSPROPERTY\_BDA\_信号\_锁定


客户端使用 KSPROPERTY\_BDA\_信号\_锁定，以确定是否可以锁定信号。

## <span id="ddk_ksproperty_bda_signal_locked_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_LOCKED_KS"></span>


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
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**1 指定了控制节点的标识符，或设置为−1以指定 pin。

返回的值指示是否可以锁定信号。 如果信号可以锁定，**则返回 TRUE** ，否则返回**FALSE** 。

如果 RF 调谐器节点返回**TRUE**，则通常会指示阶段锁（PLL）锁。

如果某个解调器节点返回**TRUE**，则指示至少有20% 的信号质量。

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

[**KSPROPERTY\_BDA\_信号\_质量**](ksproperty-bda-signal-quality.md)

 

 






