---
title: KSPROPERTY\_VPCONFIG\_SETCONNECTINFO
description: KSPROPERTY\_VPCONFIG\_SETCONNECTINFO 属性设置视频端口配置和用户定义的连接信息。 它是一个指针，指向由 KSPROPERTY\_VPCONFIG\_GETCONNECTINFO 属性返回的 DDVIDEOPORTCONNECT 结构数组。
ms.assetid: 120f6889-cd67-4c05-b4b8-adab3efd7f2c
keywords:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e98ec6b7ff3815b740910ef17b66ab6d444683
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823662"
---
# <a name="ksproperty_vpconfig_setconnectinfo"></a>KSPROPERTY\_VPCONFIG\_SETCONNECTINFO


KSPROPERTY\_VPCONFIG\_SETCONNECTINFO 属性设置视频端口配置和用户定义的连接信息。 它是一个指针，指向由 KSPROPERTY\_VPCONFIG\_GETCONNECTINFO 属性返回的[**DDVIDEOPORTCONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)结构数组。

## <span id="ddk_ksproperty_vpconfig_setconnectinfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SETCONNECTINFO_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect" data-raw-source="[&lt;strong&gt;DDVIDEOPORTCONNECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)"><strong>DDVIDEOPORTCONNECT</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是描述视频端口连接配置的 DDVIDEOPORTCONNECT 结构。

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


[**DDVIDEOPORTCONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)

[**KSPROPERTY\_VPCONFIG\_GETCONNECTINFO**](ksproperty-vpconfig-getconnectinfo.md)

 

 






