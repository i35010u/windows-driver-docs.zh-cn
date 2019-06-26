---
title: KSPROPERTY\_DVDSUBPIC\_PALETTE
description: KSPROPERTY\_DVDSUBPIC\_PALETTE 属性指定的子画面流使用的调色板。
ms.assetid: 9dafb956-4adf-45ec-b997-8ed35991f7d8
keywords:
- KSPROPERTY_DVDSUBPIC_PALETTE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_PALETTE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b654f80729a706be9b81c5820053a666fa336480
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354888"
---
# <a name="kspropertydvdsubpicpalette"></a>KSPROPERTY\_DVDSUBPIC\_PALETTE


KSPROPERTY\_DVDSUBPIC\_PALETTE 属性指定的子画面流使用的调色板。

## <span id="ddk_ksproperty_dvdsubpic_palette_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_PALETTE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sppal" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPPAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sppal)"><strong>KSPROPERTY_SPPAL</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_SPPAL 结构描述要使用的 YUV 颜色格式中显示的子画面的颜色调色板。

<a name="remarks"></a>备注
-------

[ **KSPROPERTY\_SPPAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sppal)结构包含一个 16 YUV 元素的数组。 这些元素对应于请求的子画面命令流中的 4 位颜色数字。

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


[**KSPROPERTY\_SPPAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksproperty_sppal)

 

 






