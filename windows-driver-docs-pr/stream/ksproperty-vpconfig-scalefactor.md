---
title: KSPROPERTY \_ VPCONFIG \_ SCALEFACTOR
description: KSPROPERTY \_ VPCONFIG \_ SCALEFACTOR 属性将视频端口尺寸设置为用户定义的规范。
ms.assetid: 0fbfedc8-9dff-4c7c-910f-507b84614e47
keywords:
- KSPROPERTY_VPCONFIG_SCALEFACTOR 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SCALEFACTOR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae349c8957150be2829e5c80d8dc4408a406fb15
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191043"
---
# <a name="ksproperty_vpconfig_scalefactor"></a>KSPROPERTY \_ VPCONFIG \_ SCALEFACTOR


KSPROPERTY \_ VPCONFIG \_ SCALEFACTOR 属性将视频端口尺寸设置为用户定义的规范。

## <span id="ddk_ksproperty_vpconfig_scalefactor_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SCALEFACTOR_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpsize" data-raw-source="[&lt;strong&gt;KS_AMVPSIZE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpsize)"><strong>KS_AMVPSIZE</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KS \_ AMVPSIZE 结构，它指定视频端口的宽度和高度。

<a name="remarks"></a>注解
-------

当 KSPROPSETID VPVBIConfig 使用此属性时 \_ ，所有属性请求都必须返回 \_ 未实现的状态 \_ 。

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

[**KS \_ AMVPSIZE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpsize)

 

