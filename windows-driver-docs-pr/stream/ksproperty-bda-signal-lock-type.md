---
title: KSPROPERTY\_BDA\_信号\_锁\_类型
description: 客户端使用 KSPROPERTY\_BDA\_信号\_锁\_类型，以确定当前的锁类型的信号。
ms.assetid: 2ddf49c4-f0d1-4918-b564-719c695a83ac
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE 流式处理媒体设备
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
ms.openlocfilehash: 0233bb16d7c4e18385c675482abfd0aa7b5e5a55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361123"
---
# <a name="kspropertybdasignallocktype"></a>KSPROPERTY\_BDA\_信号\_锁\_类型


客户端使用 KSPROPERTY\_BDA\_信号\_锁\_类型，以确定当前的锁类型的信号。

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
<td><p>否</p></td>
<td><p>Pin 或筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定的控制节点的标识符，或设置为 − 1，以指定一个 pin。

返回[ **BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)-类型化的值标识当前的锁类型。

RF 调谐器节点应提供此有关的指示。

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


[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_信号\_锁\_CAP**](ksproperty-bda-signal-lock-caps.md)

 

 






