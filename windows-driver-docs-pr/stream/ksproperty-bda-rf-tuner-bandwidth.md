---
title: KSPROPERTY\_BDA\_RF\_TUNER\_BANDWIDTH
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_带宽控制调谐器节点的带宽设置。
ms.assetid: 34feb05d-c1dc-4ce1-86bf-d7d33920befd
keywords:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH 流式处理媒体设备
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
ms.openlocfilehash: 3b5a343424a291448b09f95f65b926eda4392d05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329979"
---
# <a name="kspropertybdarftunerbandwidth"></a>KSPROPERTY\_BDA\_RF\_TUNER\_BANDWIDTH


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_带宽控制调谐器节点的带宽设置。

## <span id="ddk_ksproperty_bda_rf_tuner_bandwidth_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_BANDWIDTH_KS"></span>


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
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定调谐器节点的标识符。

属性值指定的带宽设置。 带宽是用来传输信号或一组相互关联的信号的频率的范围。 换而言之，可以一次传输的信息量。

指定 KSPROPERTY\_BDA\_RF\_调谐器\_带宽属性：

-   BDA\_CHAN\_带宽\_不\_设定 (− 1)，表示未设置带宽。

-   BDA\_CHAN\_带宽\_不\_定义 (0) 指示未定义带宽。

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

 

 






