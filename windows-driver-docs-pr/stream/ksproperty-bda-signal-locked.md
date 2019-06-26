---
title: KSPROPERTY\_BDA\_信号\_已锁定
description: 客户端使用 KSPROPERTY\_BDA\_信号\_已锁定，以确定是否可以锁定信号。
ms.assetid: 98023f83-2e90-4649-8e85-3e7b7f26b01d
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCKED 流式处理媒体设备
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
ms.openlocfilehash: 8e64f81c5d3b92712527310673bbb1ac56db4363
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361131"
---
# <a name="kspropertybdasignallocked"></a>KSPROPERTY\_BDA\_信号\_已锁定


客户端使用 KSPROPERTY\_BDA\_信号\_已锁定，以确定是否可以锁定信号。

## <span id="ddk_ksproperty_bda_signal_locked_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_LOCKED_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin 或筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定的控制节点的标识符，或设置为 − 1，以指定一个 pin。

返回的值指示是否可以锁定信号。 返回 **，则返回 TRUE**如果信号可以锁定并**FALSE**否则为。

如果 RF 调谐器节点返回 **，则返回 TRUE**，通常表示阶段-锁定-循环 (PLL) 锁。

如果解调器节点返回 **，则返回 TRUE**，指示至少 20%的信号质量。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_信号\_质量**](ksproperty-bda-signal-quality.md)

 

 






