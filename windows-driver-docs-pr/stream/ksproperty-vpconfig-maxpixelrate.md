---
title: KSPROPERTY \_ VPCONFIG \_ MAXPIXELRATE
description: KSPROPERTY \_ VPCONFIG \_ MAXPIXELRATE 属性指定基于像素格式的最大像素速率，并按连接的高度) 指定维度 (宽度。
ms.assetid: 5a1e70b6-32ab-4a6c-82f7-3e6e828262a4
keywords:
- KSPROPERTY_VPCONFIG_MAXPIXELRATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_MAXPIXELRATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9c175aec27e240e305bd22d92c6d236f784aea5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104474"
---
# <a name="ksproperty_vpconfig_maxpixelrate"></a>KSPROPERTY \_ VPCONFIG \_ MAXPIXELRATE


KSPROPERTY \_ VPCONFIG \_ MAXPIXELRATE 属性指定基于像素格式的最大像素速率，并按连接的高度) 指定维度 (宽度。

## <span id="ddk_ksproperty_vpconfig_maxpixelrate_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_MAXPIXELRATE_KS"></span>


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
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksvpmaxpixelrate" data-raw-source="[&lt;strong&gt;KSVPMAXPIXELRATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksvpmaxpixelrate)"><strong>KSVPMAXPIXELRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSVPMAXPIXELRATE 结构，描述视频端口支持的每秒像素的宽度、高度和最大数目。

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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSVPMAXPIXELRATE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksvpmaxpixelrate)

