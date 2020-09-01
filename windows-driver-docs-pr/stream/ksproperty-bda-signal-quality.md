---
title: KSPROPERTY \_ BDA \_ 信号 \_ 质量
description: 客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 质量来确定从信号中成功提取的数据量（以百分比形式）。
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
ms.openlocfilehash: e6ea11d5eafcab6c493a94d97382af4807a83276
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190565"
---
# <a name="ksproperty_bda_signal_quality"></a>KSPROPERTY \_ BDA \_ 信号 \_ 质量


客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 质量来确定从信号中成功提取的数据量（以百分比形式）。

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
<th>获取</th>
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
<td><p>固定或筛选</p></td>
<td><p>KSP_NODE</p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

KSP **NodeId** \_ 节点的节点1指定了控制节点的标识符，或设置为−1以指定 pin。

返回的值指定以百分比形式从信号中提取的数据。

Demodulation 节点通常会报告信号质量，这表示可以从信号中提取原始数据的多少。

对于模拟信号，可以通过检查水平同步 (HSync) 和垂直同步 (VSync) 的时间来计算此百分比，还可以通过查看水平消隐 (HBlanking) 和垂直对齐 () 中包含的信息来计算此百分比。

对于数字信号，可以通过检查数据包循环冗余检查 (CRC) 并转发错误更正 (FEC) 置信度值，来计算此百分比，如下所示：

-   100% 非常理想。

-   95百分比显示呈现时几乎难察觉) 项目的 (。

-   90% 包含可轻松查看的足够数量的项目。

-   80% 是可查看的最低级别。

-   60% 是数据服务的最低级别，包括 (EPG) 接收电子收视指南，才能正常工作。

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
<td><p>Header</p></td>
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

