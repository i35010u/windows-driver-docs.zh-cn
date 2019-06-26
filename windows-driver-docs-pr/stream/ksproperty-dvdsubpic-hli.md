---
title: KSPROPERTY\_DVDSUBPIC\_HLI
description: KSPROPERTY\_DVDSUBPIC\_HLI 属性指定的矩形的子画面或屏幕，若要更改，包括颜色或对比度。
ms.assetid: c3498ff8-11fe-4f53-8317-83a487684ac7
keywords:
- KSPROPERTY_DVDSUBPIC_HLI 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_HLI
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 778d4f9eaed631648b8b1f491491d2b34c00b9f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354886"
---
# <a name="kspropertydvdsubpichli"></a>KSPROPERTY\_DVDSUBPIC\_HLI


KSPROPERTY\_DVDSUBPIC\_HLI 属性指定的矩形的子画面或屏幕，若要更改，包括颜色或对比度。

## <span id="ddk_ksproperty_dvdsubpic_hli_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_HLI_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sphli" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPHLI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sphli)"><strong>KSPROPERTY_SPHLI</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_SPHLI 结构描述 DVD 突出显示更改的信息。

<a name="remarks"></a>备注
-------

[ **KSPROPERTY\_SPHLI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sphli)结构描述从 DVD 突出显示信息的当前所选的按钮。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_SPHLI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sphli)

 

 






