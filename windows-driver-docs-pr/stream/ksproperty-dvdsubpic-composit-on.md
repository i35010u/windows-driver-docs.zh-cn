---
title: KSPROPERTY\_DVDSUBPIC\_复合\_ON
description: KSPROPERTY\_DVDSUBPIC\_复合\_属性上启用或禁用子画面的显示。
ms.assetid: f9dcf8ca-44fb-45e2-9993-813439c742ef
keywords:
- KSPROPERTY_DVDSUBPIC_COMPOSIT_ON 流式处理媒体设备
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
ms.openlocfilehash: ad7c137a9059ab600eec0ccbff32b06d8445ffc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521794"
---
# <a name="kspropertydvdsubpiccompositon"></a>KSPROPERTY\_DVDSUBPIC\_复合\_ON


KSPROPERTY\_DVDSUBPIC\_复合\_属性上启用或禁用子画面的显示。

## <span id="ddk_ksproperty_dvdsubpic_composit_on_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_COMPOSIT_ON_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>KSPROPERTY_COMPOSIT_ON</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_复合\_上 （定义类型的布尔值）。 指定 **，则返回 TRUE**若要启用子画面显示，或指定**FALSE**要关闭子画面显示。

<a name="remarks"></a>备注
-------

如果禁用子画面显示解码器必须仍解码的子画面数据但不是显示。 接收到的子画面启用命令时，这样便于即时显示。

可以重写 KSPROPERTY 子画面数据命令流中没有强制显示子画面命令\_DVDSUBPIC\_复合\_属性上。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





