---
title: KSPROPERTY\_DVDSUBPIC\_
description: KSPROPERTY\_DVDSUBPIC\_B-HLI 属性指定要更改的子画面或 screen 的矩形，包括颜色或对比度。
ms.assetid: c3498ff8-11fe-4f53-8317-83a487684ac7
keywords:
- KSPROPERTY_DVDSUBPIC_HLI 流媒体设备
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
ms.openlocfilehash: b2eb82b02be16ddddfdfdf08b4473c133108f1eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827081"
---
# <a name="ksproperty_dvdsubpic_hli"></a>KSPROPERTY\_DVDSUBPIC\_


KSPROPERTY\_DVDSUBPIC\_B-HLI 属性指定要更改的子画面或 screen 的矩形，包括颜色或对比度。

## <span id="ddk_ksproperty_dvdsubpic_hli_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_HLI_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPHLI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)"><strong>KSPROPERTY_SPHLI</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 KSPROPERTY\_SPHLI 结构，描述要更改的 DVD 突出显示信息。

<a name="remarks"></a>备注
-------

[**KSPROPERTY\_SPHLI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)结构描述了 DVD 突出显示信息中当前选定的按钮。

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


[**KSPROPERTY\_SPHLI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)

 

 






