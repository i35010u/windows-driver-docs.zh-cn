---
title: KSPROPERTY\_BDA\_信号\_锁定\_CAP
description: 客户端使用 KSPROPERTY\_BDA\_信号\_锁定\_CAP 来确定驱动程序可以为信号支持的锁类型。
ms.assetid: 753f1a3c-5308-49a6-96ee-f7d0090f021a
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0e673d3e0e1c1201c27b7ed04028948be8de066
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838068"
---
# <a name="ksproperty_bda_signal_lock_caps"></a>KSPROPERTY\_BDA\_信号\_锁定\_CAP


客户端使用 KSPROPERTY\_BDA\_信号\_锁定\_CAP 来确定驱动程序可以为信号支持的锁类型。

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
<td><p>固定或筛选</p></td>
<td><p>KSP_NODE</p></td>
<td><p>一个32位值，其中包含<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a>类型的值的按位 "或"</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**1 指定了控制节点的标识符，或设置为−1以指定 pin。

返回的32位值是[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)类型的值的按位 "或"，指示驱动程序支持的锁类型。

RF 调谐器节点应提供此指示。

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


[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_信号\_锁定\_类型**](ksproperty-bda-signal-lock-type.md)

 

 






