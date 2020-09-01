---
title: KSPROPERTY \_ VPCONFIG \_ INVERTPOLARITY
description: KSPROPERTY \_ VPCONFIG \_ INVERTPOLARITY 属性用于切换全局极性标志，并强制反转视频端口。
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
ms.openlocfilehash: e118840b2b216d3cd57dcb8bb06bd4defe38ff57
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185333"
---
# <a name="ksproperty_vpconfig_invertpolarity"></a>KSPROPERTY \_ VPCONFIG \_ INVERTPOLARITY


KSPROPERTY \_ VPCONFIG \_ INVERTPOLARITY 属性用于切换全局极性标志，并强制反转视频端口。

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
<td><p>布尔</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是一个布尔值。 指定 **TRUE** 以反转极性，或指定 **FALSE** 以防止反转极性。

<a name="remarks"></a>注解
-------

KSPROPERTY \_ VPCONFIG \_ INVERTPOLARITY 属性请求返回状态 " \_ 成功" 以指示成功完成。 否则，请求将返回相应的错误状态代码。

由于此功能与硬件相关，因此不使用此功能的模型必须返回 \_ 未 \_ 实现的状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

