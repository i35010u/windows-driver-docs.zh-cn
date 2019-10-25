---
title: KSPROPERTY\_DVDSUBPIC\_调色板
description: KSPROPERTY\_DVDSUBPIC\_调色板属性指定子画面流使用的调色板。
ms.assetid: 9dafb956-4adf-45ec-b997-8ed35991f7d8
keywords:
- KSPROPERTY_DVDSUBPIC_PALETTE 流媒体设备
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
ms.openlocfilehash: fb65bbc1d054938ab882147671409cb3d7adf7fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827075"
---
# <a name="ksproperty_dvdsubpic_palette"></a>KSPROPERTY\_DVDSUBPIC\_调色板


KSPROPERTY\_DVDSUBPIC\_调色板属性指定子画面流使用的调色板。

## <span id="ddk_ksproperty_dvdsubpic_palette_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_PALETTE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPPAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal)"><strong>KSPROPERTY_SPPAL</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 KSPROPERTY\_SPPAL 结构，描述用于子画面以 YUV 颜色格式显示的调色板。

<a name="remarks"></a>备注
-------

[**KSPROPERTY\_SPPAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal)结构包含一个 16 YUV 元素数组。 这些元素对应于在子画面命令流中请求的4位颜色号。

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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_SPPAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal)

 

 






