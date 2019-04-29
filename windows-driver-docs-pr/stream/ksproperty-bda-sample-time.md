---
title: KSPROPERTY\_BDA\_SAMPLE\_TIME
description: 客户端使用 KSPROPERTY\_BDA\_示例\_时间来确定对哪些信号平均级别和质量的示例时间。
ms.assetid: 53252e11-2a18-42d5-aed8-99052a2b0f21
keywords:
- KSPROPERTY_BDA_SAMPLE_TIME 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SAMPLE_TIME
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c3e5319a69de6c4e20459377ac5d8f527daeab5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389268"
---
# <a name="kspropertybdasampletime"></a>KSPROPERTY\_BDA\_SAMPLE\_TIME


客户端使用 KSPROPERTY\_BDA\_示例\_时间来确定对哪些信号平均级别和质量的示例时间。

## <span id="ddk_ksproperty_bda_sample_time_ks"></span><span id="DDK_KSPROPERTY_BDA_SAMPLE_TIME_KS"></span>


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

返回的值以毫秒为单位指定的示例时间。

每次客户端请求信号 statistics 属性时，该节点应报告其中 n 是 KSPROPERTY 所指示的值的最后一个 n 毫秒的平均值\_BDA\_示例\_时间。 如果未不设置任何时间值或驱动程序不支持 KSPROPERTY\_BDA\_示例\_时间，该驱动程序应默认为 100 毫秒的采样时间。

该驱动程序可以报告的最近完成的采样期间的时间值。

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

[**KSPROPERTY\_BDA\_信号\_质量**](ksproperty-bda-signal-quality.md)

[**KSPROPERTY\_BDA\_信号\_强度**](ksproperty-bda-signal-strength.md)

 

 






