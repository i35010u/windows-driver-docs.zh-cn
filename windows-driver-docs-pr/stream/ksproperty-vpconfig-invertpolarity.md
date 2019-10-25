---
title: KSPROPERTY\_VPCONFIG\_INVERTPOLARITY
description: KSPROPERTY\_VPCONFIG\_INVERTPOLARITY 属性将切换全局极性标志，并强制反转视频端口。
ms.assetid: c0b69aa4-0f81-42b4-9a69-5afcf702f5f1
keywords:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9217c78dc893e90d223b32fff1b084b3829558a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842811"
---
# <a name="ksproperty_vpconfig_invertpolarity"></a>KSPROPERTY\_VPCONFIG\_INVERTPOLARITY


KSPROPERTY\_VPCONFIG\_INVERTPOLARITY 属性将切换全局极性标志，并强制反转视频端口。

## <span id="ddk_ksproperty_vpconfig_invertpolarity_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_INVERTPOLARITY_KS"></span>


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
<td><p>布尔型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）为布尔值。 指定**TRUE**以反转极性，或指定**FALSE**以防止反转极性。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VPCONFIG\_INVERTPOLARITY 属性请求返回状态\_SUCCESS，以指示成功完成。 否则，请求将返回相应的错误状态代码。

由于此功能与硬件相关，因此不使用此功能的模型必须返回状态\_未\_实现。

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

 

 






