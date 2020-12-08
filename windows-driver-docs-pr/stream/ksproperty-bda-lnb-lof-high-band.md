---
title: KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层 \_
description: 客户端使用 KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层 \_ 通知 RF 调谐器节点 (LOF) ， (LNB) 设备，以便转移传入的带外 RF 信号的频率，这是由低噪音块使用的本地震荡频率。
keywords:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 681eade02c01fcb285b34a4cad6a8e7378fc9853
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822723"
---
# <a name="ksproperty_bda_lnb_lof_high_band"></a>KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层 \_


客户端使用 KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层 \_ 通知 RF 调谐器节点 (LOF) ， (LNB) 设备，以便转移传入的带外 RF 信号的频率，这是由低噪音块使用的本地震荡频率。

## <span id="ddk_ksproperty_bda_lnb_lof_high_band_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_LOF_HIGH_BAND_KS"></span>


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
<td><p>筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点标识号指定了 RF 调谐器节点的标识符。

属性值指定 LNB 用于带外信号的 LOF。

LNB 收集由卫星 dish 反射的射频信号，将 RF 信号的频率向下移动，并将生成的信号发送到 RF 调谐器。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

