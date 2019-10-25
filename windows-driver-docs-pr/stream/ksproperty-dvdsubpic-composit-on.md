---
title: KSPROPERTY\_DVDSUBPIC\_复合相比\_
description: KSPROPERTY\_DVDSUBPIC\_复合相比\_属性启用或禁用显示子画面。
ms.assetid: f9dcf8ca-44fb-45e2-9993-813439c742ef
keywords:
- KSPROPERTY_DVDSUBPIC_COMPOSIT_ON 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_COMPOSIT_ON
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65352100f3998f77d4a9c70e637d3649d155d59c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827120"
---
# <a name="ksproperty_dvdsubpic_composit_on"></a>KSPROPERTY\_DVDSUBPIC\_复合相比\_


KSPROPERTY\_DVDSUBPIC\_复合相比\_属性启用或禁用显示子画面。

## <span id="ddk_ksproperty_dvdsubpic_composit_on_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_COMPOSIT_ON_KS"></span>


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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>KSPROPERTY_COMPOSIT_ON</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSPROPERTY\_复合相比\_（类型定义的布尔值）。 指定**TRUE**以启用子画面显示，或指定**FALSE**以关闭子画面显示。

<a name="remarks"></a>备注
-------

如果子画面显示处于禁用状态，则解码器仍必须对子画面数据进行解码，但不能显示它。 这便于在收到子画面命令时立即显示。

子画面数据命令流中有一个强制显示子画面命令，该命令可以覆盖 KSPROPERTY\_DVDSUBPIC\_复合相比\_属性。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

 

 





