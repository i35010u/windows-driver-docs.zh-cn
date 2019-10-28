---
title: KSPROPERTY\_BDA\_示例\_时间
description: 客户端使用 KSPROPERTY\_BDA\_示例\_时间来确定平均信号级别和质量的采样时间。
ms.assetid: 53252e11-2a18-42d5-aed8-99052a2b0f21
keywords:
- KSPROPERTY_BDA_SAMPLE_TIME 流媒体设备
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
ms.openlocfilehash: 6b3b0ccf4f70ec576eb9962df92e8a01b7da2fe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838071"
---
# <a name="ksproperty_bda_sample_time"></a>KSPROPERTY\_BDA\_示例\_时间


客户端使用 KSPROPERTY\_BDA\_示例\_时间来确定平均信号级别和质量的采样时间。

## <span id="ddk_ksproperty_bda_sample_time_ks"></span><span id="DDK_KSPROPERTY_BDA_SAMPLE_TIME_KS"></span>


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

返回的值指定采样时间（以毫秒为单位）。

每次客户端请求 "信号统计信息" 属性时，节点应报告最后 n 毫秒的平均值，其中 n 是 KSPROPERTY\_BDA\_示例\_时间指示的值。 如果未设置时间值，或者如果驱动程序不支持 KSPROPERTY\_BDA\_示例\_时间，则驱动程序应默认为100毫秒的采样时间。

该驱动程序可以报告最近完成的采样期间的时间值。

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

[**KSPROPERTY\_BDA\_信号\_强度**](ksproperty-bda-signal-strength.md)

 

 






