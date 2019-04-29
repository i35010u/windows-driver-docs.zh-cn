---
title: KSPROPERTY\_BDA\_信号\_存在
description: 客户端使用 KSPROPERTY\_BDA\_信号\_来确定是否存在信号运营商。
ms.assetid: d3dbe0f7-a308-48e2-9751-0131fa2b512d
keywords:
- KSPROPERTY_BDA_SIGNAL_PRESENT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_PRESENT
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21958bb6a5b9efa2cb061d6b0a619c43ffb5cb0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389235"
---
# <a name="kspropertybdasignalpresent"></a>KSPROPERTY\_BDA\_信号\_存在


客户端使用 KSPROPERTY\_BDA\_信号\_来确定是否存在信号运营商。

## <span id="ddk_ksproperty_bda_signal_present_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_PRESENT_KS"></span>


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

返回的值指示信号承运人是否存在。 返回 **，则返回 TRUE**信号承运人是否存在并**FALSE**否则为。 RF 调谐器节点应提供此有关的指示。

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

 

 






