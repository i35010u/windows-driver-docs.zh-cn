---
title: KSPROPERTY\_BDA\_LNB\_LOF\_低\_带
description: 客户端使用 KSPROPERTY\_BDA\_LNB\_LOF\_低\_带，通知 RF 调谐器节点有关低噪音块（LNB）设备使用的本地震荡频率（LOF）来改变传入的低压 RF 的频率引发.
ms.assetid: 96880a70-5c3f-4391-a613-a6a90d1605b4
keywords:
- KSPROPERTY_BDA_LNB_LOF_LOW_BAND 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_LOF_LOW_BAND
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bbebd07458e954a8fdcb1ccc491cd5e35095a6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845554"
---
# <a name="ksproperty_bda_lnb_lof_low_band"></a>KSPROPERTY\_BDA\_LNB\_LOF\_低\_带


客户端使用 KSPROPERTY\_BDA\_LNB\_LOF\_低\_带，通知 RF 调谐器节点有关低噪音块（LNB）设备使用的本地震荡频率（LOF）来改变传入的低压 RF 的频率引发.

## <span id="ddk_ksproperty_bda_lnb_lof_low_band_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_LOF_LOW_BAND_KS"></span>


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

KSP\_**节点的节点**标识指定 RF 调谐器节点的标识符。

属性值指定 LNB 用于带外信号的 LOF。

LNB 收集由卫星 dish 反射的射频信号，将 RF 信号的频率向下移动，并将其向下移动，并将生成的信号发送到 RF 调谐器。

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

 

 






