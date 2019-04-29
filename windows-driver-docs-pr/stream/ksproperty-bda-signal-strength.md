---
title: KSPROPERTY\_BDA\_信号\_强度
description: 客户端使用 KSPROPERTY\_BDA\_信号\_强度来确定在 mDb (1/1000 分贝 (DB)) 中的信号的运营商强度。
ms.assetid: b8b71135-cc0b-4a59-940a-dd766cab3305
keywords:
- KSPROPERTY_BDA_SIGNAL_STRENGTH 流式处理媒体设备
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
ms.openlocfilehash: 62501a1a3ab272be4c1da73981a1d139f80b10ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357014"
---
# <a name="kspropertybdasignalstrength"></a>KSPROPERTY\_BDA\_信号\_强度


客户端使用 KSPROPERTY\_BDA\_信号\_强度来确定在 mDb (1/1000 分贝 (DB)) 中的信号的运营商强度。

## <span id="ddk_ksproperty_bda_signal_strength_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_STRENGTH_KS"></span>


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
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定的控制节点的标识符，或设置为 − 1，以指定一个 pin。

返回的值在 mDb 中指定的信号的运营商强度。

0 的强度为给定类型的广播网络预期结果名义强度。 Subnominal 优势均报告为正 mDb。 超名义优势均报告为负 mDb。

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


[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






