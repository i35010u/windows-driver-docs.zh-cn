---
title: KSPROPERTY \_ DVDSUBPIC \_ 复合相比 \_
description: KSPROPERTY \_ DVDSUBPIC \_ 复合相比 \_ ON 属性启用或禁用显示子画面。
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
ms.openlocfilehash: f83c61672f21769def32e4c672368c614c8962b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839349"
---
# <a name="ksproperty_dvdsubpic_composit_on"></a>KSPROPERTY \_ DVDSUBPIC \_ 复合相比 \_


KSPROPERTY \_ DVDSUBPIC \_ 复合相比 \_ ON 属性启用或禁用显示子画面。

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
<td><p>KSPROPERTY_COMPOSIT_ON</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 \_ \_ (类型定义的布尔) 上的 KSPROPERTY 复合相比。 指定 **TRUE** 以启用子画面显示，或指定 **FALSE** 以关闭子画面显示。

<a name="remarks"></a>备注
-------

如果子画面显示处于禁用状态，则解码器仍必须对子画面数据进行解码，但不能显示它。 这便于在收到子画面命令时立即显示。

子画面数据命令流中有一个子画面命令，该命令可以覆盖 \_ 属性上的 KSPROPERTY DVDSUBPIC \_ 复合相比 \_ 。

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

