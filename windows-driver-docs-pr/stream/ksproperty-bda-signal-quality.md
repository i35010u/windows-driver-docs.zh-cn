---
title: KSPROPERTY\_BDA\_信号\_质量
description: 客户端使用 KSPROPERTY\_BDA\_信号\_质量来确定从信号中成功提取的数据量（以百分比形式）。
ms.assetid: 8967400d-3a10-475a-997a-d756837c3438
keywords:
- KSPROPERTY_BDA_SIGNAL_QUALITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_QUALITY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1bbafdb5bd5c60b1dfd1025b841f250d11d433a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843606"
---
# <a name="ksproperty_bda_signal_quality"></a>KSPROPERTY\_BDA\_信号\_质量


客户端使用 KSPROPERTY\_BDA\_信号\_质量来确定从信号中成功提取的数据量（以百分比形式）。

## <span id="ddk_ksproperty_bda_signal_quality_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_QUALITY_KS"></span>


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

返回的值指定以百分比形式从信号中提取的数据。

Demodulation 节点通常会报告信号质量，这表示可以从信号中提取原始数据的多少。

对于模拟信号，可以通过检查水平同步（HSync）和垂直同步（VSync）的时间，并查看水平消隐（HBlanking）和垂直消隐（VBlanking）中包含的信息来计算此百分比。间隔.

对于数字信号，可以通过检查数据包循环冗余检查（CRC）和正向纠错（FEC）置信度值来计算此百分比，如下所示：

-   100% 非常理想。

-   95百分比显示呈现时非常少（几乎难察觉）的项目。

-   90% 包含可轻松查看的足够数量的项目。

-   80% 是可查看的最低级别。

-   60% 是数据服务（包括接收电子收视指南（EPG））所需的最低级别。

-   20% 表示该解调器知道存在正确的调制信号，但无法生成足够多的数据。

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

 

 






