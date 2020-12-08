---
title: KSPROPERTY \_ DVDSUBPIC \_
description: KSPROPERTY \_ DVDSUBPIC \_ b-hli 属性指定要更改的子画面或 screen 的矩形，包括颜色或对比度。
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
ms.openlocfilehash: cca25472764c6e9712a2c63d8047ceb2e17faaaf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795313"
---
# <a name="ksproperty_dvdsubpic_hli"></a>KSPROPERTY \_ DVDSUBPIC \_


KSPROPERTY \_ DVDSUBPIC \_ b-hli 属性指定要更改的子画面或 screen 的矩形，包括颜色或对比度。

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
<th>获取</th>
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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPHLI&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)"><strong>KSPROPERTY_SPHLI</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ SPHLI 结构，用于描述要更改的 DVD 突出显示信息。

<a name="remarks"></a>备注
-------

[**KSPROPERTY \_ SPHLI**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)结构描述了 DVD 突出显示信息中当前选定的按钮。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ SPHLI**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)

