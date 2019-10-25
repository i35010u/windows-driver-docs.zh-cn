---
title: KSPROPERTY\_VPCONFIG\_MAXPIXELRATE
description: KSPROPERTY\_VPCONFIG\_MAXPIXELRATE 属性指定基于像素格式的最大像素速率，并指定连接的维度（高度宽度）。
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
ms.openlocfilehash: 473e02fcca6c70732b5751603ba0dcad68efba8b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842809"
---
# <a name="ksproperty_vpconfig_maxpixelrate"></a>KSPROPERTY\_VPCONFIG\_MAXPIXELRATE


KSPROPERTY\_VPCONFIG\_MAXPIXELRATE 属性指定基于像素格式的最大像素速率，并指定连接的维度（高度宽度）。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksvpmaxpixelrate" data-raw-source="[&lt;strong&gt;KSVPMAXPIXELRATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksvpmaxpixelrate)"><strong>KSVPMAXPIXELRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 KSVPMAXPIXELRATE 结构，描述视频端口支持的每秒像素的宽度、高度和最大数目。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSVPMAXPIXELRATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksvpmaxpixelrate)

 

 






