---
title: KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO
description: KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO 属性设置视频端口配置和用户定义的连接信息。 它是指向 KSPROPERTY \_ VPCONFIG GETCONNECTINFO 属性返回的 DDVIDEOPORTCONNECT 结构的数组的指针 \_ 。
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
ms.openlocfilehash: 2140f386bc34f7e5a2aa6d00bf65ae52695e9c38
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190851"
---
# <a name="ksproperty_vpconfig_setconnectinfo"></a>KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO


KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO 属性设置视频端口配置和用户定义的连接信息。 它是指向 KSPROPERTY [**DDVIDEOPORTCONNECT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect) \_ VPCONFIG GETCONNECTINFO 属性返回的 DDVIDEOPORTCONNECT 结构的数组的指针 \_ 。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect" data-raw-source="[&lt;strong&gt;DDVIDEOPORTCONNECT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)"><strong>DDVIDEOPORTCONNECT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是描述视频端口连接配置的 DDVIDEOPORTCONNECT 结构。

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


[**DDVIDEOPORTCONNECT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)

[**KSPROPERTY \_ VPCONFIG \_ GETCONNECTINFO**](ksproperty-vpconfig-getconnectinfo.md)

 

