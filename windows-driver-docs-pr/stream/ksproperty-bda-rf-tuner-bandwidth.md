---
title: KSPROPERTY\_BDA\_RF\_调谐器\_带宽
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_带宽来控制调谐器节点的带宽设置。
ms.assetid: 34feb05d-c1dc-4ce1-86bf-d7d33920befd
keywords:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412eac5587fa0da8c8c8018d203d4af33ef14ad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838086"
---
# <a name="ksproperty_bda_rf_tuner_bandwidth"></a>KSPROPERTY\_BDA\_RF\_调谐器\_带宽


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_带宽来控制调谐器节点的带宽设置。

## <span id="ddk_ksproperty_bda_rf_tuner_bandwidth_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_BANDWIDTH_KS"></span>


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
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识符指定调谐器节点的标识符。

属性值指定要设置的带宽。 带宽是用于传输信号或相关信号组的频率范围。 换句话说，可以一次传输的信息量。

通过以下方式指定 KSPROPERTY\_BDA\_RF\_调谐器\_带宽属性：

-   BDA\_更改\_带宽\_未\_集（−1）指示未设置带宽。

-   BDA\_更改\_带宽\_\_未定义（0）指示未定义带宽。

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

 

 






