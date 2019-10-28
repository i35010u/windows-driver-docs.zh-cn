---
title: KSPROPERTY\_BDA\_信号\_锁定\_类型
description: 客户端使用 KSPROPERTY\_BDA\_信号\_锁定\_类型来确定信号的当前锁定类型。
ms.assetid: 2ddf49c4-f0d1-4918-b564-719c695a83ac
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94cbfbe634e332f445d40066d05cc070b5763a60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838070"
---
# <a name="ksproperty_bda_signal_lock_type"></a>KSPROPERTY\_BDA\_信号\_锁定\_类型


客户端使用 KSPROPERTY\_BDA\_信号\_锁定\_类型来确定信号的当前锁定类型。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**1 指定了控制节点的标识符，或设置为−1以指定 pin。

返回的[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)类型的值标识当前锁类型。

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

[**KSPROPERTY\_BDA\_信号\_锁定\_CAP**](ksproperty-bda-signal-lock-caps.md)

 

 






