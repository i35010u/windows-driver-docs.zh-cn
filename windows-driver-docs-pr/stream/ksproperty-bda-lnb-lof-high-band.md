---
title: KSPROPERTY\_BDA\_LNB\_LOF\_高\_外
description: 客户端使用 KSPROPERTY\_BDA\_LNB\_LOF\_高\_外通知 RF 调谐器节点有关由适用于转换的低干扰块 (LNB) 设备的本地震荡频率 (LOF)传入的高外 RF 信号的频率。
ms.assetid: 77ee5ad8-330e-47a6-8fdb-6a4f9b3eef1d
keywords:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND 流式处理媒体设备
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
ms.openlocfilehash: b690e3823f424067ba06a595424b5968463ab59f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364849"
---
# <a name="kspropertybdalnblofhighband"></a>KSPROPERTY\_BDA\_LNB\_LOF\_高\_外


客户端使用 KSPROPERTY\_BDA\_LNB\_LOF\_高\_外通知 RF 调谐器节点有关由适用于转换的低干扰块 (LNB) 设备的本地震荡频率 (LOF)传入的高外 RF 信号的频率。

## <span id="ddk_ksproperty_bda_lnb_lof_high_band_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_LOF_HIGH_BAND_KS"></span>


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

**NodeId** KSP 成员\_节点指定 RF 调谐器节点的标识符。

属性值指定由高带内信号 LNB LOF。

LNB 收集反射了由卫星电视的 RF 信号、 将 RF 信号的频率向下移动高外 LOF 量，并将生成信号发送到 RF 调谐器。

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


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






