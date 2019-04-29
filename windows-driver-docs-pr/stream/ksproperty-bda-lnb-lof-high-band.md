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
ms.openlocfilehash: 24728d55e8e00f36c353f9209b6a4ed4b2c0aa71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359649"
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


[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






