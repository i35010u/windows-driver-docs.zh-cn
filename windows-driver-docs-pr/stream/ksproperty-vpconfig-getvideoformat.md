---
title: KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT
description: KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT 属性检索受支持像素格式的数组。
ms.assetid: 74cc8cbc-cd81-43e1-ba15-3105a4c70808
keywords:
- KSPROPERTY_VPCONFIG_GETVIDEOFORMAT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_GETVIDEOFORMAT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e09eb1a2ddf132a3d4b9efb6a4156bf007e74c66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842812"
---
# <a name="ksproperty_vpconfig_getvideoformat"></a>KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT


KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT 属性检索受支持像素格式的数组。

## <span id="ddk_ksproperty_vpconfig_getvideoformat_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_GETVIDEOFORMAT_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat" data-raw-source="[&lt;strong&gt;DDPIXELFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)"><strong>DDPIXELFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是描述视频端口像素格式的 DDPIXELFORMAT 结构。

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

[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)

 

 






